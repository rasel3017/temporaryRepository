<button class="donate-btn" onclick="showDonateForm('mosque', '${m.id}', '${m.name}')">💰 Donate</button>

<button class="donate-btn" onclick="showDonateForm('maktab', '${m.id}', '${m.name}')">💰 Donate</button>

function showDonateForm(type, id, name) {
  const amount = prompt(`Donate to ${name}\nEnter amount (BDT):`);
  if (!amount) return;
  
  const donorName = prompt("Your name (leave blank for Anonymous):") || "Anonymous";
  const note = prompt("Note (optional):") || "";

  submitDonation(type, id, donorName, Number(amount), note);
}

async function submitDonation(type, id, donorName, amount, note) {
  if (!amount || amount <= 0) { alert("Please enter a valid amount!"); return; }

  const url = type === "mosque"
    ? `${API}/mosques/${id}/funding`
    : `${API}/maktabs/${id}/funding`;

  try {
    const res = await fetch(url, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ donorName, amount, note }),
    });
    const data = await res.json();

    if (data.success) {
      alert(`JazakAllah Khair! Your donation of ${amount} BDT has been recorded.`);
    } else {
      alert(data.message);
    }
  } catch (err) {
    alert("Failed to submit donation.");
  }
}
