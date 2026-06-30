// ===== ADMIN =====
function showAdminTab(tabId) {
  document.querySelectorAll(".admin-tab-content").forEach(t => t.classList.remove("active"));
  document.querySelectorAll(".admin-tab").forEach(t => t.classList.remove("active"));
  document.getElementById(tabId).classList.add("active");
  event.target.classList.add("active");
}

async function adminAddMosque() {
  const body = {
    name: document.getElementById("m_name").value,
    address: document.getElementById("m_address").value,
    region: document.getElementById("m_region").value,
    imamName: document.getElementById("m_imam").value,
    muazzinName: document.getElementById("m_muazzin").value,
    imageUrl: document.getElementById("m_image").value,
    latitude: parseFloat(document.getElementById("m_lat").value) || null,
    longitude: parseFloat(document.getElementById("m_lng").value) || null,
  };

  if (!body.name || !body.address || !body.region) { alert("Name, address and region are required!"); return; }

  try {
    const res = await fetch(`${API}/mosques`, {
      method: "POST",
      headers: { "Content-Type": "application/json", "Authorization": `Bearer ${token}` },
      body: JSON.stringify(body),
    });
    const data = await res.json();

    if (data.success) {
      alert("Mosque added successfully!");
      document.querySelectorAll("#addMosqueTab input").forEach(i => i.value = "");
    } else {
      alert(data.message);
    }
  } catch (err) {
    alert("Failed to add mosque.");
  }
}

async function adminAddMaktab() {
  const body = {
    name: document.getElementById("mk_name").value,
    address: document.getElementById("mk_address").value,
    teacherName: document.getElementById("mk_teacher").value,
    teacherPhone: document.getElementById("mk_phone").value,
    totalSeats: parseInt(document.getElementById("mk_seats").value),
    coursesOffered: document.getElementById("mk_courses").value,
    imageUrl: document.getElementById("mk_image").value,
    mosqueId: document.getElementById("mk_mosqueId").value || null,
  };

  if (!body.name || !body.teacherName || !body.teacherPhone || !body.totalSeats) { alert("Name, teacherName, phone and seats are required!"); return; }

  try {
    const res = await fetch(`${API}/maktabs`, {
      method: "POST",
      headers: { "Content-Type": "application/json", "Authorization": `Bearer ${token}` },
      body: JSON.stringify(body),
    });
    const data = await res.json();

    if (data.success) {
      alert("Maktab added successfully!");
      document.querySelectorAll("#addMaktabTab input").forEach(i => i.value = "");
    } else {
      alert(data.message);
    }
  } catch (err) {
    alert("Failed to add maktab.");
  }
}

async function adminAddEvent() {
  const body = {
    title: document.getElementById("e_title").value,
    topic: document.getElementById("e_topic").value,
    speaker: document.getElementById("e_speaker").value,
    eventDate: document.getElementById("e_date").value,
    eventTime: document.getElementById("e_time").value,
    location: document.getElementById("e_location").value,
    description: document.getElementById("e_description").value,
    imageUrl: document.getElementById("e_image").value,
    mosqueId: document.getElementById("e_mosqueId").value || null,
  };

  if (!body.title || !body.topic || !body.speaker || !body.eventDate || !body.eventTime) { alert("Title, topic, speaker, date and time are required!"); return; }

  try {
    const res = await fetch(`${API}/events`, {
      method: "POST",
      headers: { "Content-Type": "application/json", "Authorization": `Bearer ${token}` },
      body: JSON.stringify(body),
    });
    const data = await res.json();

    if (data.success) {
      alert("Event added successfully!");
      document.querySelectorAll("#addEventTab input").forEach(i => i.value = "");
    } else {
      alert(data.message);
    }
  } catch (err) {
    alert("Failed to add event.");
  }
}
