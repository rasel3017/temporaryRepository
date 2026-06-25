const API = "http://localhost:3000/api";
let token = localStorage.getItem("token") || null;

// ===== DARK MODE =====
function toggleDark() {
  document.body.classList.toggle("dark");
  const btn = document.querySelector(".dark-toggle");
  btn.textContent = document.body.classList.contains("dark") ? "☀️ Light" : "🌙 Dark";
}

// ===== NAVIGATION =====
function showSection(id) {
  document.querySelectorAll(".section").forEach(s => s.classList.remove("active"));
  document.querySelectorAll(".nav-link").forEach(a => a.classList.remove("active"));
  document.getElementById(id).classList.add("active");
  const link = document.querySelector(`[onclick="showSection('${id}')"]`);
  if (link) link.classList.add("active");
}

// ===== AUTH =====
async function login() {
  const email = document.getElementById("loginEmail").value;
  const password = document.getElementById("loginPassword").value;

  const res = await fetch(`${API}/auth/login`, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ email, password }),
  });

  const data = await res.json();

  if (data.success) {
    token = data.token;
    localStorage.setItem("token", token);
    localStorage.setItem("user", JSON.stringify(data.data));
    updateAuthUI();
    showSection("home");
    alert(`Welcome ${data.data.name}!`);
  } else {
    alert(data.message);
  }
}

async function register() {
  const name = document.getElementById("registerName").value;
  const email = document.getElementById("registerEmail").value;
  const password = document.getElementById("registerPassword").value;

  const res = await fetch(`${API}/auth/register`, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ name, email, password }),
  });

  const data = await res.json();

  if (data.success) {
    token = data.token;
    localStorage.setItem("token", token);
    localStorage.setItem("user", JSON.stringify(data.data));
    updateAuthUI();
    showSection("home");
    alert(`Welcome ${data.data.name}!`);
  } else {
    alert(data.message);
  }
}

function logout() {
  token = null;
  localStorage.removeItem("token");
  localStorage.removeItem("user");
  updateAuthUI();
  showSection("home");
}

function updateAuthUI() {
  const user = JSON.parse(localStorage.getItem("user"));
  const authButtons = document.querySelector(".auth-buttons");

  if (user) {
    authButtons.innerHTML = `
      <span style="color:white; margin-right:10px;">👤 ${user.name}</span>
      <button class="btn-login" onclick="logout()">Logout</button>
      <button class="dark-toggle" onclick="toggleDark()">🌙 Dark</button>
    `;
  } else {
    authButtons.innerHTML = `
      <button class="btn-login" onclick="showSection('login')">Login</button>
      <button class="dark-toggle" onclick="toggleDark()">🌙 Dark</button>
    `;
  }
}

// ===== MOSQUES =====
async function searchByRegion() {
  const region = document.getElementById("regionInput").value;
  if (!region) { alert("Please enter a region!"); return; }

  const res = await fetch(`${API}/mosques/region/${region}`);
  const data = await res.json();
  const div = document.getElementById("mosqueResults");

  if (data.count === 0) {
    div.innerHTML = "<p>No mosques found in this region.</p>";
    return;
  }

  div.innerHTML = data.data.map(m => `
    <div class="card">
      <h3>${m.name}</h3>
      <p>📍 ${m.address}</p>
      <p>🗺️ Region: ${m.region}</p>
      ${m.latitude ? `<p>📌 ${m.latitude}, ${m.longitude}</p>` : ""}
      <span class="card-badge">Mosque</span>
    </div>
  `).join("");
}

async function searchByName() {
  const name = document.getElementById("searchNameInput").value;
  if (!name) { alert("Please enter a name!"); return; }

  const res = await fetch(`${API}/mosques/search/${name}`);
  const data = await res.json();
  const div = document.getElementById("mosqueResults");

  if (data.count === 0) {
    div.innerHTML = "<p>No mosques found.</p>";
    return;
  }

  div.innerHTML = data.data.map(m => `
    <div class="card">
      <h3>${m.name}</h3>
      <p>📍 ${m.address}</p>
      <p>🗺️ Region: ${m.region}</p>
      <span class="card-badge">Mosque</span>
    </div>
  `).join("");
}

// ===== MAKTAB =====
async function getMaktabs() {
  const mosqueId = document.getElementById("mosqueIdInput").value;
  if (!mosqueId) { alert("Please enter a Mosque ID!"); return; }

  const res = await fetch(`${API}/maktabs/mosque/${mosqueId}`);
  const data = await res.json();
  const div = document.getElementById("maktabResults");

  if (data.count === 0) {
    div.innerHTML = "<p>No Maktabs found for this mosque.</p>";
    return;
  }

  div.innerHTML = data.data.map(m => `
    <div class="card">
      <h3>${m.name}</h3>
      <p>👨‍🏫 Teacher: ${m.teacherName}</p>
      <p>📞 ${m.teacherPhone}</p>
      <p>🪑 Total Seats: ${m.totalSeats}</p>
      <span class="card-badge">Maktab</span>
    </div>
  `).join("");
}

// ===== EVENTS =====
async function getEvents() {
  const region = document.getElementById("eventRegionInput").value;
  if (!region) { alert("Please enter a region!"); return; }

  const res = await fetch(`${API}/events/region/${region}`);
  const data = await res.json();
  const div = document.getElementById("eventResults");

  if (data.count === 0) {
    div.innerHTML = "<p>No events found in this region.</p>";
    return;
  }

  div.innerHTML = data.data.map(e => `
    <div class="card">
      <h3>${e.title}</h3>
      <p>📖 Topic: ${e.topic}</p>
      <p>🎤 Speaker: ${e.speaker}</p>
      <p>📅 Date: ${new Date(e.eventDate).toLocaleDateString()}</p>
      <p>⏰ Time: ${e.eventTime}</p>
      <p>🕌 Mosque: ${e.mosque?.name}</p>
      <span class="card-badge">${e.status}</span>
    </div>
  `).join("");
}

// ===== Q&A =====
async function getAllQuestions() {
  const res = await fetch(`${API}/qa/questions`);
  const data = await res.json();
  const div = document.getElementById("qaResults");

  if (data.count === 0) {
    div.innerHTML = "<p>No questions yet.</p>";
    return;
  }

  div.innerHTML = data.data.map(q => `
    <div class="card">
      <h3>${q.title}</h3>
      <p>${q.body}</p>
      <p>📂 Category: ${q.category}</p>
      <p>👤 Asked by: ${q.user?.name}</p>
      <p>💬 Answers: ${q.answers?.length || 0}</p>
      <span class="card-badge">${q.status}</span>
    </div>
  `).join("");
}

// ===== INIT =====
updateAuthUI();

<button class="dark-toggle" onclick="toggleDark()">🌙 Dark</button>
