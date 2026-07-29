async function adminEnrollStudent() {
  const maktabId = document.getElementById("s_maktabId").value;
  const name = document.getElementById("s_name").value;
  const age = parseInt(document.getElementById("s_age").value);
  const address = document.getElementById("s_address").value;
  const guardianPhone = document.getElementById("s_phone").value;

  if (!maktabId || !name || !age || !guardianPhone) { alert("Maktab ID, name, age and guardian phone are required!"); return; }

  try {
    const res = await fetch(`${API}/maktabs/${maktabId}/students`, {
      method: "POST",
      headers: { "Content-Type": "application/json", "Authorization": `Bearer ${token}` },
      body: JSON.stringify({ name, age, address, guardianPhone }),
    });
    const data = await res.json();

    if (data.success) {
      alert("Student enrolled successfully!");
      document.querySelectorAll("#enrollStudentTab input").forEach(i => i.value = "");
    } else {
      alert(data.message);
    }
  } catch (err) {
    alert("Failed to enroll student.");
  }
}

async function adminAddFunding() {
  const type = document.getElementById("f_type").value;
  const id = document.getElementById("f_id").value;
  const donorName = document.getElementById("f_donor").value || "Anonymous";
  const amount = Number(document.getElementById("f_amount").value);
  const note = document.getElementById("f_note").value;

  if (!id || !amount) { alert("ID and amount are required!"); return; }

  const url = type === "mosque" 
    ? `${API}/mosques/${id}/funding` 
    : `${API}/maktabs/${id}/funding`;

  try {
    const res = await fetch(url, {
      method: "POST",
      headers: { "Content-Type": "application/json", "Authorization": `Bearer ${token}` },
      body: JSON.stringify({ donorName, amount, note }),
    });
    const data = await res.json();

    if (data.success) {
      alert("Funding added successfully!");
      document.querySelectorAll("#addFundingTab input").forEach(i => i.value = "");
    } else {
      alert(data.message);
    }
  } catch (err) {
    alert("Failed to add funding.");
  }
}

async function adminGetStudents() {
  const maktabId = document.getElementById("v_maktabId").value;
  if (!maktabId) { alert("Please enter a Maktab ID!"); return; }

  const div = document.getElementById("studentResults");
  div.innerHTML = "<p>Loading...</p>";

  try {
    const res = await fetch(`${API}/maktabs/${maktabId}/students`);
    const data = await res.json();

    if (data.count === 0) {
      div.innerHTML = "<p>No students found.</p>";
      return;
    }

    div.innerHTML = data.data.map(s => `
      <div class="card">
        <h3>👤 ${s.name}</h3>
        <p>🎂 Age: ${s.age}</p>
        ${s.address ? `<p>📍 ${s.address}</p>` : ""}
        <p>📞 Guardian: ${s.guardianPhone}</p>
        <p>📅 Enrolled: ${new Date(s.enrolledAt).toLocaleDateString()}</p>
      </div>
    `).join("");
  } catch (err) {
    div.innerHTML = "<p>Failed to load students.</p>";
  }
}

async function adminGetFunding() {
  const type = document.getElementById("v_fundType").value;
  const id = document.getElementById("v_fundId").value;
  if (!id) { alert("Please enter an ID!"); return; }

  const div = document.getElementById("fundingResults");
  div.innerHTML = "<p>Loading...</p>";

  const url = type === "mosque"
    ? `${API}/mosques/${id}/funding`
    : `${API}/maktabs/${id}/funding`;

  try {
    const res = await fetch(url);
    const data = await res.json();

    if (data.count === 0) {
      div.innerHTML = "<p>No funding records found.</p>";
      return;
    }

    div.innerHTML = `
      <div class="card">
        <h3>💰 Total: ${data.totalAmount} BDT</h3>
        <p>📊 ${data.count} donation(s)</p>
      </div>
      ${data.data.map(f => `
        <div class="card">
          <h3>👤 ${f.donorName}</h3>
          <p>💵 Amount: ${f.amount} BDT</p>
          ${f.note ? `<p>📝 ${f.note}</p>` : ""}
          <p>📅 ${new Date(f.donatedAt).toLocaleDateString()}</p>
        </div>
      `).join("")}
    `;
  } catch (err) {
    div.innerHTML = "<p>Failed to load funding.</p>";
  }
}

async function adminDelete() {
  const type = document.getElementById("d_type").value;
  const id = document.getElementById("d_id").value;

  if (!id) { alert("Please enter an ID!"); return; }
  if (!confirm(`Are you sure you want to delete this ${type}?`)) return;

  const urls = {
    mosque: `${API}/mosques/${id}`,
    maktab: `${API}/maktabs/${id}`,
    event: `${API}/events/${id}`
  };

  try {
    const res = await fetch(urls[type], {
      method: "DELETE",
      headers: { "Authorization": `Bearer ${token}` }
    });
    const data = await res.json();

    if (data.success) {
      alert(`${type} deleted successfully!`);
      document.getElementById("d_id").value = "";
    } else {
      alert(data.message);
    }
  } catch (err) {
    alert(`Failed to delete ${type}.`);
  }
}
