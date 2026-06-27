/* ===== MOSQUE CARD ===== */
.card-image {
  width: 100%;
  height: 200px;
  object-fit: cover;
  border-radius: 6px 6px 0 0;
  margin-bottom: 15px;
}

.card-body { padding: 0; }

.prayer-mini {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-top: 10px;
  background: var(--primary-light);
  padding: 8px;
  border-radius: 6px;
}

.prayer-mini span {
  font-size: 0.8rem;
  color: var(--primary);
  font-weight: bold;
}

.map-btn {
  display: inline-block;
  margin-top: 10px;
  padding: 8px 15px;
  background: var(--primary);
  color: white;
  border-radius: 5px;
  text-decoration: none;
  font-size: 0.9rem;
  transition: background 0.2s;
}

.map-btn:hover { background: var(--primary-dark); }

/* ===== EVENT CARD ===== */
.card-badge.free {
  background: #e8f5ee;
  color: #1a6b3c;
}

.card-badge.paid {
  background: #fff3e0;
  color: #e65100;
}

.card-badge.accepted {
  background: #e8f5ee;
  color: #1a6b3c;
}

/* ===== EVENT ANNOUNCEMENT ===== */
.event-announcement-card {
  background: var(--card-bg);
  border-radius: 10px;
  overflow: hidden;
  box-shadow: var(--shadow);
  transition: transform 0.2s;
}

.event-announcement-card:hover {
  transform: translateY(-4px);
}

.event-announcement-card img {
  width: 100%;
  height: 160px;
  object-fit: cover;
}

.no-image {
  width: 100%;
  height: 160px;
  background: var(--primary-light);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 3rem;
}

.event-announcement-body {
  padding: 15px;
}

.event-announcement-body h3 {
  color: var(--primary);
  margin-bottom: 8px;
}

.event-announcement-body p {
  color: var(--text-light);
  font-size: 0.9rem;
  margin-bottom: 4px;
}

/* ===== Q&A ===== */
.qa-card .answers {
  margin-top: 15px;
  border-top: 1px solid var(--border);
  padding-top: 15px;
}

.qa-card .answers h4 {
  color: var(--primary);
  margin-bottom: 10px;
}

.answer-item {
  background: var(--primary-light);
  padding: 10px;
  border-radius: 6px;
  margin-bottom: 8px;
}

.answer-item p {
  color: var(--text);
  font-size: 0.9rem;
}

/* ===== PRAYER TIMES ===== */
.prayer-card {
  background: var(--card-bg);
  border-radius: 10px;
  padding: 25px;
  box-shadow: var(--shadow);
  margin-top: 15px;
}

.prayer-card h3 {
  color: var(--primary);
  margin-bottom: 5px;
}

.prayer-times-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 15px;
  margin-top: 20px;
}

.prayer-time-item {
  background: var(--primary-light);
  padding: 20px;
  border-radius: 8px;
  text-align: center;
}

.prayer-time-item.fajr { background: #e3f2fd; }
.prayer-time-item.zuhr { background: #fff8e1; }
.prayer-time-item.asr { background: #f3e5f5; }
.prayer-time-item.maghrib { background: #fce4ec; }
.prayer-time-item.isha { background: #e8eaf6; }

.prayer-name {
  display: block;
  font-weight: bold;
  color: var(--primary);
  font-size: 1rem;
  margin-bottom: 8px;
}

.prayer-time {
  display: block;
  font-size: 1.4rem;
  font-weight: bold;
  color: var(--text);
}

/* ===== RAMADAN ===== */
.ramadan-header {
  background: linear-gradient(135deg, #1a1a2e, #16213e);
  color: white;
  padding: 20px;
  border-radius: 10px;
  margin-bottom: 15px;
  text-align: center;
}

.ramadan-header h3 { margin-bottom: 5px; }

.ramadan-table {
  background: var(--card-bg);
  border-radius: 10px;
  overflow: hidden;
  box-shadow: var(--shadow);
}

.ramadan-row {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr;
  padding: 12px 20px;
  border-bottom: 1px solid var(--border);
  align-items: center;
}

.ramadan-row.header {
  background: var(--primary);
  color: white;
  font-weight: bold;
}

.ramadan-row.even {
  background: var(--primary-light);
}

/* ===== USER GREETING ===== */
.user-greeting {
  color: white;
  font-size: 0.95rem;
}

/* ===== RESPONSIVE ADDITIONS ===== */
@media (max-width: 768px) {
  .prayer-times-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .ramadan-row {
    grid-template-columns: 1fr 1fr;
    gap: 5px;
  }

  .ramadan-row span:first-child {
    grid-column: 1 / -1;
    font-weight: bold;
  }
}

@media (max-width: 480px) {
  .prayer-times-grid {
    grid-template-columns: 1fr 1fr;
  }
}
