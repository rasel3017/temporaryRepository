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
      <a href="#" class="nav-link active" onclick="showSection('home')">Home</a>
      <a href="#" class="nav-link" onclick="showSection('mosques')">Mosques</a>
      <a href="#" class="nav-link" onclick="showSection('maktab')">Maktab</a>
      <a href="#" class="nav-link" onclick="showSection('events')">Events</a>
      <a href="#" class="nav-link" onclick="showSection('qa')">Q&A</a>
      <a href="#" class="nav-link" onclick="showSection('about')">About</a>
    </nav>
    <div class="auth-buttons">
      <button class="dark-toggle" onclick="toggleDark()">🌙 Dark</button>
      <button class="btn-login" onclick="showSection('login')">Login</button>
    </div>
  </header>

  <!-- MAIN -->
  <main>

    <!-- HOME SECTION -->
    <section id="home" class="section active">

      <!-- HERO BANNER -->
      <div class="hero" style="background-image: url('images/mosque1.jpg')">
        <div class="hero-overlay">
          <h1>Welcome to Smart Mosque Management System</h1>
          <p>Find mosques, explore Maktabs, discover Islamic events and get answers to your questions.</p>
          <div class="hero-buttons">
            <button class="btn-primary" onclick="showSection('mosques')">🕌 Find a Mosque</button>
            <button class="btn-secondary" onclick="showSection('events')">📅 View Events</button>
          </div>
        </div>
      </div>

      <!-- STATS BAR -->
      <div class="stats-bar">
        <div class="stat-item">
          <span class="stat-number" id="totalMosques">...</span>
          <span class="stat-label">Mosques</span>
        </div>
        <div class="stat-item">
          <span class="stat-number" id="totalEvents">...</span>
          <span class="stat-label">Events</span>
        </div>
        <div class="stat-item">
          <span class="stat-number" id="totalQuestions">...</span>
          <span class="stat-label">Questions</span>
        </div>
        <div class="stat-item">
          <span class="stat-number">🇧🇩</span>
          <span class="stat-label">Bangladesh</span>
        </div>
      </div>

      <!-- ANNOUNCEMENTS -->
      <div class="home-section">
        <h2>📢 Upcoming Events & Mahfil</h2>
        <div id="homeEvents" class="grid-3">
          <p>Loading events...</p>
        </div>
      </div>

      <!-- IMAGE GALLERY -->
      <div class="home-section">
        <h2>📸 Islamic Events Gallery</h2>
        <div class="gallery">
          <img src="images/event1.jpg" alt="Islamic Event">
          <img src="images/event2.jpg" alt="Islamic Event">
          <img src="images/event3.jpg" alt="Islamic Event">
          <img src="images/event4.jpg" alt="Islamic Event">
        </div>
      </div>

      <!-- QURAN SECTION -->
      <div class="home-section quran-section" style="background-image: url('images/quran1.jpg')">
        <div class="quran-overlay">
          <h2>📖 Learn & Grow</h2>
          <p>Join Maktabs and courses to deepen your Islamic knowledge.</p>
          <button class="btn-primary" onclick="showSection('maktab')">Explore Maktabs</button>
        </div>
      </div>

      <!-- FEATURES -->
      <div class="home-section">
        <h2>🌟 What We Offer</h2>
        <div class="features">
          <div class="feature-card" onclick="showSection('mosques')">
            <span>🕌</span>
            <h3>Mosque Finder</h3>
            <p>Find mosques in your region with detailed information and location.</p>
          </div>
          <div class="feature-card" onclick="showSection('maktab')">
            <span>📚</span>
            <h3>Maktab Management</h3>
            <p>Explore Islamic schools, enroll your children and support with donations.</p>
          </div>
          <div class="feature-card" onclick="showSection('events')">
            <span>📅</span>
            <h3>Events & Mahfil</h3>
            <p>Discover upcoming Islamic events and Mahfil near you.</p>
          </div>
          <div class="feature-card" onclick="showSection('qa')">
            <span>❓</span>
            <h3>Q&A System</h3>
            <p>Ask Islamic questions and get answers from the community.</p>
          </div>
        </div>
      </div>

    </section>

    <!-- MOSQUES SECTION -->
    <section id="mosques" class="section">
      <div class="section-header" style="background-image: url('images/mosque2.jpg')">
        <div class="section-header-overlay">
          <h2>🕌 Find a Mosque</h2>
          <p>Search mosques across Bangladesh by region or name</p>
        </div>
      </div>
      <div class="section-body">
        <div class="search-row">
          <div class="search-box">
            <input type="text" id="regionInput" placeholder="Search by region (e.g. Dhaka)">
            <button onclick="searchByRegion()">Search</button>
          </div>
          <div class="search-box">
            <input type="text" id="searchNameInput" placeholder="Search by name (e.g. Baitul)">
            <button onclick="searchByName()">Search</button>
          </div>
        </div>
        <div id="mosqueResults" class="results"></div>
      </div>
    </section>

    <!-- MAKTAB SECTION -->
    <section id="maktab" class="section">
      <div class="section-header" style="background-image: url('images/quran2.jpg')">
        <div class="section-header-overlay">
          <h2>📚 Maktab</h2>
          <p>Islamic schools attached to mosques across Bangladesh</p>
        </div>
      </div>
      <div class="section-body">
        <div class="search-box">
          <input type="text" id="mosqueIdInput" placeholder="Enter Mosque ID to find Maktabs">
          <button onclick="getMaktabs()">Find Maktabs</button>
        </div>
        <div id="maktabResults" class="results"></div>
      </div>
    </section>

    <!-- EVENTS SECTION -->
    <section id="events" class="section">
      <div class="section-header" style="background-image: url('images/event1.jpg')">
        <div class="section-header-overlay">
          <h2>📅 Islamic Events & Mahfil</h2>
          <p>Discover upcoming Islamic events and Mahfil near you</p>
        </div>
      </div>
      <div class="section-body">
        <div class="search-box">
          <input type="text" id="eventRegionInput" placeholder="Enter region (e.g. Dhaka)">
          <button onclick="getEvents()">Find Events</button>
        </div>
        <div id="eventResults" class="results"></div>
      </div>
    </section>

    <!-- Q&A SECTION -->
    <section id="qa" class="section">
      <div class="section-header" style="background-image: url('images/quran3.jpg')">
        <div class="section-header-overlay">
          <h2>❓ Questions & Answers</h2>
          <p>Ask Islamic questions and get answers from the community</p>
        </div>
      </div>
      <div class="section-body">
        <button class="btn-primary" onclick="getAllQuestions()">Load All Questions</button>
        <div id="qaResults" class="results"></div>
      </div>
    </section>

    <!-- ABOUT SECTION -->
    <section id="about" class="section">
      <div class="section-header" style="background-image: url('images/mosque3.jpg')">
        <div class="section-header-overlay">
          <h2>About This Project</h2>
          <p>Smart Mosque Management System — CSE-2423</p>
        </div>
      </div>
      <div class="section-body">
        <div class="about-content">
          <p>The <strong>Smart Mosque Management System</strong> is a DBMS course project built to help manage mosque-related activities in Bangladesh.</p>
          <br>
          <h3>✅ Completed Features</h3>
          <ul>
            <li>🕌 Mosque Route & Recommendation</li>
            <li>📚 Maktab Management</li>
            <li>📅 Mahfil Event Locator</li>
            <li>❓ Question & Answer System</li>
            <li>🔐 User Authentication</li>
          </ul>
          <br>
          <h3>🔲 Planned Features</h3>
          <ul>
            <li>📖 Course / Learning Module</li>
            <li>🕐 Prayer Time Schedule</li>
            <li>🗺️ Google Maps Integration</li>
            <li>📊 Admin Dashboard</li>
          </ul>
          <br>
          <h3>🛠️ Technologies Used</h3>
          <ul>
            <li>Node.js & Express.js</li>
            <li>PostgreSQL & Prisma ORM v7</li>
            <li>HTML, CSS, JavaScript</li>
            <li>JWT Authentication</li>
          </ul>
          <br>
          <p><strong>Course:</strong> Database Management System (CSE-2423)</p>
        </div>
      </div>
    </section>

    <!-- LOGIN SECTION -->
    <section id="login" class="section">
      <div class="auth-container">
        <div class="auth-image" style="background-image: url('images/mosque4.jpg')"></div>
        <div class="auth-form">
          <h2>Login</h2>
          <div class="form-group">
            <label>Email</label>
            <input type="email" id="loginEmail" placeholder="Enter your email">
          </div>
          <div class="form-group">
            <label>Password</label>
            <input type="password" id="loginPassword" placeholder="Enter your password">
          </div>
          <button class="btn-primary btn-full" onclick="login()">Login</button>
          <p style="margin-top: 15px; text-align:center;">Don't have an account? <a href="#" onclick="showSection('register')">Register</a></p>
        </div>
      </div>
    </section>

    <!-- REGISTER SECTION -->
    <section id="register" class="section">
      <div class="auth-container">
        <div class="auth-image" style="background-image: url('images/mosque1.jpg')"></div>
        <div class="auth-form">
          <h2>Register</h2>
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
          <button class="btn-primary btn-full" onclick="register()">Register</button>
          <p style="margin-top: 15px; text-align:center;">Already have an account? <a href="#" onclick="showSection('login')">Login</a></p>
        </div>
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
