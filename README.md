async function showEventDetails(eventId) {
  showSection("events");
  const div = document.getElementById("eventResults");
  div.innerHTML = "<p>Loading...</p>";

  try {
    const res = await fetch(`${API}/events/${eventId}`);
    const data = await res.json();
    displayEvents([data.data], div);
  } catch (err) {
    div.innerHTML = "<p>Could not load event.</p>";
  }
}
