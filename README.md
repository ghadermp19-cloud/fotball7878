# fotball7878 <!DOCTYPE html>
<html lang="fa">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ورود و ثبت‌نام شیک</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Vazirmatn:wght@400;700&display=swap');

body {
  font-family: 'Vazirmatn', sans-serif;
  background: linear-gradient(135deg,#4CAF50,#2E7D32);
  margin:0;
  padding:0;
  height:100vh;
  display:flex;
  justify-content:center;
  align-items:center;
}

.container {
  background:#fff;
  border-radius:12px;
  box-shadow:0 10px 25px rgba(0,0,0,0.3);
  width:350px;
  padding:30px;
  text-align:center;
  position:relative;
  overflow:hidden;
}

h2 {
  margin-bottom:25px;
  color:#2E7D32;
}

input {
  width:100%;
  padding:12px 15px;
  margin:10px 0;
  border-radius:8px;
  border:1px solid #ccc;
  outline:none;
  transition:0.3s;
}

input:focus {
  border-color:#4CAF50;
  box-shadow:0 0 5px #4CAF50;
}

button {
  width:100%;
  padding:12px;
  border:none;
  border-radius:8px;
  background:#4CAF50;
  color:white;
  font-size:16px;
  cursor:pointer;
  transition:0.3s;
  margin-top:10px;
}

button:hover {
  background:#388E3C;
}

.message {
  margin-top:10px;
  font-weight:600;
}

.switch {
  margin-top:15px;
  color:#4CAF50;
  cursor:pointer;
  font-weight:bold;
  text-decoration:underline;
}

.hidden { display:none; }
</style>
</head>
<body>

<div class="container">
  <h2 id="formTitle">ورود</h2>

  <!-- فرم ورود -->
  <div id="loginForm">
    <input type="text" id="loginUsername" placeholder="نام کاربری">
    <input type="password" id="loginPassword" placeholder="رمز عبور">
    <button onclick="loginUser()">ورود</button>
    <div class="message" id="loginMessage"></div>
    <div class="switch" onclick="toggleForm()">ساخت حساب کاربری</div>
  </div>

  <!-- فرم ثبت‌نام -->
  <div id="registerForm" class="hidden">
    <input type="text" id="registerUsername" placeholder="نام کاربری">
    <input type="password" id="registerPassword" placeholder="رمز عبور">
    <button onclick="registerUser()">ثبت‌نام</button>
    <div class="message" id="registerMessage"></div>
    <div class="switch" onclick="toggleForm()">ورود</div>
  </div>
</div>

<script>
// سوییچ بین ورود و ثبت‌نام
function toggleForm() {
  document.getElementById('loginForm').classList.toggle('hidden');
  document.getElementById('registerForm').classList.toggle('hidden');
  document.getElementById('formTitle').innerText = document.getElementById('loginForm').classList.contains('hidden') ? "ثبت‌نام" : "ورود";
}

// ذخیره کاربران در LocalStorage
let users = JSON.parse(localStorage.getItem('users') || '[]');

// ثبت‌نام
function registerUser() {
  const username = document.getElementById('registerUsername').value.trim();
  const password = document.getElementById('registerPassword').value.trim();
  const users = JSON.parse(localStorage.getItem('users') || '[]');
  const msg = document.getElementById('registerMessage');

  if(!username || !password){
    msg.style.color="red";
    msg.innerText = "نام کاربری و رمز را وارد کنید.";
    return;
  }

  if(users.find(u => u.username === username)){
    msg.style.color="red";
    msg.innerText = "این نام کاربری قبلاً استفاده شده.";
    return;
  }

  users.push({username,password});
  localStorage.setItem('users', JSON.stringify(users));
  msg.style.color="green";
  msg.innerText = "ثبت‌نام با موفقیت انجام شد!";
  document.getElementById('registerUsername').value='';
  document.getElementById('registerPassword').value='';
}

// ورود
function loginUser() {
  const username = document.getElementById('loginUsername').value.trim();
  const password = document.getElementById('loginPassword').value.trim();
  const users = JSON.parse(localStorage.getItem('users') || '[]');
  const msg = document.getElementById('loginMessage');

  const user = users.find(u => u.username === username && u.password === password);
  if(user){
    msg.style.color="green";
    msg.innerText = "ورود موفق!";
    setTimeout(()=>alert(`خوش آمدید ${username}`),500);
  } else {
    msg.style.color="red";
    msg.innerText = "نام کاربری یا رمز عبور اشتباه است.";
  }
}
</script>

</body>
</html>
