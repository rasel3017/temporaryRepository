/* ===== MOBILE FIX ===== */
@media (max-width: 768px) {
  
  /* Header */
  header {
    flex-wrap: wrap;
    height: auto;
    padding: 10px 15px;
    gap: 8px;
  }

  nav {
    order: 3;
    width: 100%;
    overflow-x: auto;
    display: flex;
    gap: 3px;
    padding-bottom: 5px;
  }

  .nav-link {
    font-size: 0.75rem;
    padding: 5px 8px;
    white-space: nowrap;
  }

  .auth-buttons {
    gap: 6px;
  }

  .btn-login {
    padding: 6px 12px;
    font-size: 0.85rem;
  }

  .dark-toggle {
    padding: 5px 8px;
    font-size: 0.8rem;
  }

  /* Hero */
  .hero { height: 280px; }
  .hero-overlay h1 { font-size: 1.2rem; }
  .hero-overlay p { font-size: 0.9rem; }
  .hero-buttons { flex-direction: column; align-items: center; }

  /* Stats */
  .stats-bar { 
    flex-wrap: wrap;
    gap: 15px;
    padding: 15px;
  }
  .stat-number { font-size: 1.5rem; }

  /* Gallery */
  .gallery { grid-template-columns: repeat(2, 1fr); }

  /* Grid */
  .grid-3 { grid-template-columns: 1fr; }

  /* Features */
  .features { grid-template-columns: repeat(2, 1fr); }

  /* Section header */
  .section-header { height: 180px; }
  .section-header-overlay h2 { font-size: 1.5rem; }

  /* Search */
  .search-row { flex-direction: column; }
  .search-box { flex-direction: column; }
  .search-box input { width: 100%; }
  .search-box button { width: 100%; }

  /* Cards */
  .card-image { height: 150px; }

  /* Auth */
  .auth-container { flex-direction: column; }
  .auth-image { min-height: 150px; }
  .auth-form { padding: 20px; }

  /* Admin tabs */
  .admin-tabs { flex-direction: column; }
  .admin-tab { width: 100%; }

  /* Prayer times */
  .prayer-times-grid { grid-template-columns: repeat(2, 1fr); }

  /* Ramadan */
  .ramadan-row { 
    grid-template-columns: 1fr 1fr;
    font-size: 0.8rem;
  }
  .ramadan-row span:first-child {
    grid-column: 1 / -1;
    font-weight: bold;
  }

  /* Footer */
  .footer-content { grid-template-columns: 1fr; }
}

@media (max-width: 480px) {
  .features { grid-template-columns: 1fr; }
  .gallery { grid-template-columns: 1fr 1fr; }
  .prayer-times-grid { grid-template-columns: repeat(2, 1fr); }
  .logo-text { font-size: 0.95rem; }
  .hero-overlay h1 { font-size: 1rem; }
}
