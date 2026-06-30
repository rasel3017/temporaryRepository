async function postQuestion() {
  if (!token) { alert("Please login to ask a question!"); showSection("login"); return; }

  const title = document.getElementById("questionTitle").value;
  const body = document.getElementById("questionBody").value;
  const category = document.getElementById("questionCategory").value;

  if (!title || !body || !category) { alert("Please fill all fields!"); return; }

  try {
    const res = await fetch(`${API}/qa/questions`, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        "Authorization": `Bearer ${token}`
      },
      body: JSON.stringify({ title, body, category }),
    });
    const data = await res.json();

    if (data.success) {
      document.getElementById("questionTitle").value = "";
      document.getElementById("questionBody").value = "";
      document.getElementById("questionCategory").value = "";
      alert("Question posted successfully!");
      getAllQuestions();
    } else {
      alert(data.message);
    }
  } catch (err) {
    alert("Failed to post question.");
  }
}
