<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>EMS DATABASE v9.5</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --bg-main: #0a0a0c;
            --bg-sidebar: #131317;
            --bg-card: #1a1a20;
            --accent-color: #7dd3fc;
            --text-main: #cbd5e1;
            --text-muted: #64748b;
            --border-color: #1e293b;
            --code-bg: #0f172a;
            --code-text: #94a3b8;
        }

        body {
            background-color: var(--bg-main) !important;
            color: var(--text-main) !important;
            font-family: 'Inter', sans-serif;
            margin: 0; padding: 0; height: 100vh; overflow: hidden;
        }

        /* Giriş Ekranı */
        #login-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background-color: var(--bg-main); z-index: 9999;
            display: flex; justify-content: center; align-items: center;
        }
        .login-box {
            background-color: var(--bg-sidebar); padding: 40px; border-radius: 12px;
            border: 1px solid var(--border-color); text-align: center; width: 300px;
        }
        .login-box h1 { color: var(--accent-color); font-size: 16px; margin-bottom: 20px; }
        .login-box input {
            width: 100%; padding: 12px; background: var(--bg-main); border: 1px solid var(--border-color);
            border-radius: 6px; color: white; margin-bottom: 15px; box-sizing: border-box; text-align: center;
        }
        .login-box button {
            width: 100%; padding: 12px; background: var(--accent-color); color: #0a0a0c;
            border: none; border-radius: 6px; font-weight: bold; cursor: pointer;
        }

        /* Ana Panel */
        #main-app { display: none; height: 100vh; grid-template-columns: 300px 1fr; }
        .sidebar { background-color: var(--bg-sidebar); border-right: 1px solid var(--border-color); padding: 20px; overflow-y: auto; }
        .content-area { padding: 40px; overflow-y: auto; }
        .section-card { background-color: var(--bg-card); border-radius: 8px; padding: 25px; margin-bottom: 30px; border: 1px solid var(--border-color); }
        .section-card h2 { color: var(--accent-color); border-bottom: 1px solid var(--border-color); padding-bottom: 10px; font-size: 18px; display: flex; justify-content: space-between; align-items: center; }
        pre { background-color: var(--code-bg); padding: 15px; border-radius: 6px; color: var(--code-text); line-height: 1.6; font-family: 'JetBrains Mono'; white-space: pre-wrap; }
        .card-copy-btn { background: rgba(125, 211, 252, 0.1); border: 1px solid var(--accent-color); color: var(--accent-color); padding: 4px 10px; border-radius: 4px; cursor: pointer; font-size: 12px; }
    </style>
</head>
<body>

    <div id="login-overlay">
        <div class="login-box">
            <h1>EMS SİSTEM GİRİŞİ</h1>
            <input type="password" id="password-field" placeholder="Şifre" onkeydown="if(event.key === 'Enter') checkPassword()">
            <button onclick="checkPassword()">YETKİLENDİR</button>
        </div>
    </div>

    <div id="main-app">
        <div class="sidebar">
            <h3 style="color: var(--accent-color)">EMS DATABASE v9.5</h3>
            <div style="color: var(--text-muted); font-size: 13px;">31 Protokol Erişim Yetkisi.</div>
        </div>
        <div class="content-area" id="content">
            <div id="sec1" class="section-card">
                <h2>1. Olay Yeri Giriş <button class="card-copy-btn" onclick="copyText(this)">Kopyala</button></h2>
                <pre>/me İlk yardım çantasını hazırlar, çevre güvenliğini kontrol eder.</pre>
            </div>
            
            <div id="sec31" class="section-card">
                <h2>31. Klinik Ölüm <button class="card-copy-btn" onclick="copyText(this)">Kopyala</button></h2>
                <pre>/do Yapılan tüm müdahalelere rağmen hastadan yanıt alınamadı.
/me Ölüm saati: [SAAT] olarak not düşer.</pre>
            </div>
        </div>
    </div>

    <script>
        const CORRECT_PASSWORD = "musa32"; // Yeni şifre burada

        function checkPassword() {
            const inputField = document.getElementById("password-field");
            if (inputField.value === CORRECT_PASSWORD) {
                document.getElementById("login-overlay").style.display = "none";
                document.getElementById("main-app").style.display = "grid";
            } else {
                inputField.value = "";
                alert("Hatalı Şifre!");
            }
        }

        function copyText(btn) {
            const text = btn.closest('.section-card').querySelector('pre').innerText;
            navigator.clipboard.writeText(text);
            btn.innerText = "Kopyalandı!";
            setTimeout(() => btn.innerText = "Kopyala", 2000);
        }
    </script>
</body>
</html>
