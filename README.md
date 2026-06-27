<!-- PRAYER TIMES SECTION -->
<section id="prayer" class="section">
  <div class="section-header" style="background-image: url('images/mosque4.jpg')">
    <div class="section-header-overlay">
      <h2>🕐 Prayer Times</h2>
      <p>Daily prayer times for any district in Bangladesh</p>
    </div>
  </div>
  <div class="section-body">
    <div class="search-box">
      <input type="text" id="prayerCity" placeholder="Enter city/district (e.g. Dhaka, Chittagong)">
      <button onclick="fetchPrayerTimes(document.getElementById('prayerCity').value)">Get Times</button>
    </div>
    <div id="prayerResults"></div>
  </div>
</section>

<!-- RAMADAN SECTION -->
<section id="ramadan" class="section">
  <div class="section-header" style="background-image: url('images/quran4.jpg')">
    <div class="section-header-overlay">
      <h2>🌙 Ramadan Schedule 2027</h2>
      <p>Sehri and Iftar times by district</p>
    </div>
  </div>
  <div class="section-body">
    <div class="search-box">
      <input type="text" id="ramadanCity" placeholder="Enter city/district (e.g. Dhaka, Chittagong)">
      <button onclick="fetchRamadanSchedule(document.getElementById('ramadanCity').value)">Get Schedule</button>
    </div>
    <div id="ramadanResults"></div>
  </div>
</section>
