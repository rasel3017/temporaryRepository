${isAdmin() ? `<button class="delete-btn" onclick="deleteQuestion('${q.id}')">🗑️ Delete</button>` : ""}


function isAdmin() {
  const user = JSON.parse(localStorage.getItem("user"));
  return user && user.role === "admin";
}

async function deleteQuestion(questionId) {
  if (!confirm("Are you sure you want to delete this question?")) return;

  try {
    const res = await fetch(`${API}/qa/questions/${questionId}`, {
      method: "DELETE",
      headers: { "Authorization": `Bearer ${token}` }
    });
    const data = await res.json();

    if (data.success) {
      alert("Question deleted!");
      getAllQuestions();
    } else {
      alert(data.message);
    }
  } catch (err) {
    alert("Failed to delete question.");
  }
}
