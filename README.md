// ===== PROFILE =====
async function loadProfile() {
  const user = JSON.parse(localStorage.getItem("user"));
  if (!user) { showSection("login"); return; }

  document.getElementById("profileName").value = user.name;
  document.getElementById("profileEmail").value = user.email;
}

async function updateProfile() {
  const name = document.getElementById("profileName").value;
  const email = document.getElementById("profileEmail").value;
  const password = document.getElementById("profilePassword").value;

  const body = {};
  if (name) body.name = name;
  if (email) body.email = email;
  if (password) body.password = password;

  try {
    const res = await fetch(`${API}/auth/update-profile`, {
      method: "PUT",
      headers: {
        "Content-Type": "application/json",
        "Authorization": `Bearer ${token}`
      },
      body: JSON.stringify(body),
    });
    const data = await res.json();

    if (data.success) {
      localStorage.setItem("user", JSON.stringify(data.data));
      updateAuthUI();
      document.getElementById("profilePassword").value = "";
      alert("Profile updated successfully!");
    } else {
      alert(data.message);
    }
  } catch (err) {
    alert("Update failed. Please try again.");
  }
}
