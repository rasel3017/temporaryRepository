const API = "http://localhost:3000/api";
let token = localStorage.getItem("token") || null;

// ===== DARK MODE =====
function toggleDark() {
  document.body.classList.toggle("dark");
  const btn = document.querySelector(".dark-toggle");
  btn.textContent = document.body.classList.contains("dark") ? "☀️ Light" : "🌙 Dark";
  localStorage.setItem("darkMode", document.body.classList.contains("dark"));
}

// Load dark mode preference
if (localStorage.getItem("darkMode") === "true") {
  document.body.classList.add("dark");
}

// ===== NAVIGATION =====
function showSection(id) {
  document.querySelectorAll(".section").forEach(s => s.classList.remove("active"));
  document.querySelectorAll(".nav-link").forEach(a => a.classList.remove("active"));
  document.getElementById(id).classList.add("active");
  const link = document.querySelector(`[onclick="showSection('${id}')"]`);
  if (link) link.classList.add("active");
  window.scrollTo(0, 0);

  // Auto load content when section opens
  if (id === "mosques") loadAllMosques();
  if (id === "maktab") loadAllMaktabs();
  if (id === "events") loadAllEvents();
  if (id === "qa") getAllQuestions();
  if (id === "prayer") loadPrayerTimes();
  if (id === "ramadan") loadRamadanSchedule();
}

// ===== AUTH =====
async function login() {
  const email = document.getElementById("loginEmail").value;
  const password = document.getElementById("loginPassword").value;

  if (!email || !password) { alert("Please enter email and password!"); return; }

  try {
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
      alert(`Welcome back ${data.data.name}!`);
    } else {
      alert(data.message);
    }
  } catch (err) {
    alert("Login failed. Please try again.");
  }
}

async function register() {
  const name = document.getElementById("registerName").value;
  const email = document.getElementById("registerEmail").value;
  const password = document.getElementById("registerPassword").value;

  if (!name || !email || !password) { alert("Please fill all fields!"); return; }

  try {
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
  } catch (err) {
    alert("Registration failed. Please try again.");
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
      <span class="user-greeting">👤 ${user.name}</span>
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

// ===== HOME =====
async function loadHomeStats() {
  try {
    const [mosquesRes, eventsRes, questionsRes] = await Promise.all([
      fetch(`${API}/mosques/region/Dhaka`),
      fetch(`${API}/events/region/Dhaka`),
      fetch(`${API}/qa/questions`)
    ]);

    const mosques = await mosquesRes.json();
    const events = await eventsRes.json();
    const questions = await questionsRes.json();

    document.getElementById("totalMosques").textContent = mosques.count || 0;
    document.getElementById("totalEvents").textContent = events.count || 0;
    document.getElementById("totalQuestions").textContent = questions.count || 0;
  } catch (err) {
    console.error("Stats load failed:", err);
  }
}

async function loadHomeAnnouncements() {
  try {
    const res = await fetch(`${API}/events/upcoming`);
    const data = await res.json();
    const div = document.getElementById("homeEvents");

    if (!data.data || data.data.length === 0) {
      div.innerHTML = "<p>No upcoming events.</p>";
      return;
    }

    div.innerHTML = data.data.slice(0, 3).map(e => `
      <div class="event-announcement-card">
        ${e.imageUrl ? `<img src="${e.imageUrl}" alt="${e.title}">` : `<div class="no-image">📅</div>`}
        <div class="event-announcement-body">
          <h3>${e.title}</h3>
          <p>🎤 ${e.speaker}</p>
          <p>📅 ${new Date(e.eventDate).toLocaleDateString('en-BD')}</p>
          <p>⏰ ${e.eventTime}</p>
          ${e.location ? `<p>📍 ${e.location}</p>` : ""}
          <span class="card-badge ${e.isFree ? 'free' : 'paid'}">${e.isFree ? "Free Entry" : "Paid"}</span>
        </div>
      </div>
    `).join("");
  } catch (err) {
    document.getElementById("homeEvents").innerHTML = "<p>Could not load events.</p>";
  }
}

// ===== MOSQUES =====
async function loadAllMosques() {
  const div = document.getElementById("mosqueResults");
  div.innerHTML = "<p>Loading mosques...</p>";

  try {
    const res = await fetch(`${API}/mosques/region/Dhaka`);
    const data = await res.json();
    displayMosques(data.data, div);
  } catch (err) {
    div.innerHTML = "<p>Could not load mosques.</p>";
  }
}

async function searchByRegion() {
  const region = document.getElementById("regionInput").value;
  if (!region) { alert("Please enter a region!"); return; }

  const div = document.getElementById("mosqueResults");
  div.innerHTML = "<p>Searching...</p>";

  try {
    const res = await fetch(`${API}/mosques/region/${region}`);
    const data = await res.json();
    displayMosques(data.data, div);
  } catch (err) {
    div.innerHTML = "<p>Search failed.</p>";
  }
}

async function searchByName() {
  const name = document.getElementById("searchNameInput").value;
  if (!name) { alert("Please enter a name!"); return; }

  const div = document.getElementById("mosqueResults");
  div.innerHTML = "<p>Searching...</p>";

  try {
    const res = await fetch(`${API}/mosques/search/${name}`);
    const data = await res.json();
    displayMosques(data.data, div);
  } catch (err) {
    div.innerHTML = "<p>Search failed.</p>";
  }
}

function displayMosques(mosques, div) {
  if (!mosques || mosques.length === 0) {
    div.innerHTML = "<p>No mosques found.</p>";
    return;
  }

  div.innerHTML = mosques.map(m => `
    <div class="card mosque-card">
      ${m.imageUrl ? `<img src="${m.imageUrl}" alt="${m.name}" class="card-image">` : ""}
      <div class="card-body">
        <h3>🕌 ${m.name}</h3>
        <p>📍 ${m.address}</p>
        <p>🗺️ Region: ${m.region}</p>
        ${m.imamName ? `<p>👳 Imam: ${m.imamName}</p>` : ""}
        ${m.muazzinName ? `<p>🔊 Muazzin: ${m.muazzinName}</p>` : ""}
        ${m.fajrTime ? `
          <div class="prayer-mini">
            <span>Fajr: ${m.fajrTime}</span>
            <span>Zuhr: ${m.zuhrTime}</span>
            <span>Asr: ${m.asrTime}</span>
            <span>Maghrib: ${m.maghribTime}</span>
            <span>Isha: ${m.ishaTime}</span>
          </div>
        ` : ""}
        ${m.latitude ? `
          <a href="https://maps.google.com/?q=${m.latitude},${m.longitude}" 
             target="_blank" class="map-btn">🗺️ View on Google Maps</a>
        ` : ""}
      </div>
    </div>
  `).join("");
}

// ===== MAKTAB =====
async function loadAllMaktabs() {
  const div = document.getElementById("maktabResults");
  div.innerHTML = "<p>Loading Maktabs...</p>";

  try {
    const res = await fetch(`${API}/maktabs`);
    const data = await res.json();
    displayMaktabs(data.data, div);
  } catch (err) {
    div.innerHTML = "<p>Could not load Maktabs.</p>";
  }
}

async function getMaktabs() {
  const mosqueId = document.getElementById("mosqueIdInput").value;
  if (!mosqueId) { alert("Please enter a Mosque ID!"); return; }

  const div = document.getElementById("maktabResults");
  div.innerHTML = "<p>Searching...</p>";

  try {
    const res = await fetch(`${API}/maktabs/mosque/${mosqueId}`);
    const data = await res.json();
    displayMaktabs(data.data, div);
  } catch (err) {
    div.innerHTML = "<p>Search failed.</p>";
  }
}

function displayMaktabs(maktabs, div) {
  if (!maktabs || maktabs.length === 0) {
    div.innerHTML = "<p>No Maktabs found.</p>";
    return;
  }

  div.innerHTML = maktabs.map(m => `
    <div class="card">
      ${m.imageUrl ? `<img src="${m.imageUrl}" alt="${m.name}" class="card-image">` : ""}
      <div class="card-body">
        <h3>📚 ${m.name}</h3>
        ${m.address ? `<p>📍 ${m.address}</p>` : ""}
        <p>👨‍🏫 Ustad: ${m.teacherName}</p>
        <p>📞 ${m.teacherPhone}</p>
        <p>🪑 Total Seats: ${m.totalSeats}</p>
        ${m.coursesOffered ? `<p>📖 Courses: ${m.coursesOffered}</p>` : ""}
        ${m.mosque ? `<p>🕌 Mosque: ${m.mosque.name}</p>` : `<span class="card-badge">Independent</span>`}
      </div>
    </div>
  `).join("");
}

// ===== EVENTS =====
async function loadAllEvents() {
  const div = document.getElementById("eventResults");
  div.innerHTML = "<p>Loading events...</p>";

  try {
    const res = await fetch(`${API}/events/region/Dhaka`);
    const data = await res.json();
    displayEvents(data.data, div);
  } catch (err) {
    div.innerHTML = "<p>Could not load events.</p>";
  }
}

async function getEvents() {
  const region = document.getElementById("eventRegionInput").value;
  if (!region) { alert("Please enter a region!"); return; }

  const div = document.getElementById("eventResults");
  div.innerHTML = "<p>Searching...</p>";

  try {
    const res = await fetch(`${API}/events/region/${region}`);
    const data = await res.json();
    displayEvents(data.data, div);
  } catch (err) {
    div.innerHTML = "<p>Search failed.</p>";
  }
}

function displayEvents(events, div) {
  if (!events || events.length === 0) {
    div.innerHTML = "<p>No events found.</p>";
    return;
  }

  div.innerHTML = events.map(e => `
    <div class="card event-card">
      ${e.imageUrl ? `<img src="${e.imageUrl}" alt="${e.title}" class="card-image">` : ""}
      <div class="card-body">
        <h3>📅 ${e.title}</h3>
        <p>📖 Topic: ${e.topic}</p>
        <p>🎤 Speaker: ${e.speaker}</p>
        <p>📅 Date: ${new Date(e.eventDate).toLocaleDateString('en-BD')}</p>
        <p>⏰ Time: ${e.eventTime}</p>
        ${e.location ? `<p>📍 Location: ${e.location}</p>` : ""}
        ${e.description ? `<p>ℹ️ ${e.description}</p>` : ""}
        ${e.mosque ? `<p>🕌 Mosque: ${e.mosque.name}</p>` : ""}
        <span class="card-badge ${e.isFree ? 'free' : 'paid'}">${e.isFree ? "Free Entry" : "Paid Entry"}</span>
        <span class="card-badge">${e.status}</span>
      </div>
    </div>
  `).join("");
}

// ===== Q&A =====
async function getAllQuestions() {
  const div = document.getElementById("qaResults");
  div.innerHTML = "<p>Loading questions...</p>";

  try {
    const res = await fetch(`${API}/qa/questions`);
    const data = await res.json();

    if (data.count === 0) {
      div.innerHTML = "<p>No questions yet. Be the first to ask!</p>";
      return;
    }

    div.innerHTML = data.data.map(q => `
      <div class="card qa-card">
        <h3>❓ ${q.title}</h3>
        <p>${q.body}</p>
        <p>📂 Category: ${q.category}</p>
        <p>👤 Asked by: ${q.user?.name}</p>
        <p>💬 ${q.answers?.length || 0} Answer(s)</p>
        <span class="card-badge">${q.status}</span>
        ${q.answers && q.answers.length > 0 ? `
          <div class="answers">
            <h4>Answers:</h4>
            ${q.answers.map(a => `
              <div class="answer-item">
                <p>${a.body}</p>
                ${a.isAccepted ? '<span class="card-badge accepted">✅ Best Answer</span>' : ""}
              </div>
            `).join("")}
          </div>
        ` : ""}
      </div>
    `).join("");
  } catch (err) {
    div.innerHTML = "<p>Could not load questions.</p>";
  }
}

// ===== PRAYER TIMES =====
async function loadPrayerTimes() {
  const city = document.getElementById("prayerCity")?.value || "Dhaka";
  fetchPrayerTimes(city);
}

async function fetchPrayerTimes(city) {
  const div = document.getElementById("prayerResults");
  div.innerHTML = "<p>Loading prayer times...</p>";

  try {
    const res = await fetch(`https://api.aladhan.com/v1/timingsByCity?city=${city}&country=Bangladesh&method=1`);
    const data = await res.json();

    if (data.code !== 200) {
      div.innerHTML = "<p>Could not load prayer times.</p>";
      return;
    }

    const t = data.data.timings;
    const date = data.data.date.readable;

    div.innerHTML = `
      <div class="prayer-card">
        <h3>🕌 Prayer Times for ${city}</h3>
        <p>📅 ${date}</p>
        <div class="prayer-times-grid">
          <div class="prayer-time-item fajr">
            <span class="prayer-name">Fajr</span>
            <span class="prayer-time">${t.Fajr}</span>
          </div>
          <div class="prayer-time-item">
            <span class="prayer-name">Sunrise</span>
            <span class="prayer-time">${t.Sunrise}</span>
          </div>
          <div class="prayer-time-item zuhr">
            <span class="prayer-name">Zuhr</span>
            <span class="prayer-time">${t.Dhuhr}</span>
          </div>
          <div class="prayer-time-item asr">
            <span class="prayer-name">Asr</span>
            <span class="prayer-time">${t.Asr}</span>
          </div>
          <div class="prayer-time-item maghrib">
            <span class="prayer-name">Maghrib</span>
            <span class="prayer-time">${t.Maghrib}</span>
          </div>
          <div class="prayer-time-item isha">
            <span class="prayer-name">Isha</span>
            <span class="prayer-time">${t.Isha}</span>
          </div>
        </div>
      </div>
    `;
  } catch (err) {
    div.innerHTML = "<p>Could not load prayer times. Check your internet connection.</p>";
  }
}

// ===== RAMADAN SCHEDULE =====
async function loadRamadanSchedule() {
  const city = document.getElementById("ramadanCity")?.value || "Dhaka";
  fetchRamadanSchedule(city);
}

async function fetchRamadanSchedule(city) {
  const div = document.getElementById("ramadanResults");
  div.innerHTML = "<p>Loading Ramadan schedule...</p>";

  try {
    // Ramadan 2027 - month 9, year 2027
    const res = await fetch(`https://api.aladhan.com/v1/calendarByCity?city=${city}&country=Bangladesh&method=1&month=3&year=2027`);
    const data = await res.json();

    if (data.code !== 200) {
      div.innerHTML = "<p>Could not load Ramadan schedule.</p>";
      return;
    }

    div.innerHTML = `
      <div class="ramadan-header">
        <h3>🌙 Ramadan 2027 Schedule — ${city}</h3>
        <p>Sehri ends at Fajr time | Iftar at Maghrib time</p>
      </div>
      <div class="ramadan-table">
        <div class="ramadan-row header">
          <span>Date</span>
          <span>Sehri (Fajr)</span>
          <span>Iftar (Maghrib)</span>
        </div>
        ${data.data.map((day, i) => `
          <div class="ramadan-row ${i % 2 === 0 ? 'even' : ''}">
            <span>${i + 1} Ramadan | ${day.date.readable}</span>
            <span>🌙 ${day.timings.Fajr}</span>
            <span>🌅 ${day.timings.Maghrib}</span>
          </div>
        `).join("")}
      </div>
    `;
  } catch (err) {
    div.innerHTML = "<p>Could not load Ramadan schedule. Check your internet connection.</p>";
  }
}

// ===== INIT =====
updateAuthUI();
loadHomeStats();
loadHomeAnnouncements();
getAllQuestions();
