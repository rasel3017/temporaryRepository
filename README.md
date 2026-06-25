/* ===== CSS VARIABLES ===== */
:root {
  --primary: #1a6b3c;
  --primary-dark: #145530;
  --primary-light: #e8f5ee;
  --secondary: #f0a500;
  --bg: #f5f5f5;
  --card-bg: #ffffff;
  --text: #333333;
  --text-light: #666666;
  --border: #dddddd;
  --shadow: 0 2px 10px rgba(0,0,0,0.1);
  --header-height: 65px;
}

/* DARK MODE */
body.dark {
  --bg: #1a1a2e;
  --card-bg: #16213e;
  --text: #eaeaea;
  --text-light: #aaaaaa;
  --border: #333355;
  --shadow: 0 2px 10px rgba(0,0,0,0.4);
  --primary-light: #1a3a2a;
}

/* ===== RESET ===== */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Segoe UI', Arial, sans-serif;
  background-color: var(--bg);
  color: var(--text);
  transition: background 0.3s, color 0.3s;
}

/* ===== HEADER ===== */
header {
  background-color: var(--primary);
  color: white;
  padding: 0 30px;
  height: var(--header-height);
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: sticky;
  top: 0;
  z-index: 100;
  box-shadow: 0 2px 10px rgba(0,0,0,0.2);
}

.logo {
  display: flex;
  align-items: center;
  gap: 10px;
}

.logo-icon { font-size: 1.8rem; }

.logo-text {
  font-size: 1.2rem;
  font-weight: bold;
  color: white;
}

nav {
  display: flex;
  gap: 5px;
}

.nav-link {
  color: rgba(255,255,255,0.85);
  text-decoration: none;
  padding: 8px 14px;
  border-radius: 5px;
  font-size: 0.95rem;
  transition: all 0.2s;
}

.nav-link:hover,
.nav-link.active {
  background-color: rgba(255,255,255,0.2);
  color: white;
}

.auth-buttons {
  display: flex;
  align-items: center;
  gap: 10px;
}

.btn-login {
  background: white;
  color: var(--primary);
  border: none;
  padding: 8px 20px;
  border-radius: 5px;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.2s;
}

.btn-login:hover {
  background: var(--secondary);
  color: white;
}

.dark-toggle {
  background: none;
  border: 2px solid rgba(255,255,255,0.5);
  color: white;
  padding: 6px 12px;
  border-radius: 20px;
  cursor: pointer;
  font-size: 0.9rem;
  transition: all 0.2s;
}

.dark-toggle:hover {
  background: rgba(255,255,255,0.2);
}

/* ===== MAIN ===== */
main {
  min-height: calc(100vh - var(--header-height) - 200px);
}

/* ===== SECTIONS ===== */
.section { display: none; }
.section.active { display: block; }

/* ===== HERO ===== */
.hero {
  height: 500px;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
}

.hero-overlay {
  background: rgba(0,0,0,0.55);
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 30px;
  color: white;
}

.hero-overlay h1 {
  font-size: 2.2rem;
  margin-bottom: 15px;
  text-shadow: 0 2px 4px rgba(0,0,0,0.5);
}

.hero-overlay p {
  font-size: 1.15rem;
  margin-bottom: 25px;
  opacity: 0.9;
  max-width: 600px;
}

.hero-buttons {
  display: flex;
  gap: 15px;
  flex-wrap: wrap;
  justify-content: center;
}

/* ===== STATS BAR ===== */
.stats-bar {
  background: var(--primary);
  display: flex;
  justify-content: center;
  gap: 60px;
  padding: 20px;
}

.stat-item {
  text-align: center;
  color: white;
}

.stat-number {
  display: block;
  font-size: 2rem;
  font-weight: bold;
}

.stat-label {
  font-size: 0.9rem;
  opacity: 0.85;
}

/* ===== HOME SECTIONS ===== */
.home-section {
  max-width: 1100px;
  margin: 40px auto;
  padding: 0 20px;
}

.home-section h2 {
  color: var(--primary);
  font-size: 1.6rem;
  margin-bottom: 20px;
  border-bottom: 3px solid var(--primary-light);
  padding-bottom: 10px;
}

/* ===== GALLERY ===== */
.gallery {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 15px;
}

.gallery img {
  width: 100%;
  height: 180px;
  object-fit: cover;
  border-radius: 8px;
  transition: transform 0.3s;
  cursor: pointer;
}

.gallery img:hover {
  transform: scale(1.03);
}

/* ===== QURAN SECTION ===== */
.quran-section {
  background-size: cover;
  background-position: center;
  border-radius: 12px;
  overflow: hidden;
  max-width: 1100px;
  margin: 40px auto;
  padding: 0 !important;
}

.quran-overlay {
  background: rgba(26, 107, 60, 0.85);
  padding: 60px 40px;
  text-align: center;
  color: white;
}

.quran-overlay h2 {
  color: white !important;
  border: none !important;
  font-size: 1.8rem;
  margin-bottom: 10px;
}

.quran-overlay p {
  font-size: 1.1rem;
  margin-bottom: 20px;
  opacity: 0.9;
}

/* ===== GRID ===== */
.grid-3 {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}

/* ===== SECTION HEADER ===== */
.section-header {
  height: 250px;
  background-size: cover;
  background-position: center;
  position: relative;
}

.section-header-overlay {
  background: rgba(0,0,0,0.55);
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  color: white;
  padding: 20px;
}

.section-header-overlay h2 {
  font-size: 2rem;
  margin-bottom: 8px;
}

.section-header-overlay p {
  font-size: 1rem;
  opacity: 0.9;
}

/* ===== SECTION BODY ===== */
.section-body {
  max-width: 1000px;
  margin: 30px auto;
  padding: 0 20px;
}

/* ===== SEARCH ===== */
.search-row {
  display: flex;
  gap: 20px;
  margin-bottom: 20px;
  flex-wrap: wrap;
}

.search-box {
  display: flex;
  gap: 10px;
  flex: 1;
  min-width: 250px;
}

.search-box input {
  flex: 1;
  padding: 12px 15px;
  border: 1px solid var(--border);
  border-radius: 6px;
  font-size: 1rem;
  background: var(--card-bg);
  color: var(--text);
  outline: none;
  transition: border 0.2s;
}

.search-box input:focus {
  border-color: var(--primary);
}

.search-box button {
  padding: 12px 25px;
  background: var(--primary);
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-size: 1rem;
  transition: background 0.2s;
  white-space: nowrap;
}

.search-box button:hover {
  background: var(--primary-dark);
}

/* ===== BUTTONS ===== */
.btn-primary {
  background: var(--secondary);
  color: white;
  border: none;
  padding: 12px 25px;
  border-radius: 6px;
  font-size: 1rem;
  cursor: pointer;
  margin: 5px;
  transition: all 0.2s;
}

.btn-primary:hover {
  opacity: 0.9;
  transform: translateY(-1px);
}

.btn-secondary {
  background: transparent;
  color: white;
  border: 2px solid white;
  padding: 12px 25px;
  border-radius: 6px;
  font-size: 1rem;
  cursor: pointer;
  margin: 5px;
  transition: all 0.2s;
}

.btn-secondary:hover {
  background: rgba(255,255,255,0.2);
}

.btn-full {
  width: 100%;
  margin: 0;
  padding: 14px;
  font-size: 1.05rem;
}

/* ===== CARDS ===== */
.results { margin-top: 15px; }

.card {
  background: var(--card-bg);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 15px;
  box-shadow: var(--shadow);
  transition: transform 0.2s;
}

.card:hover { transform: translateY(-2px); }

.card h3 {
  color: var(--primary);
  margin-bottom: 8px;
  font-size: 1.1rem;
}

.card p {
  color: var(--text-light);
  font-size: 0.95rem;
  margin-bottom: 5px;
}

.card-badge {
  display: inline-block;
  background: var(--primary-light);
  color: var(--primary);
  padding: 3px 10px;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: bold;
  margin-top: 8px;
}

/* ===== FEATURES ===== */
.features {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 20px;
}

.feature-card {
  background: var(--card-bg);
  padding: 25px;
  border-radius: 10px;
  text-align: center;
  box-shadow: var(--shadow);
  transition: transform 0.2s;
  cursor: pointer;
}

.feature-card:hover { transform: translateY(-4px); }

.feature-card span { font-size: 2.5rem; }

.feature-card h3 {
  margin: 10px 0 8px;
  color: var(--primary);
}

.feature-card p {
  color: var(--text-light);
  font-size: 0.9rem;
}

/* ===== AUTH ===== */
.auth-container {
  display: flex;
  min-height: 500px;
  max-width: 900px;
  margin: 40px auto;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: var(--shadow);
}

.auth-image {
  flex: 1;
  background-size: cover;
  background-position: center;
  min-height: 400px;
}

.auth-form {
  flex: 1;
  background: var(--card-bg);
  padding: 40px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.auth-form h2 {
  color: var(--primary);
  margin-bottom: 25px;
  font-size: 1.8rem;
}

.form-group { margin-bottom: 20px; }

.form-group label {
  display: block;
  margin-bottom: 6px;
  font-weight: bold;
  color: var(--text);
}

.form-group input {
  width: 100%;
  padding: 12px 15px;
  border: 1px solid var(--border);
  border-radius: 6px;
  font-size: 1rem;
  background: var(--card-bg);
  color: var(--text);
  outline: none;
  transition: border 0.2s;
}

.form-group input:focus { border-color: var(--primary); }

/* ===== ABOUT ===== */
.about-content {
  background: var(--card-bg);
  padding: 30px;
  border-radius: 10px;
  box-shadow: var(--shadow);
  line-height: 1.8;
}

.about-content h3 {
  color: var(--primary);
  margin-bottom: 10px;
}

.about-content ul {
  list-style: none;
  padding-left: 10px;
}

.about-content ul li { padding: 5px 0; }

/* ===== FOOTER ===== */
footer {
  background: #1a1a2e;
  color: #ccc;
  margin-top: 60px;
}

.footer-content {
  max-width: 1000px;
  margin: 0 auto;
  padding: 40px 20px;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 30px;
}

.footer-section h3 {
  color: white;
  margin-bottom: 15px;
}

.footer-section p {
  font-size: 0.9rem;
  line-height: 1.7;
}

.footer-section a {
  display: block;
  color: #aaa;
  text-decoration: none;
  padding: 3px 0;
  font-size: 0.9rem;
  transition: color 0.2s;
}

.footer-section a:hover { color: white; }

.footer-bottom {
  border-top: 1px solid #333;
  text-align: center;
  padding: 15px;
  font-size: 0.85rem;
  color: #888;
}

/* ===== RESPONSIVE ===== */
@media (max-width: 768px) {
  header {
    flex-wrap: wrap;
    height: auto;
    padding: 10px 15px;
    gap: 10px;
  }

  nav {
    order: 3;
    width: 100%;
    overflow-x: auto;
    padding-bottom: 5px;
  }

  .nav-link {
    font-size: 0.85rem;
    padding: 6px 10px;
    white-space: nowrap;
  }

  .hero { height: 350px; }
  .hero-overlay h1 { font-size: 1.5rem; }

  .stats-bar { gap: 25px; }

  .gallery {
    grid-template-columns: repeat(2, 1fr);
  }

  .grid-3 {
    grid-template-columns: 1fr;
  }

  .auth-container {
    flex-direction: column;
  }

  .auth-image { min-height: 200px; }

  .search-row { flex-direction: column; }
}

@media (max-width: 480px) {
  .logo-text { font-size: 1rem; }
  .stats-bar { gap: 15px; }
  .stat-number { font-size: 1.5rem; }
  .gallery { grid-template-columns: 1fr 1fr; }
  .hero-overlay h1 { font-size: 1.2rem; }
}
