<!-- PROFILE SECTION -->
<section id="profile" class="section">
  <div class="section-header" style="background-image: url('images/mosque1.jpg')">
    <div class="section-header-overlay">
      <h2>👤 My Profile</h2>
      <p>View and update your account information</p>
    </div>
  </div>
  <div class="section-body">
    <div class="form-container">
      <div class="form-group">
        <label>Name</label>
        <input type="text" id="profileName" placeholder="Your name">
      </div>
      <div class="form-group">
        <label>Email</label>
        <input type="email" id="profileEmail" placeholder="Your email">
      </div>
      <div class="form-group">
        <label>New Password (leave blank to keep current)</label>
        <input type="password" id="profilePassword" placeholder="New password">
      </div>
      <button class="btn-primary btn-full" onclick="updateProfile()">Update Profile</button>
    </div>
  </div>
</section>
