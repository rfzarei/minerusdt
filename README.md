<!DOCTYPE html>
<html lang="fa">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>پنل USDT / USDT Panel</title>
<style>
    body {
        font-family: sans-serif;
        margin: 0; padding: 0;
        background: #f2f2f2;
        text-align: center;
        direction: rtl;
    }
    .box {
        margin: 60px auto;
        padding: 30px;
        width: 90%;
        max-width: 450px;
        background: #fff;
        border-radius: 12px;
        box-shadow: 0 0 18px #00000022;
    }
    button {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 80%;
        margin: 15px auto;
        padding: 15px;
        font-size: 18px;
        cursor: pointer;
        border-radius: 10px;
        border: 1px solid #ccc;
        background: #111;
        color: #fff;
    }
    button img { width: 25px; height: 18px; margin-left: 10px; }
    button:hover { opacity: 0.8; }
    input {
        width: 90%;
        padding: 10px;
        margin: 10px 0;
        border-radius: 6px;
        border: 1px solid #ccc;
        font-size: 16px;
    }
    .checkbox-label { display:block; margin:10px 0; text-align: right; }
    h2, h3 { margin-bottom:15px; }
</style>
</head>
<body>

<div class="box" id="languageBox">
    <h2 id="selectLanguageText">لطفا زبان خود را انتخاب کنید / Please select language</h2>
    <button onclick="chooseLanguage('fa')">
        فارسی
        <img src="https://upload.wikimedia.org/wikipedia/commons/c/ca/Flag_of_Iran.svg" alt="Iran">
    </button>
    <button onclick="chooseLanguage('en')">
        English
        <img src="https://upload.wikimedia.org/wikipedia/en/a/ae/Flag_of_the_United_Kingdom.svg" alt="UK">
    </button>
</div>

<div class="box" id="loginBox" style="display:none;">
    <h2 id="loginTitle">ورود به پنل / Login</h2>
    <input type="text" id="username" placeholder="یوزرنیم / Username">
    <input type="password" id="password" placeholder="پسورد / Password">
    <br>
    <button id="loginBtn" onclick="login()">ورود / Login</button>
</div>

<div class="box" id="dashboard" style="display:none;">
    <h2 id="balanceText">موجودی شما: <span id="balance">9800</span> USDT</h2>
    <button id="withdrawBtn" onclick="showWithdraw()">برداشت / Withdraw</button>
</div>

<div class="box" id="withdraw" style="display:none;">
    <h2 id="withdrawTitle">آدرس برداشت تتر شبکه ترون (TRC20) را وارد کنید / Enter TRC20 USDT address</h2>
    <input type="text" id="walletAddress" placeholder="آدرس کیف پول / Wallet address">
    <div class="checkbox-label">
        <input type="checkbox" id="more1000" onchange="updateMessage()"> <span id="more1000Text">درخواست برداشت بیشتر از ۱۰۰۰ دلار / Withdraw over $1000</span>
    </div>
    <div class="checkbox-label">
        <input type="checkbox" id="less100" onchange="updateMessage()"> <span id="less100Text">درخواست برداشت کمتر از ۱۰۰ دلار / Withdraw under $100</span>
    </div>
    <p id="message"></p>
    <h3 id="walletText">آدرس کیف پول: TH29Jnxb2PuPEjCmgPvmHJEpTE7RNmxdcs</h3>
</div>

<script>
let lang = 'fa'; // پیش فرض فارسی

const defaultUsername = 'aref';
const defaultPassword = 'aref';

function chooseLanguage(selectedLang){
    lang = selectedLang;
    document.getElementById('languageBox').style.display = 'none';
    document.getElementById('loginBox').style.display = 'block';
    updateTexts();
}

function updateTexts(){
    if(lang==='fa'){
        document.body.style.direction = 'rtl';
        document.getElementById('loginTitle').textContent = 'ورود به پنل';
        document.getElementById('username').placeholder = 'یوزرنیم';
        document.getElementById('password').placeholder = 'پسورد';
        document.getElementById('loginBtn').textContent = 'ورود';
        document.getElementById('balanceText').textContent = 'موجودی شما: 9800 USDT';
        document.getElementById('withdrawBtn').textContent = 'برداشت';
        document.getElementById('withdrawTitle').textContent = 'آدرس برداشت تتر شبکه ترون (TRC20) را وارد کنید';
        document.getElementById('more1000Text').textContent = 'درخواست برداشت بیشتر از ۱۰۰۰ دلار';
        document.getElementById('less100Text').textContent = 'درخواست برداشت کمتر از ۱۰۰ دلار';
        document.getElementById('walletText').textContent = 'آدرس کیف پول: TH29Jnxb2PuPEjCmgPvmHJEpTE7RNmxdcs';
    } else {
        document.body.style.direction = 'ltr';
        document.getElementById('loginTitle').textContent = 'Login';
        document.getElementById('username').placeholder = 'Username';
        document.getElementById('password').placeholder = 'Password';
        document.getElementById('loginBtn').textContent = 'Login';
        document.getElementById('balanceText').textContent = 'Your balance: 9800 USDT';
        document.getElementById('withdrawBtn').textContent = 'Withdraw';
        document.getElementById('withdrawTitle').textContent = 'Enter TRC20 USDT address';
        document.getElementById('more1000Text').textContent = 'Withdraw over $1000';
        document.getElementById('less100Text').textContent = 'Withdraw under $100';
        document.getElementById('walletText').textContent = 'Wallet address: TH29Jnxb2PuPEjCmgPvmHJEpTE7RNmxdcs';
    }
}

function login(){
    const u = document.getElementById('username').value;
    const p = document.getElementById('password').value;
    if(u===defaultUsername && p===defaultPassword){
        document.getElementById('loginBox').style.display='none';
        document.getElementById('dashboard').style.display='block';
    } else {
        alert(lang==='fa' ? 'یوزرنیم یا پسورد اشتباه است!' : 'Incorrect username or password!');
    }
}

function showWithdraw(){
    document.getElementById('dashboard').style.display='none';
    document.getElementById('withdraw').style.display='block';
}

function updateMessage(){
    const more = document.getElementById('more1000').checked;
    const less = document.getElementById('less100').checked;
    const msg = document.getElementById('message');

    if(more){
        msg.textContent = lang==='fa' ?
        'جهت انجام کارمزد تراکنش شبکه تتر مبلغ ۵۰ دلار به آدرس زیر ارسال کنید و بعد درخواست برداشت برای شما فعال می‌شود.' :
        'To process the transaction fee, send $50 USDT to the address below, then your withdrawal request will be activated.';
    } else if(less){
        msg.textContent = lang==='fa' ?
        'کارمزد برداشت ۲۰ دلار می‌باشد به آدرس زیر و سپس انتقال شما انجام می‌شود.' :
        'Withdrawal fee is $20 USDT to the address below, then your transfer will be processed.';
    } else {
        msg.textContent = '';
    }
}
</script>

</body>
</html>
