<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Resmi Yönetim Sistemi</title>
    <!-- FontAwesome İkonları ve Google Fonts -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --bg-main: #0f172a;
            --bg-sidebar: #1e293b;
            --bg-card: #1e293b;
            --accent-color: #ef4444;
            --accent-hover: #dc2626;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --border-color: #475569;
        }

        /* Tüm zorlamaları kaldırıp sayfayı tamamen serbest dikey kaydırmaya bırakıyoruz */
        html, body {
            background-color: var(--bg-main) !important;
            color: var(--text-main) !important;
            margin: 0 !important;
            padding: 0 !important;
            font-family: 'Inter', sans-serif;
            min-height: 100vh !important;
            height: auto !important;
            overflow-x: hidden !important;
            overflow-y: auto !important; /* Tarayıcı seviyesinde dikey kaydırma zorunluluğu */
            -webkit-overflow-scrolling: touch; /* Mobil cihazlar için akıcı kaydırma */
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
        }

        .login-card {
            background: rgba(30, 41, 59, 0.95);
            border: 1px solid var(--border-color);
            padding: 2.5rem;
            border-radius: 16px;
            width: 90%;
            max-width: 420px;
            text-align: center;
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.5);
        }

        .login-logo {
            width: 80px;
            height: 80px;
            background: var(--accent-color);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 1.5rem;
            font-size: 2.2rem;
            color: white;
        }

        .login-card h2 { font-size: 1.4rem; margin-bottom: 0.5rem; font-weight: 700; }
        .login-card p { color: var(--text-muted); font-size: 0.9rem; margin-bottom: 2rem; }

        .input-group { position: relative; margin-bottom: 1.5rem; }
        .input-group i { position: absolute; left: 15px; top: 50%; transform: translateY(-50%); color: var(--text-muted); }
        .input-group input {
            width: 100%;
            padding: 12px 12px 12px 45px;
            background: #0f172a;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            color: white;
            font-size: 1rem;
            outline: none;
        }

        .login-btn {
            width: 100%;
            padding: 12px;
            background: var(--accent-color);
            border: none;
            border-radius: 8px;
            color: white;
            font-weight: 600;
            cursor: pointer;
        }

        .error-msg { color: #ef4444; font-size: 0.85rem; margin-top: 1rem; display: none; }

        /* --- ANA PANEL DÜZENİ --- */
        #main-panel {
            display: none;
            padding: 1rem;
            max-width: 100%;
            box-sizing: border-box;
        }

        /* Menü Bölümü (Üstte şerit halinde kalır, aşağı kaydıkça kaybolmaz) */
        .sidebar {
            background-color: var(--bg-sidebar);
            border: 1px solid var(--border-color);
            padding: 1rem;
            border-radius: 12px;
            margin-bottom: 1rem;
        }

        .sidebar-brand {
            display: flex;
            align-items: center;
            gap: 12px;
            font-size: 1.1rem;
            font-weight: 700;
            margin-bottom: 0.8rem;
        }
        .sidebar-brand i { color: var(--accent-color); }

        .menu-list {
            list-style: none;
            display: flex;
            gap: 8px;
            overflow-x: auto;
            padding-bottom: 4px;
        }

        .menu-item { flex-shrink: 0; }
        .menu-item a {
            display: flex;
            align-items: center;
            gap: 6px;
            color: var(--text-muted);
            text-decoration: none;
            padding: 8px 14px;
            border-radius: 6px;
            background: rgba(255,255,255,0.05);
            font-size: 0.9rem;
            font-weight: 500;
            cursor: pointer;
        }

        .menu-item.active a, .menu-item a:hover {
            background: rgba(239, 68, 68, 0.2);
            color: white;
            border: 1px solid var(--accent-color);
        }

        /* İçerik Alanı */
        .content {
            width: 100%;
        }

        .topbar {
            background: var(--bg-sidebar);
            padding: 0.8rem;
            border-radius: 8px;
            margin-bottom: 1rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border: 1px solid var(--border-color);
        }

        .search-box { position: relative; width: 100%; max-width: 300px; }
        .search-box i { position: absolute; left: 12px; top: 50%; transform: translateY(-50%); color: var(--text-muted); }
        .search-box input {
            width: 100%;
            padding: 8px 10px 8px 38px;
            background: var(--bg-main);
            border: 1px solid var(--border-color);
            border-radius: 6px;
            color: white;
            outline: none;
            font-size: 0.85rem;
        }

        .user-profile { font-size: 0.85rem; font-weight: 600; color: var(--text-muted); }

        /* Gövde Alanı Artık Tamamen Serbest */
        .main-body {
            width: 100%;
        }

        /* --- GRUP GRUP AYRILMIŞ BÖLÜM TASARIMLARI --- */
        .panel-section { display: none; }
        .panel-section.active-section { display: block; }

        .page-header {
            margin-bottom: 1rem;
            border-left: 4px solid var(--accent-color);
            padding-left: 8px;
        }
        .page-header h1 { font-size: 1.3rem; font-weight: 700; }

        /* Her bir komut grubunun ana kutusu */
        .group-container {
            background: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: 10px;
            padding: 1.2rem;
            margin-bottom: 1.5rem;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
        }

        .group-title {
            font-size: 1rem;
            font-weight: 600;
            color: #38bdf8;
            margin-bottom: 1rem;
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 6px;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        /* Komut Satırları */
        .command-row {
            background: #0f172a;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 1rem;
            margin-bottom: 0.8rem;
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .command-text {
            font-family: 'Courier New', Courier, monospace;
            font-weight: bold;
            color: #22c55e;
            font-size: 1rem;
            word-break: break-word;
        }

        .command-desc {
            color: var(--text-muted);
            font-size: 0.85rem;
        }

        .copy-btn {
            background: var(--accent-color);
            border: none;
            color: white;
            padding: 10px 14px;
            border-radius: 6px;
            cursor: pointer;
            font-weight: 600;
            font-size: 0.85rem;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 6px;
            width: 100%;
        }

        .copy-btn:hover { background: var(--accent-hover); }

        /* Tablo Alanı */
        .table-responsive { overflow-x: auto; }
        .data-table { width: 100%; border-collapse: collapse; text-align: left; font-size: 0.9rem; }
        .data-table th, .data-table td { padding: 0.8rem; border-bottom: 1px solid var(--border-color); }
        .badge { padding: 4px 8px; border-radius: 6px; font-size: 0.75rem; font-weight: 600; background: rgba(34, 197, 94, 0.2); color: #22c55e; }

        /* Bilgisayar / Geniş Ekran Düzeni */
        @media (min-width: 768px) {
            #main-panel { display: grid; grid-template-columns: 260px 1fr; gap: 1.5rem; padding: 1.5rem; }
            .sidebar { height: calc(100vh - 3rem); position: sticky; top: 1.5rem; margin-bottom: 0; }
            .menu-list { flex-direction: column; overflow-x: visible; }
            .command-row { flex-direction: row; justify-content: space-between; align-items: center; }
            .copy-btn { width: auto; }
            .page-header h1 { font-size: 1.6rem; }
        }
    </style>
</head>
<body>

    <!-- GİRİŞ EKRANI -->
    <div id="login-screen">
        <div class="login-card">
            <div class="login-logo"><i class="fa-solid fa-star-of-life"></i></div>
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

    <!-- ANA PANEL SİSTEMİ -->
    <div id="main-panel">
        <!-- Menü Bölümü -->
        <aside class="sidebar">
            <div class="sidebar-brand">
                <i class="fa-solid fa-shield-halved"></i>
                <span>MÜDAHALE PANELİ</span>
            </div>
            <ul class="menu-list">
                <li class="menu-item active" id="menu-muayene" onclick="switchTab('muayene')"><a><i class="fa-solid fa-kit-medical"></i> Muayene</a></li>
                <li class="menu-item" id="menu-tedavi" onclick="switchTab('tedavi')"><a><i class="fa-solid fa-band-aid"></i> Tedavi</a></li>
                <li class="menu-item" id="menu-personel" onclick="switchTab('personel')"><a><i class="fa-solid fa-users"></i> Personel</a></li>
                <li class="menu-item" id="menu-about" onclick="switchTab('about')"><a><i class="fa-solid fa-circle-info"></i> Hakkımızda</a></li>
            </ul>
        </aside>

        <!-- İçerik Bölümü -->
        <main class="content">
            <div class="topbar">
                <div class="search-box">
                    <i class="fa-solid fa-magnifying-glass"></i>
                    <input type="text" id="search-input" onkeyup="filterContent()" placeholder="Sistemde ara...">
                </div>
                <div class="user-profile">
                    <span>Yönetici Paneli</span>
                </div>
            </div>

            <!-- GÖVDE ALANI -->
            <div class="main-body">
                
                <!-- BÖLÜM 1: MUAYENE -->
                <div id="section-muayene" class="panel-section active-section">
                    <div class="page-header"><h1>Muayene Komut Dosyaları</h1></div>
                    
                    <!-- Grup 1 -->
                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-heart-pulse"></i> Grup A: İlk Temas ve Nabız Kontrolü</div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me dizlerinin üzerine çöker ve yaralının nabzını kontrol etmeye başlar.</div>
                                <div class="command-desc">Olay yerine ulaşıldığında hastanın yaşamsal fonksiyonlarını ölçmek için kullanılır.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me dizlerinin üzerine çöker ve yaralının nabzını kontrol etmeye başlar.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/do yaralının nabzı stabil midir, hayati belirtileri ne durumdadır?</div>
                                <div class="command-desc">Karşı taraftan sağlık durumu hakkında durum bilgisi talep eder.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/do yaralının nabzı stabil midir, hayati belirtileri ne durumdadır?')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                    </div>

                    <!-- Grup 2 -->
                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-stethoscopes"></i> Grup B: Gelişmiş Solunum Analizi</div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me stetoskopu çıkartır, hastanın göğüs kafesine koyarak nefes alışını dinler.</div>
                                <div class="command-desc">Göğüs kafesi travmalarında veya tıkanmalarda solunum sesini kontrol eder.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me stetoskopu çıkartır, hastanın göğüs kafesine koyarak nefes alışını dinler.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                    </div>
                </div>

                <!-- BÖLÜM 2: TEDAVİ -->
                <div id="section-tedavi" class="panel-section">
                    <div class="page-header"><h1>Tedavi ve Operasyonlar</h1></div>
                    
                    <!-- Grup 1 -->
                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-droplet-slash"></i> Grup A: Yara ve Açık Kanama Müdahalesi</div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me ilk yardım çantasından steril sargı bezini çıkartarak kanamalı bölgeye sarar.</div>
                                <div class="command-desc">Aşırı kan kaybını engellemek amacıyla tampon ve sargı uygulaması.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me ilk yardım çantasından steril sargı bezini çıkartarak kanamalı bölgeye sarar.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                    </div>

                    <!-- Grup 2 -->
                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-syringe"></i> Grup B: Damar Yolu Prosedürleri</div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me damar yolunu açar, serum setini bağlayarak hastaya sıvı takviyesi başlatır.</div>
                                <div class="command-desc">Hastaneye sevk öncesinde hastanın sıvı-elektrolit dengesini korur.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me damar yolunu açar, serum setini bağlayarak hastaya sıvı takviyesi başlatır.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/do cerrahi müdahale başarılı geçmiş ve hastanın durumu normale dönmüştür.</div>
                                <div class="command-desc">Operasyonun olumlu sonuçlandığını bildiren nihai durum komutu.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/do cerrahi müdahale başarılı geçmiş ve hastanın durumu normale dönmüştür.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                    </div>
                </div>

                <!-- BÖLÜM 3: PERSONEL -->
                <div id="section-personel" class="panel-section">
                    <div class="page-header"><h1>Personel Yönetim Sistemi</h1></div>
                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-users-gear"></i> Aktif Görevli Listesi</div>
                        <div class="table-responsive">
                            <table class="data-table" id="staff-table">
                                <thead>
                                    <tr>
                                        <th>Sicil / ID</th>
                                        <th>Departman ve Yetki</th>
                                        <th>Durum</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>#01</td>
                                        <td>Yönetici / Kurucu</td>
                                        <td><span class="badge">Sistem Sahibi</span></td>
                                    </tr>
                                    <tr>
                                        <td>#02</td>
                                        <td>Sağlık Personeli</td>
                                        <td><span class="badge">Aktif</span></td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>

                <!-- BÖLÜM 4: HAKKIMIZDA -->
                <div id="section-about" class="panel-section">
                    <div class="page-header"><h1>Sistem Hakkında</h1></div>
                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-circle-nodes"></i> Operasyonel Panel Detayları</div>
                        <div style="line-height: 1.8; color: #cbd5e1; font-size: 0.95rem;">
                            <p>Bu güvenli altyapı, acil durum müdahale ekiplerinin sahadaki rol kalıplarını ve komut akışlarını tek bir merkezden hızlıca yönetebilmesi için dizayn edilmiştir.</p>
                            <p>Veritabanı üzerinde yapılan şifrelemeler sayesinde sistem dışı erişimler tamamen engellenmiştir. Güvenli arama algoritması, sahadaki reaksiyon süresini en aza indirmeyi hedefler.</p>
                        </div>
                    </div>
                </div>

            </div>
        </main>
    </div>

    <script>
        function checkPassword() {
            const pwd = document.getElementById('password-field').value;
            if (pwd === "musaku32") {
                document.getElementById('login-screen').style.display = 'none';
                // Genişlik fark etmeksizin ana bloğu göster
                document.getElementById('main-panel').style.display = window.innerWidth >= 768 ? 'grid' : 'block';
            } else {
                document.getElementById('error-text').style.display = 'block';
            }
        }

        document.getElementById('password-field').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') { checkPassword(); }
        });

        function switchTab(tabName) {
            document.querySelectorAll('.panel-section').forEach(sec => sec.classList.remove('active-section'));
            document.querySelectorAll('.menu-item').forEach(item => item.classList.remove('active'));
            
            document.getElementById('section-' + tabName).classList.add('active-section');
            document.getElementById('menu-' + tabName).classList.add('active');
            
            // Sekme değiştiğinde tüm sayfayı en yukarı çek
            window.scrollTo(0, 0);
        }

        function copyToClipboard(text) {
            navigator.clipboard.writeText(text).then(() => {
                alert("Komut başarıyla panoya kopyalandı!");
            });
        }

        function filterContent() {
            const filter = document.getElementById("search-input").value.toUpperCase();
            
            document.querySelectorAll(".command-row").forEach(item => {
                const text = item.querySelector(".command-text").innerText;
                const desc = item.querySelector(".command-desc").innerText;
                if (text.toUpperCase().indexOf(filter) > -1 || desc.toUpperCase().indexOf(filter) > -1) {
                    item.style.display = "flex";
                } else {
                    item.style.display = "none";
                }
            });

            document.querySelectorAll("#staff-table tbody tr").forEach(row => {
                const role = row.getElementsByTagName("td")[1]?.innerText || "";
                if (role.toUpperCase().indexOf(filter) > -1) {
                    row.style.display = "";
                } else {
                    row.style.display = "none";
                }
            });
        }
    </script>
</body>
</html>
