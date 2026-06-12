<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>USMS & EMS Resmi Yönetim Sistemi</title>
    <!-- FontAwesome İkonları ve Google Fonts -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --bg-main: #0f172a;
            --bg-sidebar: #1e293b;
            --bg-card: #334155;
            --accent-color: #ef4444; /* EMS Kırmızısı */
            --accent-hover: #dc2626;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --border-color: #475569;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif;
        }

        body {
            background-color: var(--bg-main);
            color: var(--text-main);
            height: 100vh;
            overflow: hidden;
        }

        /* --- GİRİŞ EKRANI --- */
        #login-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, #0f172a 0%, #1e1b4b 100%);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 9999;
            transition: all 0.5s ease;
        }

        .login-card {
            background: rgba(30, 41, 59, 0.7);
            backdrop-filter: blur(16px);
            border: 1px solid var(--border-color);
            padding: 2.5rem;
            border-radius: 16px;
            width: 100%;
            max-width: 420px;
            text-align: center;
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.5);
        }

        .login-logo {
            width: 90px;
            height: 90px;
            background: var(--accent-color);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 1.5rem;
            font-size: 2.5rem;
            color: white;
            box-shadow: 0 0 20px rgba(239, 68, 68, 0.4);
        }

        .login-card h2 {
            font-size: 1.5rem;
            margin-bottom: 0.5rem;
            font-weight: 700;
            letter-spacing: 0.5px;
        }

        .login-card p {
            color: var(--text-muted);
            font-size: 0.9rem;
            margin-bottom: 2rem;
        }

        .input-group {
            position: relative;
            margin-bottom: 1.5rem;
        }

        .input-group i {
            position: absolute;
            left: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: var(--text-muted);
        }

        .input-group input {
            width: 100%;
            padding: 12px 12px 12px 45px;
            background: #0f172a;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            color: white;
            font-size: 1rem;
            outline: none;
            transition: all 0.3s;
        }

        .input-group input:focus {
            border-color: var(--accent-color);
            box-shadow: 0 0 0 2px rgba(239, 68, 68, 0.2);
        }

        .login-btn {
            width: 100%;
            padding: 12px;
            background: var(--accent-color);
            border: none;
            border-radius: 8px;
            color: white;
            font-weight: 600;
            font-size: 1rem;
            cursor: pointer;
            transition: background 0.3s;
        }

        .login-btn:hover {
            background: var(--accent-hover);
        }

        .error-msg {
            color: #ef4444;
            font-size: 0.85rem;
            margin-top: 1rem;
            display: none;
        }

        /* --- ANA PANEL SİSTEMİ --- */
        #main-panel {
            display: none;
            height: 100vh;
            grid-template-columns: 260px 1fr;
        }

        /* Sol Menü (Sidebar) */
        .sidebar {
            background-color: var(--bg-sidebar);
            border-right: 1px solid var(--border-color);
            display: flex;
            flex-direction: column;
            padding: 1.5rem;
        }

        .sidebar-brand {
            display: flex;
            align-items: center;
            gap: 12px;
            font-size: 1.2rem;
            font-weight: 700;
            padding-bottom: 1.5rem;
            border-bottom: 1px solid var(--border-color);
            margin-bottom: 1.5rem;
        }

        .sidebar-brand i {
            color: var(--accent-color);
        }

        .menu-list {
            list-style: none;
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        .menu-item a {
            display: flex;
            align-items: center;
            gap: 12px;
            color: var(--text-muted);
            text-decoration: none;
            padding: 12px;
            border-radius: 8px;
            font-weight: 500;
            transition: all 0.2s;
        }

        .menu-item.active a, .menu-item a:hover {
            background: rgba(239, 68, 68, 0.1);
            color: var(--accent-color);
        }

        /* Sağ İçerik Alanı */
        .content {
            display: flex;
            flex-direction: column;
            height: 100vh;
            overflow-y: auto;
        }

        /* Üst Bar (Topbar) */
        .topbar {
            background: var(--bg-sidebar);
            padding: 1rem 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid var(--border-color);
        }

        .search-box {
            position: relative;
            width: 350px;
        }

        .search-box i {
            position: absolute;
            left: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: var(--text-muted);
        }

        .search-box input {
            width: 100%;
            padding: 10px 10px 10px 40px;
            background: var(--bg-main);
            border: 1px solid var(--border-color);
            border-radius: 20px;
            color: white;
            outline: none;
            font-size: 0.9rem;
        }

        .user-profile {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .user-avatar {
            width: 35px;
            height: 35px;
            background: #475569;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 600;
        }

        /* Ana Veri Tablosu ve Kartlar */
        .main-body {
            padding: 2rem;
        }

        .page-header {
            margin-bottom: 1.5rem;
        }

        .page-header h1 {
            font-size: 1.8rem;
            font-weight: 600;
        }

        .data-card {
            background: var(--bg-sidebar);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 1.5rem;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
        }

        .data-table {
            width: 100%;
            border-collapse: collapse;
            text-align: left;
        }

        .data-table th, .data-table td {
            padding: 1rem;
            border-bottom: 1px solid var(--border-color);
        }

        .data-table th {
            color: var(--text-muted);
            font-weight: 600;
            font-size: 0.9rem;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .data-table tbody tr:hover {
            background: rgba(255, 255, 255, 0.02);
        }

        .badge {
            padding: 4px 8px;
            border-radius: 6px;
            font-size: 0.8rem;
            font-weight: 600;
        }

        .badge-success { background: rgba(34, 197, 94, 0.2); color: #22c55e; }
        .badge-danger { background: rgba(239, 68, 68, 0.2); color: #ef4444; }
    </style>
</head>
<body>

    <!-- 1. GİRİŞ EKRANI -->
    <div id="login-screen">
        <div class="login-card">
            <div class="login-logo">
                <i class="fa-solid Mount fa-star-of-life"></i>
            </div>
            <h2>YÖNETİM SİSTEMİ</h2>
            <p>Devlet Hastanesi Personel ve Veri Paneli</p>
            
            <div class="input-group">
                <i class="fa-solid fa-lock"></i>
                <input type="password" id="password-field" placeholder="Erişim Şifresini Girin...">
            </div>
            
            <button class="login-btn" onclick="checkPassword()">Sisteme Giriş Yap</button>
            <div class="error-msg" id="error-text">Hatalı Şifre! Lütfen tekrar deneyin.</div>
        </div>
    </div>

    <!-- 2. ANA PANEL SİSTEMİ (Giriş Sonrası) -->
    <div id="main-panel">
        <!-- Sol Menü -->
        <aside class="sidebar">
            <div class="sidebar-brand">
                <i class="fa-solid fa-shield-halved"></i>
                <span>USMS & EMS PANEL</span>
            </div>
            <ul class="menu-list">
                <li class="menu-item active"><a href="#"><i class="fa-solid fa-database"></i> Ana Veritabanı</a></li>
                <li class="menu-item"><a href="#"><i class="fa-solid fa-users"></i> Personel Listesi</a></li>
                <li class="menu-item"><a href="#"><i class="fa-solid fa-file-medical"></i> Sertifikalar</a></li>
                <li class="menu-item"><a href="#"><i class="fa-solid fa-calendar-days"></i> Nöbet Çizelgesi</a></li>
            </ul>
        </aside>

        <!-- Sağ İçerik -->
        <main class="content">
            <!-- Üst Bar -->
            <div class="topbar">
                <div class="search-box">
                    <i class="fa-solid fa-magnifying-glass"></i>
                    <input type="text" id="search-input" onkeyup="filterTable()" placeholder="Sistemde isim veya veri ara...">
                </div>
                <div class="user-profile">
                    <span>Musa Akdoğan</span>
                    <div class="user-avatar">M</div>
                </div>
            </div>

            <!-- Sayfa İçeriği -->
            <div class="main-body">
                <div class="page-header">
                    <h1>Mevcut Veritabanı Kayıtları</h1>
                </div>
                
                <div class="data-card">
                    <table class="data-table" id="data-table">
                        <thead>
                            <tr>
                                <th>ID</th>
                                <th>Personel Adı</th>
                                <th>Rütbe / Görev</th>
                                <th>Durum</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>#001</td>
                                <td>Ahmet Yılmaz</td>
                                <td>Paramedik</td>
                                <td><span class="badge badge-success">Aktif Nöbette</span></td>
                            </tr>
                            <tr>
                                <td>#002</td>
                                <td>Mehmet Demir</td>
                                <td>Stajyer</td>
                                <td><span class="badge badge-success">Aktif Nöbette</span></td>
                            </tr>
                            <tr>
                                <td>#003</td>
                                <td>Can Tekin</td>
                                <td>Doktor</td>
                                <td><span class="badge badge-danger">İzinli</span></td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </main>
    </div>

    <script>
        // Şifre Kontrolü
        function checkPassword() {
            const passwordInput = document.getElementById('password-field').value;
            const errorText = document.getElementById('error-text');
            
            // Senin şifren
            if (passwordInput === "musaku32") {
                document.getElementById('login-screen').style.opacity = '0';
                setTimeout(() => {
                    document.getElementById('login-screen').style.display = 'none';
                    document.getElementById('main-panel').style.display = 'grid';
                }, 500);
            } else {
                errorText.style.display = 'block';
            }
        }

        // Klavye ile Giriş Desteği (Enter)
        document.getElementById('password-field').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                checkPassword();
            }
        });

        // Canlı Arama Kutusu Filtreleme Fonksiyonu
        function filterTable() {
            const input = document.getElementById("search-input");
            const filter = input.value.toUpperCase();
            const table = document.getElementById("data-table");
            const tr = table.getElementsByTagName("tr");

            for (let i = 1; i < tr.length; i++) {
                let tdName = tr[i].getElementsByTagName("td")[1];
                let tdRole = tr[i].getElementsByTagName("td")[2];
                if (tdName || tdRole) {
                    let txtValueName = tdName.textContent || tdName.innerText;
                    let txtValueRole = tdRole.textContent || tdRole.innerText;
                    if (txtValueName.toUpperCase().indexOf(filter) > -1 || txtValueRole.toUpperCase().indexOf(filter) > -1) {
                        tr[i].style.display = "";
                    } else {
                        tr[i].style.display = "none";
                    }
                }       
            }
        }
    </script>
</body>
</html>
