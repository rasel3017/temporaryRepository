* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  background-color: #f5f5f5;
  color: #333;
}

header {
  background-color: #1a6b3c;
  color: white;
  padding: 15px 30px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

header h1 {
  font-size: 1.5rem;
}

nav a {
  color: white;
  text-decoration: none;
  margin-left: 20px;
  font-size: 1rem;
}

nav a:hover {
  text-decoration: underline;
}

main {
  max-width: 900px;
  margin: 30px auto;
  padding: 0 20px;
}

section {
  background: white;
  padding: 25px;
  border-radius: 8px;
  margin-bottom: 30px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

h2 {
  margin-bottom: 15px;
  color: #1a6b3c;
}

input[type="text"] {
  padding: 10px;
  width: 60%;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 1rem;
}

button {
  padding: 10px 20px;
  background-color: #1a6b3c;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
  margin-left: 10px;
}

button:hover {
  background-color: #145530;
}

.mosque-card {
  border: 1px solid #ddd;
  padding: 15px;
  border-radius: 6px;
  margin-top: 10px;
  background: #f9f9f9;
}

.mosque-card h3 {
  color: #1a6b3c;
  margin-bottom: 5px;
}
