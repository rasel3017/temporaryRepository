async function searchMaktabByName() {
  const name = document.getElementById("maktabSearchInput").value;
  if (!name) { alert("Please enter a name!"); return; }

  const div = document.getElementById("maktabResults");
  div.innerHTML = "<p>Searching...</p>";

  try {
    const res = await fetch(`${API}/maktabs/search/${name}`);
    const data = await res.json();
    displayMaktabs(data.data, div);
  } catch (err) {
    div.innerHTML = "<p>Search failed.</p>";
  }
}
