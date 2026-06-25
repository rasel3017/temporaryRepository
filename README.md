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

.logo-icon {
  font-size: 1.8rem;
}

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

/* DARK MODE TOGGLE */
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
  max-width: 1000px;
  margin: 30px auto;
  padding: 0 20px;
  min-height: calc(100vh - var(--header-height) - 200px);
}

/* ===== SECTIONS ===== */
.section {
  display: none;
}

.section.active {
  display: block;
}

/* ===== HERO ===== */
.hero {
  background: linear-gradient(135deg, var(--primary), var(--primary-dark));
  color: white;
  padding: 60px 40px;
  border-radius: 12px;
  text-align: center;
  margin-bottom: 30px;
}

.hero h1 {
  font-size: 2rem;
  margin-bottom: 15px;
}

.hero p {
  font-size: 1.1rem;
  opacity: 0.9;
  margin-bottom: 25px;
}

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

/* ===== FEATURE CARDS ===== */
.features {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
  margin-top: 20px;
}

.feature-card {
  background: var(--card-bg);
  padding: 25px;
  border-radius: 10px;
  text-align: center;
  box-shadow: var(--shadow);
  transition: transform 0.2s;
}

.feature-card:hover {
  transform: translateY(-4px);
}

.feature-card span {
  font-size: 2.5rem;
}

.feature-card h3 {
  margin: 10px 0 8px;
  color: var(--primary);
}

.feature-card p {
  color: var(--text-light);
  font-size: 0.9rem;
}

/* ===== SECTION CARDS ===== */
section h2 {
  color: var(--primary);
  margin-bottom: 20px;
  font-size: 1.6rem;
  border-bottom: 3px solid var(--primary-light);
  padding-bottom: 10px;
}

/* ===== SEARCH BOX ===== */
.search-box {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
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
}

.search-box button:hover {
  background: var(--primary-dark);
}

/* ===== RESULTS ===== */
.results {
  margin-top: 15px;
}

.card {
  background: var(--card-bg);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 15px;
  box-shadow: var(--shadow);
  transition: transform 0.2s;
}

.card:hover {
  transform: translateY(-2px);
}

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

/* ===== FORM ===== */
.form-container {
  background: var(--card-bg);
  padding: 30px;
  border-radius: 10px;
  box-shadow: var(--shadow);
  max-width: 450px;
}

.form-group {
  margin-bottom: 20px;
}

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

.form-group input:focus {
  border-color: var(--primary);
}

/* ===== ABOUT ===== */
.about-content {
  background: var(--card-bg);
  padding: 30px;
  border-radius: 10px;
  box-shadow: var(--shadow);
  line-height: 1.8;
}

.about-content ul {
  list-style: none;
  padding-left: 10px;
}

.about-content ul li {
  padding: 5px 0;
}

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
  font-size: 1.1rem;
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

.footer-section a:hover {
  color: white;
}

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
    padding: 0 15px;
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

  .hero h1 {
    font-size: 1.4rem;
  }

  .hero {
    padding: 40px 20px;
  }

  .search-box {
    flex-direction: column;
  }

  .form-container {
    max-width: 100%;
  }
}

@media (max-width: 480px) {
  .logo-text {
    font-size: 1rem;
  }

  main {
    padding: 0 15px;
    margin: 20px auto;
  }
}
