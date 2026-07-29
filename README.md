<!-- ENROLL STUDENT FORM -->
<div id="enrollStudentTab" class="admin-tab-content">
  <div class="form-container">
    <h3>Enroll Student</h3>
    <div class="form-group"><label>Maktab ID</label><input type="text" id="s_maktabId" placeholder="Maktab ID"></div>
    <div class="form-group"><label>Student Name</label><input type="text" id="s_name" placeholder="Student name"></div>
    <div class="form-group"><label>Age</label><input type="number" id="s_age" placeholder="Age"></div>
    <div class="form-group"><label>Address</label><input type="text" id="s_address" placeholder="Address"></div>
    <div class="form-group"><label>Guardian Phone</label><input type="text" id="s_phone" placeholder="Guardian phone"></div>
    <button class="btn-primary btn-full" onclick="adminEnrollStudent()">Enroll Student</button>
  </div>
</div>

<!-- ADD FUNDING FORM -->
<div id="addFundingTab" class="admin-tab-content">
  <div class="form-container">
    <h3>Add Funding</h3>
    <div class="form-group">
      <label>Fund To</label>
      <select id="f_type" style="width:100%; padding:12px; border:1px solid var(--border); border-radius:6px; background:var(--card-bg); color:var(--text);">
        <option value="mosque">Mosque</option>
        <option value="maktab">Maktab</option>
      </select>
    </div>
    <div class="form-group"><label>Mosque/Maktab ID</label><input type="text" id="f_id" placeholder="ID of mosque or maktab"></div>
    <div class="form-group"><label>Donor Name (optional)</label><input type="text" id="f_donor" placeholder="Leave blank for Anonymous"></div>
    <div class="form-group"><label>Amount (BDT)</label><input type="number" id="f_amount" placeholder="5000"></div>
    <div class="form-group"><label>Note</label><input type="text" id="f_note" placeholder="Purpose of donation"></div>
    <button class="btn-primary btn-full" onclick="adminAddFunding()">Add Funding</button>
  </div>
</div>

<!-- VIEW DATA -->
<div id="viewDataTab" class="admin-tab-content">
  <div class="section-body" style="padding:0;">
    <div class="search-box" style="margin-bottom:15px;">
      <input type="text" id="v_maktabId" placeholder="Enter Maktab ID to view students">
      <button onclick="adminGetStudents()">View Students</button>
    </div>
    <div id="studentResults" class="results"></div>
    <div class="search-box" style="margin-top:20px; margin-bottom:15px;">
      <select id="v_fundType" style="padding:12px; border:1px solid var(--border); border-radius:6px; background:var(--card-bg); color:var(--text);">
        <option value="mosque">Mosque Funding</option>
        <option value="maktab">Maktab Funding</option>
      </select>
      <input type="text" id="v_fundId" placeholder="Enter Mosque/Maktab ID">
      <button onclick="adminGetFunding()">View Funding</button>
    </div>
    <div id="fundingResults" class="results"></div>
  </div>
</div>

<!-- DELETE TAB -->
<div id="deleteTab" class="admin-tab-content">
  <div class="form-container">
    <h3>Delete Records</h3>
    <div class="form-group">
      <label>What to delete?</label>
      <select id="d_type" style="width:100%; padding:12px; border:1px solid var(--border); border-radius:6px; background:var(--card-bg); color:var(--text);">
        <option value="mosque">Mosque</option>
        <option value="maktab">Maktab</option>
        <option value="event">Event</option>
      </select>
    </div>
    <div class="form-group"><label>ID</label><input type="text" id="d_id" placeholder="Enter ID to delete"></div>
    <button class="delete-btn" style="width:100%; padding:14px;" onclick="adminDelete()">🗑️ Delete</button>
  </div>
</div>
