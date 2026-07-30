div.innerHTML = data.data.slice(0, 3).map(e => `
  <div class="event-announcement-card" onclick="showEventDetails('${e.id}')" style="cursor:pointer;">
    ${e.imageUrl ? `<img src="${e.imageUrl}" alt="${e.title}">` : `<div class="no-image">📅</div>`}
    <div class="event-announcement-body">
      <h3>${e.title}</h3>
      <p>🎤 ${e.speaker}</p>
      <p>📅 ${new Date(e.eventDate).toLocaleDateString('en-BD')}</p>
      <p>⏰ ${e.eventTime}</p>
      ${e.location ? `<p>📍 ${e.location}</p>` : ""}
      <span class="card-badge ${e.isFree ? 'free' : 'paid'}">${e.isFree ? "Free Entry" : "Paid"}</span>
    </div>
  </div>
`).join("");
