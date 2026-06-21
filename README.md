const API = "http://localhost:3000/api";

// Search mosques by region
async function searchByRegion() {
  const region = document.getElementById("regionInput").value;

  if (!region) {
    alert("Please enter a region!");
    return;
  }

  const response = await fetch(`${API}/mosques/region/${region}`);
  const data = await response.json();

  const resultsDiv = document.getElementById("mosqueResults");

  if (data.count === 0) {
    resultsDiv.innerHTML = "<p>No mosques found in this region.</p>";
    return;
  }

  resultsDiv.innerHTML = data.data.map(mosque => `
    <div class="mosque-card">
      <h3>${mosque.name}</h3>
      <p>${mosque.address}</p>
      <p>Region: ${mosque.region}</p>
    </div>
  `).join("");
}
