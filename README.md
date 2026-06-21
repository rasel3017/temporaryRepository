<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Smart Mosque Management System</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>

  <!-- HEADER -->
  <header>
    <div class="logo">
      <span class="logo-icon">🕌</span>
      <span class="logo-text">Smart Mosque</span>
    </div>
    <nav>
      <a href="#home" class="nav-link active" onclick="showSection('home')">Home</a>
      <a href="#" class="nav-link" onclick="showSection('mosques')">Mosques</a>
      <a href="#" class="nav-link" onclick="showSection('maktab')">Maktab</a>
      <a href="#" class="nav-link" onclick="showSection('events')">Events</a>
      <a href="#" class="nav-link" onclick="showSection('qa')">Q&A</a>
      <a href="#" class="nav-link" onclick="showSection('about')">About</a>
    </nav>
    <div class="auth-buttons">
      <button class="btn-login" onclick="showSection('login')">Login</button>
    </div>
  </header>

  <!-- MAIN -->
  <main>

    <!-- HOME SECTION -->
    <section id="home" class="section active">
      <div class="hero">
        <h1>Welcome to Smart Mosque Management System</h1>
        <p>Find mosques, explore Maktabs, discover Islamic events and get answers to your questions.</p>
        <button class="btn-primary" onclick="showSection('mosques')">Find a Mosque</button>
        <button class="btn-secondary" onclick="showSection('events')">View Events</button>
      </div>
      <div class="features">
        <div class="feature-card">
          <span>🕌</span>
          <h3>Mosque Finder</h3>
          <p>Find mosques in your region with detailed information.</p>
        </div>
        <div class="feature-card">
          <span>📚</span>
          <h3>Maktab Management</h3>
          <p>Explore Islamic schools and enroll your children.</p>
        </div>
        <div class="feature-card">
          <span>📅</span>
          <h3>Events & Mahfil</h3>
          <p>Discover upcoming Islamic events near you.</p>
        </div>
        <div class="feature-card">
          <span>❓</span>
          <h3>Q&A System</h3>
          <p>Ask Islamic questions and get answers from the community.</p>
        </div>
      </div>
    </section>

    <!-- MOSQUES SECTION -->
    <section id="mosques" class="section">
      <h2>🕌 Find a Mosque</h2>
      <div class="search-box">
        <input type="text" id="regionInput" placeholder="Enter region (e.g. Dhaka)">
        <button onclick="searchByRegion()">Search</button>
      </div>
      <div class="search-box" style="margin-top: 10px;">
        <input type="text" id="searchNameInput" placeholder="Search by name (e.g. Baitul)">
        <button onclick="searchByName()">Search</button>
      </div>
      <div id="mosqueResults" class="results"></div>
    </section>

    <!-- MAKTAB SECTION -->
    <section id="maktab" class="section">
      <h2>📚 Maktab</h2>
      <div class="search-box">
        <input type="text" id="mosqueIdInput" placeholder="Enter Mosque ID to find Maktabs">
        <button onclick="getMaktabs()">Find Maktabs</button>
      </div>
      <div id="maktabResults" class="results"></div>
    </section>

    <!-- EVENTS SECTION -->
    <section id="events" class="section">
      <h2>📅 Islamic Events & Mahfil</h2>
      <div class="search-box">
        <input type="text" id="eventRegionInput" placeholder="Enter region (e.g. Dhaka)">
        <button onclick="getEvents()">Find Events</button>
      </div>
      <div id="eventResults" class="results"></div>
    </section>

    <!-- Q&A SECTION -->
    <section id="qa" class="section">
      <h2>❓ Questions & Answers</h2>
      <button class="btn-primary" onclick="getAllQuestions()">Load All Questions</button>
      <div id="qaResults" class="results"></div>
    </section>

    <!-- ABOUT SECTION -->
    <section id="about" class="section">
      <h2>About This Project</h2>
      <div class="about-content">
        <p>The <strong>Smart Mosque Management System</strong> is a DBMS course project built to help manage mosque-related activities in Bangladesh.</p>
        <br>
        <h3>Features</h3>
        <ul>
          <li>🕌 Mosque Route & Recommendation</li>
          <li>📚 Maktab Management</li>
          <li>📅 Mahfil Event Locator</li>
          <li>❓ Question & Answer System</li>
        </ul>
        <br>
        <h3>Technologies Used</h3>
        <ul>
          <li>Node.js & Express.js</li>
          <li>PostgreSQL & Prisma ORM</li>
          <li>HTML, CSS, JavaScript</li>
          <li>JWT Authentication</li>
        </ul>
        <br>
        <p><strong>Course:</strong> Database Management System (CSE-2423)</p>
      </div>
    </section>

    <!-- LOGIN SECTION -->
    <section id="login" class="section">
      <h2>Login</h2>
      <div class="form-container">
        <div class="form-group">
          <label>Email</label>
          <input type="email" id="loginEmail" placeholder="Enter your email">
        </div>
        <div class="form-group">
          <label>Password</label>
          <input type="password" id="loginPassword" placeholder="Enter your password">
        </div>
        <button class="btn-primary" onclick="login()">Login</button>
        <p style="margin-top: 15px;">Don't have an account? <a href="#" onclick="showSection('register')">Register</a></p>
      </div>
    </section>

    <!-- REGISTER SECTION -->
    <section id="register" class="section">
      <h2>Register</h2>
      <div class="form-container">
        <div class="form-group">
          <label>Name</label>
          <input type="text" id="registerName" placeholder="Enter your name">
        </div>
        <div class="form-group">
          <label>Email</label>
          <input type="email" id="registerEmail" placeholder="Enter your email">
        </div>
        <div class="form-group">
          <label>Password</label>
          <input type="password" id="registerPassword" placeholder="Enter your password">
        </div>
        <button class="btn-primary" onclick="register()">Register</button>
        <p style="margin-top: 15px;">Already have an account? <a href="#" onclick="showSection('login')">Login</a></p>
      </div>
    </section>

  </main>

  <!-- FOOTER -->
  <footer>
    <div class="footer-content">
      <div class="footer-section">
        <h3>🕌 Smart Mosque</h3>
        <p>A complete mosque management system for Bangladesh.</p>
      </div>
      <div class="footer-section">
        <h3>Quick Links</h3>
        <a href="#" onclick="showSection('mosques')">Mosques</a>
        <a href="#" onclick="showSection('events')">Events</a>
        <a href="#" onclick="showSection('qa')">Q&A</a>
        <a href="#" onclick="showSection('about')">About</a>
      </div>
      <div class="footer-section">
        <h3>Course Info</h3>
        <p>Database Management System</p>
        <p>Course Code: CSE-2423</p>
      </div>
    </div>
    <div class="footer-bottom">
      <p>© 2026 Smart Mosque Management System. All rights reserved.</p>
    </div>
  </footer>

  <script src="js/main.js"></script>
</body>
</html>
