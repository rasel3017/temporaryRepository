<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Smart Mosque Management System</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>

  <header>
    <h1>🕌 Smart Mosque Management System</h1>
    <nav>
      <a href="#mosques">Mosques</a>
      <a href="#events">Events</a>
      <a href="#qa">Q&A</a>
      <a href="#login">Login</a>
    </nav>
  </header>

  <main>
    <section id="mosques">
      <h2>Find a Mosque</h2>
      <input type="text" id="regionInput" placeholder="Enter region (e.g. Dhaka)">
      <button onclick="searchByRegion()">Search</button>
      <div id="mosqueResults"></div>
    </section>
  </main>

  <script src="js/main.js"></script>
</body>
</html>
