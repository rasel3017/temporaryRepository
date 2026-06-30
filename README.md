function updateAuthUI() {
  const user = JSON.parse(localStorage.getItem("user"));
  const authButtons = document.querySelector(".auth-buttons");

  if (user) {
    authButtons.innerHTML = `
      ${user.role === "admin" ? `<a href="#" class="nav-link" onclick="showSection('admin')">⚙️ Admin</a>` : ""}
      <a href="#" class="nav-link" onclick="showSection('profile'); loadProfile();">👤 ${user.name}</a>
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
