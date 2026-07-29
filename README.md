async function loadAllEvents() {
  const div = document.getElementById("eventResults");
  div.innerHTML = "<p>Loading events...</p>";

  try {
    const res = await fetch(`${API}/events`);
    const data = await res.json();
    displayEvents(data.data, div);
  } catch (err) {
    div.innerHTML = "<p>Could not load events.</p>";
  }
}
