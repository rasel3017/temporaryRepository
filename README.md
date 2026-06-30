function renderQuestions() {
  const div = document.getElementById("qaResults");
  const toShow = allQuestionsData.slice(0, questionsShown);

  div.innerHTML = toShow.map(q => {
    const answers = q.answers || [];
    const visibleAnswers = answers.slice(0, 2);
    const hasMore = answers.length > 2;

    return `
    <div class="card qa-card">
      <h3>❓ ${q.title}</h3>
      <p>${q.body}</p>
      <p>📂 Category: ${q.category}</p>
      <p>👤 Asked by: ${q.user?.name}</p>
      <p>💬 ${answers.length} Answer(s)</p>
      <span class="card-badge">${q.status}</span>
      ${answers.length > 0 ? `
        <div class="answers" id="answers-${q.id}">
          <h4>Answers:</h4>
          ${visibleAnswers.map(a => `
            <div class="answer-item">
              <p>${a.body}</p>
              ${a.isAccepted ? '<span class="card-badge accepted">✅ Best Answer</span>' : ""}
            </div>
          `).join("")}
        </div>
        ${hasMore ? `<button class="view-all-btn" onclick="viewAllAnswers('${q.id}')">View All ${answers.length} Answers</button>` : ""}
      ` : ""}
      <div class="answer-form">
        <input type="text" id="answer-${q.id}" placeholder="Write your answer...">
        <button onclick="postAnswer('${q.id}')">Reply</button>
      </div>
    </div>
  `}).join("");

  if (questionsShown < allQuestionsData.length) {
    div.innerHTML += `<button class="btn-primary" onclick="loadMoreQuestions()">Load More Questions</button>`;
  }
}

function viewAllAnswers(questionId) {
  const question = allQuestionsData.find(q => q.id === questionId);
  const answersDiv = document.getElementById(`answers-${questionId}`);

  answersDiv.innerHTML = `
    <h4>All Answers:</h4>
    ${question.answers.map(a => `
      <div class="answer-item">
        <p>${a.body}</p>
        ${a.isAccepted ? '<span class="card-badge accepted">✅ Best Answer</span>' : ""}
      </div>
    `).join("")}
  `;
}
