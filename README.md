<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Resmi Yönetim Sistemi</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --bg-main: #0f172a;
            --bg-sidebar: #1e293b;
            --bg-card: #1e293b;
            --bg-item: #334155;
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
            cursor: pointer;
        }

        .menu-item.active a, .menu-item a:hover {
            background: rgba(239, 68, 68, 0.1);
            color: var(--accent-color);
        }

        .content {
            display: flex;
            flex-direction: column;
            height: 100vh;
            overflow: hidden;
        }

        .topbar {
            background: var(--bg-sidebar);
            padding: 1rem 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid var(--border-color);
            flex-shrink: 0;
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

        .main-body {
            padding: 2rem;
            flex-grow: 1;
            overflow-y: auto;
        }

        .page-header {
            margin-bottom: 2rem;
            border-bottom: 2px solid var(--accent-color);
            padding-bottom: 0.5rem;
        }

        .page-header h1 {
            font-size: 1.8rem;
            font-weight: 700;
            letter-spacing: 0.5px;
        }

        /* --- BÖLÜM VE KUTU DÜZENLEMELERİ --- */
        .section-block {
            margin-bottom: 2.5rem;
        }

        .section-title {
            font-size: 1.1rem;
            font-weight: 600;
            color: var(--text-muted);
            margin-bottom: 1rem;
            text-transform: uppercase;
            letter-spacing: 1px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .data-card {
            background: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 1.5rem;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.2);
        }

        .role-list {
            display: flex;
            flex-direction: column;
            gap: 16px; /* Kutuların aralarını açtık */
        }

        .role-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: var(--bg-main);
            padding: 1.2rem;
            border-radius: 8px;
            border: 1px solid var(--border-color);
            border-left: 5px solid var(--accent-color);
            transition: transform 0.2s;
        }

        .role-item:hover {
            transform: translateX(4px);
            background: #131c2e;
        }

        .role-text {
            font-family: 'Courier New', Courier, monospace;
            font-weight: bold;
            color: #38bdf8;
            font-size: 1.1rem;
        }

        .role-desc {
            color: var(--text-muted);
            font-size: 0.9rem;
            margin-top: 6px;
            font-family: 'Inter', sans-serif;
            font-weight: normal;
        }

        .copy-btn {
            background: var(--accent-color);
            border: none;
            color: white;
            padding: 8px 16px;
            border-radius: 6px;
            cursor: pointer;
            font-weight: 600;
            font-size: 0.85rem;
            transition: background 0.2s;
            display: flex;
            align-items: center;
            gap: 6px;
            flex-shrink: 0;
        }

        .copy-btn:hover {
            background: var(--accent-hover);
        }

        .panel-section {
            display: none;
        }

        .panel-section.active-section {
            display: block;
        }

        /* Tablo Stilleri */
        .data-table {
            width: 100%;
            border-collapse: collapse;
            text-align: left;
        }

        .data-table th, .data-table td {
            padding: 1.2rem;
            border-bottom: 1px solid var(--border-color);
        }

        .data-table th {
            color: var(--text-muted);
            font-weight: 600;
            font-size: 0.9rem;
            text-transform: uppercase;
        }

        .badge {
            padding: 6px 12px;
            border-radius: 6px;
            font-size: 0.8rem;
            font-weight: 600;
        }
        .badge-success { background: rgba(34, 197, 94, 0.2); color: #22c55e; }
        
        .about-text {
            line-height: 1.8;
            color: #cbd5e1;
            font-size: 1.05rem;
        }
        .about-text p {
            margin-bottom: 1.2rem;
        }
    </style>
</head>
<body>

    <div id="login-screen">
        <div class="login-card">
            <div class="login-logo">
                <i class="fa-solid fa-star-of-life"></i>
            </div>
            <h2>VERİTABANI PANELİ</h2>
            <p>Erişim Sağlamak İçin Yetkili Şifrenizi Girin</p>
            
            <div class="input-group">
                <i class="fa-solid fa-lock"></i>
                <input type="password" id="password-field" placeholder="Erişim Şifresi...">
            </div>
            
            <button class="login-btn" onclick="checkPassword()">Giriş Yap</button>
            <div class="error-msg" id="error-text">Hatalı Şifre! Lütfen tekrar deneyin.</div>
        </div>
    </div>

    <div id="main-panel">
        <aside class="sidebar">
            <div class="sidebar-brand">
                <i class="fa-solid fa-shield-halved"></i>
                <span>MÜDAHALE PANELİ</span>
            </div>
            <ul class="menu-list">
                <li class="menu-item active" id="menu-muayene" onclick="switchTab('muayene')"><a><i class="fa-solid fa-kit-medical"></i> Muayene Komutları</a></li>
                <li class="menu-item" id="menu-tedavi" onclick="switchTab('tedavi')"><a><i class="fa-solid fa-band-aid"></i> Tedavi Komutları</a></li>
                <li class="menu-item" id="menu-personel" onclick="switchTab('personel')"><a><i class="fa-solid fa-users"></i> Personel Listesi</a></li>
                <li class="menu-item" id="menu-about" onclick="switchTab('about')"><a><i class="fa-solid fa-circle-info"></i> Hakkımızda</a></li>
            </ul>
        </aside>

        <main class="content">
            <div class="topbar">
                <div class="search-box">
                    <i class="fa-solid fa-magnifying-glass"></i>
                    <input type="text" id="search-input" onkeyup="filterContent()" placeholder="Sistemde ara...">
                </div>
                <div class="user-profile">
                    <span>Yönetici</span>
                    <div class="user-avatar"><i class="fa-solid fa-user-shield"></i></div>
                </div>
            </div>

            <div class="main-body">
                
                <div id="section-muayene" class="panel-section active-section">
                    <div class="page-header">
                        <h1>Muayene Komutları</h1>
                    </div>
                    
                    <div class="section-block">
                        <div class="section-title"><i class="fa-solid fa-heart-pulse"></i> İlk Kontrol Alanı</div>
                        <div class="data-card">
                            <div class="role-list">
                                <div class="role-item">
                                    <div>
                                        <div class="role-text">/me dizlerinin üzerine çöker ve yaralının nabzını kontrol etmeye başlar.</div>
                                        <div class="role-desc">İlk müdahale esnasında nabız ölçümü rolü.</div>
                                    </div>
                                    <button class="copy-btn" onclick="copyToClipboard('/me dizlerinin üzerine çöker ve yaralının nabzını kontrol etmeye başlar.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                                </div>
                                <div class="role-item">
                                    <div>
                                        <div class="role-text">/do yaralının nabzı stabil midir, hayati belirtileri ne durumdadır?</div>
                                        <div class="role-desc">Yaralının durumunu karşı tarafa sorma amaçlı atılan durum komutu.</div>
                                    </div>
                                    <button class="copy-btn" onclick="copyToClipboard('/do yaralının nabzı stabil midir, hayati belirtileri ne durumdadır?')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="section-block">
                        <div class="section-title"><i class="fa-solid fa-stethoscopes"></i> Solunum ve İleri Muayene</div>
                        <div class="data-card">
                            <div class="role-list">
                                <div class="role-item">
                                    <div>
                                        <div class="role-text">/me stetoskopu çıkartır, hastanın göğüs kafesine koyarak nefes alışını dinler.</div>
                                        <div class="role-desc">Akciğerlerin ve solunum yollarının kontrol edilmesi rolü.</div>
                                    </div>
                                    <button class="copy-btn" onclick="copyToClipboard('/me stetoskopu çıkartır, hastanın göğüs kafesine koyarak nefes alışını dinler.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div id="section-tedavi" class="panel-section">
                    <div class="page-header">
                        <h1>Tedavi ve Müdahale Komutları</h1>
                    </div>
                    
                    <div class="section-block">
                        <div class="section-title"><i class="fa-solid fa-droplet-slash"></i> Kanama ve Yara Müdahalesi</div>
                        <div class="data-card">
                            <div class="role-list">
                                <div class="role-item">
                                    <div>
                                        <div class="role-text">/me ilk yardım çantasından steril sargı bezini çıkartarak kanamalı bölgeye sarar.</div>
                                        <div class="role-desc">Aktif kanamaları durdurma ve pansuman amacıyla kullanılır.</div>
                                    </div>
                                    <button class="copy-btn" onclick="copyToClipboard('/me ilk yardım çantasından steril sargı bezini çıkartarak kanamalı bölgeye sarar.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="section-block">
                        <div class="section-title"><i class="fa-solid fa-syringe"></i> Damar Yolu ve İlaç/Serum Takviyesi</div>
                        <div class="data-card">
                            <div class="role-list">
                                <div class="role-item">
                                    <div>
                                        <div class="role-text">/me damar yolunu açar, serum setini bağlayarak hastaya sıvı takviyesi başlatır.</div>
                                        <div class="role-desc">Klinik veya saha ortamında stabilizasyon için sıvı aktarımı rolü.</div>
                                    </div>
                                    <button class="copy-btn" onclick="copyToClipboard('/me damar yolunu açar, serum setini bağlayarak hastaya sıvı takviyesi başlatır.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="section-block">
                        <div class="section-title"><i class="fa-solid fa-check-double"></i> Operasyon Sonu Durum Belirleme</div>
                        <div class="data-card">
                            <div class="role-list">
                                <div class="role-item">
                                    <div>
                                        <div class="role-text">/do cerrahi müdahale başarılı geçmiş ve hastanın durumu normale dönmüştür.</div>
