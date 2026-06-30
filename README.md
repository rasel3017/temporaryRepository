<!-- ADMIN SECTION -->
<section id="admin" class="section">
  <div class="section-header" style="background-image: url('images/mosque2.jpg')">
    <div class="section-header-overlay">
      <h2>⚙️ Admin Dashboard</h2>
      <p>Manage mosques, maktabs and events</p>
    </div>
  </div>
  <div class="section-body">

    <div class="admin-tabs">
      <button class="admin-tab active" onclick="showAdminTab('addMosqueTab')">Add Mosque</button>
      <button class="admin-tab" onclick="showAdminTab('addMaktabTab')">Add Maktab</button>
      <button class="admin-tab" onclick="showAdminTab('addEventTab')">Add Event</button>
    </div>

    <!-- ADD MOSQUE FORM -->
    <div id="addMosqueTab" class="admin-tab-content active">
      <div class="form-container">
        <h3>Add New Mosque</h3>
        <div class="form-group"><label>Name</label><input type="text" id="m_name" placeholder="Mosque name"></div>
        <div class="form-group"><label>Address</label><input type="text" id="m_address" placeholder="Full address"></div>
        <div class="form-group"><label>Region</label><input type="text" id="m_region" placeholder="e.g. Dhaka"></div>
        <div class="form-group"><label>Imam Name</label><input type="text" id="m_imam" placeholder="Imam name"></div>
        <div class="form-group"><label>Muazzin Name</label><input type="text" id="m_muazzin" placeholder="Muazzin name"></div>
        <div class="form-group"><label>Image URL</label><input type="text" id="m_image" placeholder="images/mosque1.jpg"></div>
        <div class="form-group"><label>Latitude</label><input type="text" id="m_lat" placeholder="23.7275"></div>
        <div class="form-group"><label>Longitude</label><input type="text" id="m_lng" placeholder="90.4099"></div>
        <button class="btn-primary btn-full" onclick="adminAddMosque()">Add Mosque</button>
      </div>
    </div>

    <!-- ADD MAKTAB FORM -->
    <div id="addMaktabTab" class="admin-tab-content">
      <div class="form-container">
        <h3>Add New Maktab</h3>
        <div class="form-group"><label>Name</label><input type="text" id="mk_name" placeholder="Maktab name"></div>
        <div class="form-group"><label>Address</label><input type="text" id="mk_address" placeholder="Full address"></div>
        <div class="form-group"><label>Ustad Name</label><input type="text" id="mk_teacher" placeholder="Teacher name"></div>
        <div class="form-group"><label>Phone</label><input type="text" id="mk_phone" placeholder="Phone number"></div>
        <div class="form-group"><label>Total Seats</label><input type="number" id="mk_seats" placeholder="50"></div>
        <div class="form-group"><label>Courses Offered</label><input type="text" id="mk_courses" placeholder="Quran, Tajweed, Arabic"></div>
        <div class="form-group"><label>Image URL</label><input type="text" id="mk_image" placeholder="images/quran1.jpg"></div>
        <div class="form-group"><label>Mosque ID (optional)</label><input type="text" id="mk_mosqueId" placeholder="Leave blank if independent"></div>
        <button class="btn-primary btn-full" onclick="adminAddMaktab()">Add Maktab</button>
      </div>
    </div>

    <!-- ADD EVENT FORM -->
    <div id="addEventTab" class="admin-tab-content">
      <div class="form-container">
        <h3>Add New Event</h3>
        <div class="form-group"><label>Title</label><input type="text" id="e_title" placeholder="Event title"></div>
        <div class="form-group"><label>Topic</label><input type="text" id="e_topic" placeholder="Event topic"></div>
        <div class="form-group"><label>Speaker</label><input type="text" id="e_speaker" placeholder="Speaker name"></div>
        <div class="form-group"><label>Date</label><input type="date" id="e_date"></div>
        <div class="form-group"><label>Time</label><input type="text" id="e_time" placeholder="08:00 PM"></div>
        <div class="form-group"><label>Location</label><input type="text" id="e_location" placeholder="Event location"></div>
        <div class="form-group"><label>Description</label><input type="text" id="e_description" placeholder="Biryani, free Quran etc."></div>
        <div class="form-group"><label>Image URL</label><input type="text" id="e_image" placeholder="images/event1.jpg"></div>
        <div class="form-group"><label>Mosque ID (optional)</label><input type="text" id="e_mosqueId" placeholder="Leave blank if independent"></div>
        <button class="btn-primary btn-full" onclick="adminAddEvent()">Add Event</button>
      </div>
    </div>

  </div>
</section>
