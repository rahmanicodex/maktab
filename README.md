
<html lang="fa" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <title>سامانه مدیریت مکتب افغان</title>
  <link href="https://fonts.googleapis.com/css2?family=Vazirmatn&display=swap" rel="stylesheet" />
  <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css"
  />
  <style>
    * {
      font-family: 'Vazirmatn', sans-serif;
    }
    body {
      background: url('https://images.unsplash.com/photo-1577896851231-70ef18881754?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80')
        no-repeat center center fixed;
      background-size: cover;
      margin: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      padding: 15px;
    }
    .container,
    .admin-panel,
    .teacher-panel,
    .parent-panel {
      background-color: rgba(255, 255, 255, 0.95);
      border-radius: 15px;
      padding: 30px;
      width: 100%;
      max-width: 600px;
      box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);
      text-align: center;
      box-sizing: border-box;
      overflow-y: auto;
      max-height: 90vh;
    }
    h1,
    h2,
    h3 {
      color: #1d3557;
      margin-bottom: 15px;
    }
    input,
    select,
    textarea {
      width: 100%;
      padding: 10px;
      margin-top: 10px;
      border-radius: 10px;
      border: 1px solid #ccc;
      box-sizing: border-box;
      font-size: 14px;
    }
    button {
      width: 100%;
      padding: 10px;
      background-color: #1d3557;
      color: white;
      border: none;
      border-radius: 10px;
      margin-top: 15px;
      font-size: 16px;
      cursor: pointer;
      transition: background-color 0.3s;
    }
    button:hover {
      background-color: #0d1c34;
    }
    .hidden {
      display: none;
    }
    .record {
      background: #f8f9fa;
      border: 1px solid #ccc;
      border-radius: 8px;
      padding: 12px 15px;
      margin-top: 12px;
      text-align: right;
      font-size: 14px;
      line-height: 1.5;
      box-shadow: 1px 1px 3px rgba(0, 0, 0, 0.05);
    }
    .school-info {
      margin-top: 20px;
      text-align: right;
      font-size: 14px;
      line-height: 1.8;
      color: #333;
    }
    .school-info i {
      margin-left: 8px;
      color: #1d3557;
    }
    .user-list {
      text-align: right;
      margin-top: 20px;
    }
    /* استایل بهبود یافته برای لیست کاربران */
    .user-item {
      background: #f1f1f1;
      padding: 8px 12px;
      border-radius: 8px;
      margin-top: 10px;
      display: flex;
      justify-content: flex-start;
      align-items: center;
      gap: 8px;
      flex-wrap: nowrap;
    }
    .user-item input {
      padding: 6px 8px;
      font-size: 14px;
      border-radius: 6px;
      border: 1px solid #ccc;
      width: 130px;
      flex-shrink: 0;
      direction: ltr;
      text-align: left;
    }
    .user-item button {
      padding: 6px 12px;
      font-size: 13px;
      border-radius: 6px;
      background-color: #1d3557;
      color: white;
      border: none;
      cursor: pointer;
      flex-shrink: 0;
      transition: background-color 0.3s;
    }
    .user-item button:hover {
      background-color: #0d1c34;
    }
    /* برای فرم معلم، فیلدهای کوچکتر */
    .teacher-panel input,
    .teacher-panel select,
    .teacher-panel textarea {
      font-size: 14px;
    }
    .teacher-panel button {
      font-size: 15px;
    }
  </style>
</head>
<body>
  <div class="container" id="login-panel">
    <h1>سامانه مدیریت مکتب خصوصی بامیکا</h1>
    <div class="school-info">
      <p><i class="fas fa-map-marker-alt"></i> آدرس: کابل، دشت برچی، ریگریشن</p>
      <p><i class="fas fa-phone"></i> شماره تماس: ۰۷۰۰۱۲۳۴۵۶</p>
      <p><i class="fab fa-whatsapp"></i> واتساپ: ۰۷۰۰۱۲۳۴۵۶</p>
      <p>
        <i class="fab fa-telegram"></i> کانال تلگرام:
        <a href="مکتب خصوصی بامیکا" target="_blank">مکتب خصوصی بامیکا</a>
      </p>
      <p>
        <i class="fab fa-facebook"></i> صفحه فیسبوک:
        <a href="مکتب خصوصی بامیکا" target="_blank">مکتب خصوصی بامیکا</a>
      </p>
    </div>
    <select id="userTypeSelect">
      <option value="admin">مدیر</option>
      <option value="teacher">معلم</option>
      <option value="parent">والدین</option>
    </select>
    <input type="text" id="username" placeholder="نام کاربری" />
    <input type="password" id="password" placeholder="رمز عبور" />
    <button onclick="handleLogin()">ورود</button>
  </div>

  <div class="admin-panel hidden" id="admin-panel">
    <h2>پنل مدیریت</h2>

    <h3>افزودن معلم</h3>
    <input type="text" id="teacherUser" placeholder="نام کاربری معلم" />
    <input type="password" id="teacherPass" placeholder="رمز عبور معلم" />
    <button onclick="registerSpecificUser('teacher')">ثبت معلم</button>
    <div id="teacherList" class="user-list"></div>

    <h3>افزودن والد</h3>
    <input type="text" id="parentUser" placeholder="نام کاربری والد" />
    <input type="password" id="parentPass" placeholder="رمز عبور والد" />
    <button onclick="registerSpecificUser('parent')">ثبت والد</button>
    <div id="parentList" class="user-list"></div>

    <button onclick="logout()">خروج</button>
  </div>

  <div class="teacher-panel hidden" id="teacher-panel">
    <h2>پنل معلم</h2>
    <input type="text" id="studentName" placeholder="نام شاگرد" />
    <input type="text" id="studentFather" placeholder="نام پدر شاگرد" />
    <select id="grade">
      <option disabled selected>انتخاب صنف</option>
      <script>
        for (let i = 1; i <= 10; i++) {
          document.write(
            `<option value="${i}الف">صنف ${i} الف</option><option value="${i}ب">صنف ${i} ب</option>`
          );
        }
      </script>
    </select>
    <input type="text" id="subject" placeholder="مضمون" />
    <select id="performance">
      <option value="عالی">عالی</option>
      <option value="متوسط">متوسط</option>
      <option value="ضعیف">ضعیف</option>
    </select>
    <textarea id="extraNote" placeholder="توضیحات اضافی"></textarea>
    <input type="date" id="recordDate" />
    <button onclick="submitStudentData()">ثبت آمار</button>
    <div id="teacherRecords"></div>
    <button onclick="logout()">خروج</button>
  </div>

  <div class="parent-panel hidden" id="parent-panel">
    <h2>پنل والدین</h2>
    <div id="studentInfo"></div>
    <button onclick="logout()">خروج</button>
  </div>

  <script>
    let users = JSON.parse(localStorage.getItem('users')) || {
      admin: { مدیر: '1234' },
      teacher: {},
      parent: {},
    };
    let studentRecords = JSON.parse(localStorage.getItem('records')) || [];
    let currentUser = null;
    let currentRole = null;

    function saveData() {
      localStorage.setItem('users', JSON.stringify(users));
      localStorage.setItem('records', JSON.stringify(studentRecords));
    }

    function handleLogin() {
      const username = document.getElementById('username').value.trim();
      const password = document.getElementById('password').value.trim();
      const userType = document.getElementById('userTypeSelect').value;
      if (users[userType][username] === password) {
        currentUser = username;
        currentRole = userType;
        document.getElementById('login-panel').classList.add('hidden');
        document.getElementById(`${userType}-panel`).classList.remove('hidden');
        if (userType === 'parent') showStudentInfo();
        if (userType === 'teacher') showTeacherRecords();
        if (userType === 'admin') showUserLists();
      } else {
        alert('اطلاعات ورود نادرست است.');
      }
    }

    function registerSpecificUser(role) {
      const username = document.getElementById(`${role}User`).value.trim();
      const password = document.getElementById(`${role}Pass`).value.trim();
      if (!username || !password) return alert('تمام فیلدها الزامی است.');
      users[role][username] = password;
      saveData();
      document.getElementById(`${role}User`).value = '';
      document.getElementById(`${role}Pass`).value = '';
      alert('کاربر با موفقیت ثبت شد.');
      showUserLists();
    }

    function showUserLists() {
      ['teacher', 'parent'].forEach((role) => {
        const div = document.getElementById(role + 'List');
        div.innerHTML = Object.entries(users[role])
          .map(
            ([user, pass]) => `
          <div class="user-item">
            <input value="${user}" data-role="${role}" data-field="user" />
            <input value="${pass}" data-role="${role}" data-user="${user}" data-field="pass" />
            <button onclick="updateUser(this)">ویرایش</button>
          </div>
        `
          )
          .join('');
      });
    }

    function updateUser(btn) {
      const parentDiv = btn.parentElement;
      const inputs = parentDiv.querySelectorAll('input');
      const userInput = inputs[0];
      const passInput = inputs[1];
      const role = userInput.getAttribute('data-role');
      const oldUsername = passInput.getAttribute('data-user');
      const newUsername = userInput.value.trim();
      const newPass = passInput.value.trim();

      if (!newUsername || !newPass) return alert('نام کاربری و رمز نمی‌توان خالی باشد.');

      // حذف نام کاربری قدیمی و اضافه کردن جدید (برای تغییر نام کاربری)
      if (oldUsername !== newUsername) {
        if (users[role][newUsername]) return alert('نام کاربری تکراری است.');
        delete users[role][oldUsername];
        users[role][newUsername] = newPass;
      } else {
        users[role][oldUsername] = newPass;
      }
      saveData();
      alert('اطلاعات کاربر بروز شد.');
      showUserLists();
    }

    function submitStudentData() {
      const name = document.getElementById('studentName').value.trim();
      const father = document.getElementById('studentFather').value.trim();
      const grade = document.getElementById('grade').value;
      const subject = document.getElementById('subject').value.trim();
      const performance = document.getElementById('performance').value;
      const note = document.getElementById('extraNote').value.trim();
      const date = document.getElementById('recordDate').value;

      if (!name || !father || !grade === 'انتخاب صنف' || !subject || !performance || !date) {
        return alert('لطفاً تمام فیلدها را پر کنید.');
      }

      studentRecords.push({
        name,
        father,
        grade,
        subject,
        performance,
        note,
        date,
        teacher: currentUser,
      });
      saveData();
      alert('آمار با موفقیت ثبت شد.');

      // پاک کردن فیلدها
      document.getElementById('studentName').value = '';
      document.getElementById('studentFather').value = '';
      document.getElementById('grade').selectedIndex = 0;
      document.getElementById('subject').value = '';
      document.getElementById('performance').selectedIndex = 0;
      document.getElementById('extraNote').value = '';
      document.getElementById('recordDate').value = '';
      showTeacherRecords();
    }

    function showTeacherRecords() {
      const div = document.getElementById('teacherRecords');
      const filtered = studentRecords.filter((rec) => rec.teacher === currentUser);
      if (filtered.length === 0) {
        div.innerHTML = '<p>هیچ آمار ثبت شده‌ای وجود ندارد.</p>';
        return;
      }
      div.innerHTML = filtered
        .map(
          (r) => `
        <div class="record">
          <strong>نام شاگرد:</strong> ${r.name} <br/>
          <strong>نام پدر:</strong> ${r.father} <br/>
          <strong>صنف:</strong> ${r.grade} <br/>
          <strong>مضمون:</strong> ${r.subject} <br/>
          <strong>عملکرد:</strong> ${r.performance} <br/>
          <strong>توضیحات اضافی:</strong> ${r.note || '-'} <br/>
          <strong>تاریخ ثبت:</strong> ${r.date}
        </div>
      `
        )
        .join('');
    }

    function showStudentInfo() {
      const div = document.getElementById('studentInfo');
      // فرض کنیم نام کاربری والد برابر نام شاگرد است (می‌تونی تغییرش بدی)
      const records = studentRecords.filter((r) => r.name === currentUser);
      if (records.length === 0) {
        div.innerHTML = '<p>هیچ اطلاعاتی یافت نشد.</p>';
        return;
      }
      div.innerHTML = records
        .map(
          (r) => `
        <div class="record">
          <strong>نام شاگرد:</strong> ${r.name} <br/>
          <strong>نام پدر:</strong> ${r.father} <br/>
          <strong>صنف:</strong> ${r.grade} <br/>
          <strong>مضمون:</strong> ${r.subject} <br/>
          <strong>عملکرد:</strong> ${r.performance} <br/>
          <strong>توضیحات اضافی:</strong> ${r.note || '-'} <br/>
          <strong>تاریخ ثبت:</strong> ${r.date}
        </div>
      `
        )
        .join('');
    }

    function logout() {
      currentUser = null;
      currentRole = null;
      document.getElementById('login-panel').classList.remove('hidden');
      document.getElementById('admin-panel').classList.add('hidden');
      document.getElementById('teacher-panel').classList.add('hidden');
      document.getElementById('parent-panel').classList.add('hidden');
    }
  </script>
</body>
</html>
