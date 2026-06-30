.admin-tabs {
  display: flex;
  gap: 10px;
  margin-bottom: 25px;
  flex-wrap: wrap;
}

.admin-tab {
  padding: 12px 25px;
  background: var(--card-bg);
  border: 1px solid var(--border);
  border-radius: 6px;
  cursor: pointer;
  font-size: 1rem;
  color: var(--text);
  transition: all 0.2s;
}

.admin-tab.active {
  background: var(--primary);
  color: white;
  border-color: var(--primary);
}

.admin-tab-content {
  display: none;
}

.admin-tab-content.active {
  display: block;
}
