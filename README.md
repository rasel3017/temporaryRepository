function showAdminTab(tabId, btn) {
  document.querySelectorAll(".admin-tab-content").forEach(t => t.classList.remove("active"));
  document.querySelectorAll(".admin-tab").forEach(t => t.classList.remove("active"));
  document.getElementById(tabId).classList.add("active");
  btn.classList.add("active");
}
