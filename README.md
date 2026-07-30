async function loadHomeStats() {
  try {
    const [mosquesRes, eventsRes, questionsRes] = await Promise.all([
      fetch(`${API}/mosques/all`),
      fetch(`${API}/events`),
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
