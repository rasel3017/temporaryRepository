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
        <div class="answer-form">
          <input type="text" id="answer-${q.id}" placeholder="Write your answer...">
          <button onclick="postAnswer('${q.id}')">Reply</button>
        </div>
      </div>
    `).join("");
  } catch (err) {
    div.innerHTML = "<p>Could not load questions.</p>";
  }
}

async function postAnswer(questionId) {
  if (!token) { alert("Please login to answer!"); showSection("login"); return; }

  const body = document.getElementById(`answer-${questionId}`).value;
  if (!body) { alert("Please write an answer!"); return; }

  try {
    const res = await fetch(`${API}/qa/questions/${questionId}/answers`, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        "Authorization": `Bearer ${token}`
      },
      body: JSON.stringify({ body }),
    });
    const data = await res.json();

    if (data.success) {
      alert("Answer posted!");
      getAllQuestions();
    } else {
      alert(data.message);
    }
  } catch (err) {
    alert("Failed to post answer.");
  }
}
