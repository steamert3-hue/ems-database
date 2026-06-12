<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Resmi Yönetim Sistemi</title>
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

        /* Akıcı dikey kaydırma için ana gövde ayarları */
        html, body {
            background-color: var(--bg-main) !important;
            color: var(--text-main) !important;
            margin: 0 !important;
            padding: 0 !important;
            font-family: 'Inter', sans-serif;
            min-height: 100vh !important;
            overflow-x: hidden !important;
            overflow-y: auto !important;
            -webkit-overflow-scrolling: touch;
        }

        /* --- GİRİŞ EKRANI --- */
        #login-screen {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: linear-gradient(135deg, #0f172a 0%, #1e1b4b 100%);
            display: flex; justify-content: center; align-items: center; z-index: 9999;
        }

        .login-card {
            background: rgba(30, 41, 59, 0.95); border: 1px solid var(--border-color);
            padding: 2.5rem; border-radius: 16px; width: 90%; max-width: 420px; text-align: center;
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.5);
        }

        .login-logo {
            width: 80px; height: 80px; background: var(--accent-color); border-radius: 50%;
            display: flex; align-items: center; justify-content: center; margin: 0 auto 1.5rem;
            font-size: 2.2rem; color: white;
        }

        .input-group { position: relative; margin-bottom: 1.5rem; }
        .input-group i { position: absolute; left: 15px; top: 50%; transform: translateY(-50%); color: var(--text-muted); }
        .input-group input {
            width: 100%; padding: 12px 12px 12px 45px; background: #0f172a;
            border: 1px solid var(--border-color); border-radius: 8px; color: white; outline: none;
        }

        .login-btn {
            width: 100%; padding: 12px; background: var(--accent-color); border: none;
            border-radius: 8px; color: white; font-weight: 600; cursor: pointer;
        }

        .error-msg { color: #ef4444; font-size: 0.85rem; margin-top: 1rem; display: none; }

        /* --- PANEL TASARIMI --- */
        #main-panel { display: none; padding: 1rem; }

        .sidebar {
            background-color: var(--bg-sidebar); border: 1px solid var(--border-color);
            padding: 1rem; border-radius: 12px; margin-bottom: 1rem;
        }

        .sidebar-brand { display: flex; align-items: center; gap: 12px; font-size: 1.1rem; font-weight: 700; margin-bottom: 0.8rem; }
        .sidebar-brand i { color: var(--accent-color); }

        .menu-list { list-style: none; display: flex; gap: 8px; overflow-x: auto; padding-bottom: 4px; }
        .menu-item a {
            display: flex; align-items: center; gap: 6px; color: var(--text-muted); text-decoration: none;
            padding: 8px 14px; border-radius: 6px; background: rgba(255,255,255,0.05); font-size: 0.9rem; font-weight: 500; cursor: pointer;
        }

        .menu-item.active a, .menu-item a:hover {
            background: rgba(239, 68, 68, 0.2); color: white; border: 1px solid var(--accent-color);
        }

        .topbar {
            background: var(--bg-sidebar); padding: 0.8rem; border-radius: 8px; margin-bottom: 1rem;
            display: flex; justify-content: space-between; align-items: center; border: 1px solid var(--border-color);
        }

        .search-box { position: relative; width: 100%; max-width: 300px; }
        .search-box i { position: absolute; left: 12px; top: 50%; transform: translateY(-50%); color: var(--text-muted); }
        .search-box input {
            width: 100%; padding: 8px 10px 8px 38px; background: var(--bg-main);
            border: 1px solid var(--border-color); border-radius: 6px; color: white; outline: none; font-size: 0.85rem;
        }

        .panel-section { display: none; }
        .panel-section.active-section { display: block; }

        .page-header { margin-bottom: 1rem; border-left: 4px solid var(--accent-color); padding-left: 8px; }
        .page-header h1 { font-size: 1.3rem; font-weight: 700; }

        /* Gruplama Kutuları */
        .group-container {
            background: var(--bg-card); border: 1px solid var(--border-color);
            border-radius: 10px; padding: 1.2rem; margin-bottom: 1.5rem;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
        }

        .group-title {
            font-size: 1rem; font-weight: 600; color: #38bdf8; margin-bottom: 1rem;
            border-bottom: 1px solid var(--border-color); padding-bottom: 6px;
            display: flex; align-items: center; gap: 6px;
        }

        /* Komut Kartları */
        .command-row {
            background: #0f172a; border: 1px solid var(--border-color);
            border-radius: 8px; padding: 1rem; margin-bottom: 0.8rem;
            display: flex; flex-direction: column; gap: 10px;
        }

        .command-text { font-family: 'Courier New', Courier, monospace; font-weight: bold; color: #22c55e; font-size: 1rem; word-break: break-word; }
        .command-desc { color: var(--text-muted); font-size: 0.85rem; }

        .copy-btn {
            background: var(--accent-color); border: none; color: white;
            padding: 10px 14px; border-radius: 6px; cursor: pointer;
            font-weight: 600; font-size: 0.85rem; display: flex; align-items: center; justify-content: center; gap: 6px; width: 100%;
        }
        .copy-btn:hover { background: var(--accent-hover); }

        .table-responsive { overflow-x: auto; }
        .data-table { width: 100%; border-collapse: collapse; text-align: left; font-size: 0.9rem; }
        .data-table th, .data-table td { padding: 0.8rem; border-bottom: 1px solid var(--border-color); }
        .badge { padding: 4px 8px; border-radius: 6px; font-size: 0.75rem; font-weight: 600; background: rgba(34, 197, 94, 0.2); color: #22c55e; }

        /* Masaüstü Ekran Modu */
        @media (min-width: 768px) {
            #main-panel { display: grid; grid-template-columns: 260px 1fr; gap: 1.5rem; padding: 1.5rem; }
            .sidebar { height: calc(100vh - 3rem); position: sticky; top: 1.5rem; margin-bottom: 0; }
            .menu-list { flex-direction: column; }
            .command-row { flex-direction: row; justify-content: space-between; align-items: center; }
            .copy-btn { width: auto; }
            .page-header h1 { font-size: 1.6rem; }
        }
    </style>
</head>
<body>

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

    <div id="main-panel">
        <aside class="sidebar">
            <div class="sidebar-brand"><i class="fa-solid fa-shield-halved"></i> <span>MÜDAHALE PANELİ</span></div>
            <ul class="menu-list">
                <li class="menu-item active" id="menu-muayene" onclick="switchTab('muayene')"><a><i class="fa-solid fa-kit-medical"></i> Muayene</a></li>
                <li class="menu-item" id="menu-tedavi" onclick="switchTab('tedavi')"><a><i class="fa-solid fa-band-aid"></i> Tedavi</a></li>
                <li class="menu-item" id="menu-personel" onclick="switchTab('personel')"><a><i class="fa-solid fa-users"></i> Personel</a></li>
                <li class="menu-item" id="menu-about" onclick="switchTab('about')"><a><i class="fa-solid fa-circle-info"></i> Hakkımızda</a></li>
            </ul>
        </aside>

        <main class="content">
            <div class="topbar">
                <div class="search-box"><i class="fa-solid fa-magnifying-glass"></i> <input type="text" id="search-input" onkeyup="filterContent()" placeholder="Sistemde ara..."></div>
                <div class="user-profile"><span>Yönetici Paneli</span></div>
            </div>

            <div class="main-body">
                
                <div id="section-muayene" class="panel-section active-section">
                    <div class="page-header"><h1>Muayene Komut Dosyaları</h1></div>
                    
                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-heart-pulse"></i> Grup A: Bilinç ve Yaşamsal Değer Kontrolü</div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me dizlerinin üzerine çöker, yaralının omuzlarından sarsarak "Beni duyuyor musunuz?" der.</div>
                                <div class="command-desc">Olay yerine ulaşıldığında ilk bilinç kontrolü.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me dizlerinin üzerine çöker, yaralının omuzlarından sarsarak \"Beni duyuyor musunuz?\" der.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/do yaralının bilinci yerinde midir, herhangi bir tepki veriyor mu?</div>
                                <div class="command-desc">Karşı taraftan bilinç durumunu sorgular.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/do yaralının bilinci yerinde midir, herhangi bir tepki veriyor mu?')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me sağ elinin işaret ve orta parmağını hastanın şah damarına bastırarak nabzını ölçmeye başlar.</div>
                                <div class="command-desc">Nabız ölçümünü başlatan rol.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me sağ elinin işaret ve orta parmağını hastanın şah damarına bastırarak nabzını ölçmeye başlar.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/do şah damarından alınan nabız (Dakikada kaç atıyor) ve genel durumu nasıldır?</div>
                                <div class="command-desc">Nabız değerini öğrenmek amacıyla sorulan durum sorusu.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/do şah damarından alınan nabız (Dakikada kaç atıyor) ve genel durumu nasıldır?')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                    </div>

                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-stethoscopes"></i> Grup B: Göğüs ve Solunum Analizi</div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me kulağını hastanın ağzına yaklaştırır, gözleriyle göğüs kafesinin inip kalkışını izler (Bak-Dinle-Hisset).</div>
                                <div class="command-desc">Temel solunum kontrolü uygulaması.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me kulağını hastanın ağzına yaklaştırır, gözleriyle göğüs kafesinin inip kalkışını izler (Bak-Dinle-Hisset).')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/do hastanın solunumu var mıdır, nefes alıp vermede zorlanma gözleniyor mu?</div>
                                <div class="command-desc">Solunumun varlığını test eden soru.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/do hastanın solunumu var mıdır, nefes alıp vermede zorlanma gözleniyor mu?')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me medikal çantadan stetoskopu çıkarıp kulaklığı takar, diyaframı hastanın göğsüne koyarak akciğerleri dinler.</div>
                                <div class="command-desc">Akciğer seslerini dinlemek için ileri muayene rolü.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me medikal çantadan stetoskopu çıkarıp kulaklığı takar, diyaframı hastanın göğsüne koyarak akciğerleri dinler.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/do stetoskop ile dinlenen akciğerlerden hırıltı veya anormal bir ses geliyor mu?</div>
                                <div class="command-desc">İç kanama veya tıkanma ihtimaline karşı durum sorusu.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/do stetoskop ile dinlenen akciğerlerden hırıltı veya anormal bir ses geliyor mu?')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                    </div>

                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-eye"></i> Grup C: Göz Bebekleri ve Kafa Travması Kontrolü</div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me cebinden muayene fenerini çıkartır, hastanın göz kapaklarını aralayarak ışık tutar.</div>
                                <div class="command-desc">Işık refleksi kontrol prosedürü.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me cebinden muayene fenerini çıkartır, hastanın göz kapaklarını aralayarak ışık tutar.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/do göz bebeklerinin ışığa tepkisi nasıldır? (Büyüme/Küçülme veya Anizokori var mı?)</div>
                                <div class="command-desc">Nörolojik hasar tespiti için durum sorusu.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/do göz bebeklerinin ışığa tepkisi nasıldır? (Büyüme/Küçülme veya Anizokori var mı?)')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                    </div>
                </div>

                <div id="section-tedavi" class="panel-section">
                    <div class="page-header"><h1>Tedavi ve Operasyonlar</h1></div>
                    
                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-droplet-slash"></i> Grup A: Yara ve Açık Kanama Müdahalesi</div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me çantasından steril gazlı bezleri çıkarıp kanamalı bölgeye yerleştirir ve baskı uygulamaya başlar.</div>
                                <div class="command-desc">Aktif kanamaya tampon uygulama rolü.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me çantasından steril gazlı bezleri çıkarıp kanamalı bölgeye yerleştirir ve baskı uygulamaya başlar.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/do kanama uygulanan baskı neticesinde durmuş veya yavaşlamış mıdır?</div>
                                <div class="command-desc">Tamponun başarısını ölçen durum sorusu.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/do kanama uygulanan baskı neticesinde durmuş veya yavaşlamış mıdır?')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me rulo sargı bezini alarak yaralı bölgeyi sıkıca sarar, düğüm atarak sabitler.</div>
                                <div class="command-desc">Bandajlama ve sabitleme aşaması.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me rulo sargı bezini alarak yaralı bölgeyi sıkıca sarar, düğüm atarak sabitler.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                    </div>

                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-syringe"></i> Grup B: Damar Yolu ve İlaç Prosedürleri</div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me turnikeyi hastanın koluna bağlar, alkollü pamuk ile damar hattını silerek sterilize eder.</div>
                                <div class="command-desc">Damar yolu hazırlık aşaması.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me turnikeyi hastanın koluna bağlar, alkollü pamuk ile damar hattını silerek sterilize eder.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me uygun boyuttaki intraketi (branül) damara paralel açıyla batırarak damar yolunu açar.</div>
                                <div class="command-desc">Damara girme anı rolü.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me uygun boyuttaki intraketi (branül) damara paralel açıyla batırarak damar yolunu açar.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/do intraketin arkasından kan gelmiş midir, damar yolu başarıyla açılmış mıdır?</div>
                                <div class="command-desc">Damar hattının doğruluğunu sorgulayan /do sorusu.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/do intraketin arkasından kan gelmiş midir, damar yolu başarıyla açılmış mıdır?')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me serum setini intrakete bağlar, mandallı vanayı açarak sıvı akışını başlatır.</div>
                                <div class="command-desc">Hastaya sıvı/serum takviyesi başlatma komutu.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me serum setini intrakete bağlar, mandallı vanayı açarak sıvı akışını başlatır.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me ampul halindeki ağrı kesici/morfini kırar, şırıngaya çekerek serum lastiğinden enjekte eder.</div>
                                <div class="command-desc">Ağrı ve şok önleyici ilaç enjeksiyonu.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me ampul halindeki ağrı kesici/morfini kırar, şırıngaya çekerek serum lastiğinden enjekte eder.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                    </div>

                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-heart-crack"></i> Grup C: Kalp Masajı (CPR) ve Şok Cihazı</div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me ellerini kenetleyerek hastanın göğüs kemiğinin ortasına yerleştirir ve 30:2 ritmiyle kalp masajına başlar.</div>
                                <div class="command-desc">Kalp durması vakalarında uygulanan temel yaşam desteği.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me ellerini kenetleyerek hastanın göğüs kemiğinin ortasına yerleştirir and 30:2 ritmiyle kalp masajına başlar.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me defibrilatör cihazını açar, pedleri hastanın göğsüne yapıştırıp "Alandan çekilin!" diye bağırır ve şok butonuna basar.</div>
                                <div class="command-desc">Elektroşok cihazı uygulama rolü.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me defibrilatör cihazını açar, pedleri hastanın göğsüne yapıştırıp \"Alandan çekilin!\" diye bağırır ve şok butonuna basar.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/do uygulanan CPR ve şoklama neticesinde hastanın kalbi tekrar atmaya başlamış mıdır?</div>
                                <div class="command-desc">Kritik müdahale sonrası hayata dönme durum tespiti.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/do uygulanan CPR ve şoklama neticesinde hastanın kalbi tekrar atmaya başlamış mıdır?')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                    </div>

                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-crutch"></i> Grup D: Kırık, Çıkık ve Atelleme Prosedürü</div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me hasarlı ekstremiteyi (kol/bacak) nazikçe kavrayarak anatomik pozisyona getirir ve altını destekler.</div>
                                <div class="command-desc">Kırık kemiği düzeltme ve hizalama.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me hasarlı ekstremiteyi (kol/bacak) nazikçe kavrayarak anatomik pozisyona getirir ve altını destekler.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me medikal çantadan şişme veya vakumlu ateli çıkarır, ekstremiteye sararak sabitler.</div>
                                <div class="command-desc">Kırık bölgenin oynamaması için atel uygulaması.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me medikal çantadan şişme veya vakumlu ateli çıkarır, ekstremiteye sararak sabitler.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                    </div>

                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-scissors"></i> Grup E: Gelişmiş Ameliyathane / Cerrahi Operasyon</div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me neşteri kavrar, steril edilen hat üzerinden deriyi pürüzsüz bir şekilde keserek insizyonu açar.</div>
                                <div class="command-desc">Cerrahi operasyon başlangıcı, kesi atma rolü.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me neşteri kavrar, steril edilen hat üzerinden deriyi pürüzsüz bir şekilde keserek insizyonu açar.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me penset yardımıyla dokuyu aralar, içerideki mermi çekirdeğini/yabancı cismi bularak cerrahi kaba çıkartır.</div>
                                <div class="command-desc">Vücuttaki yabancı maddeyi/mermiyi çıkarma rolü.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me penset yardımıyla dokuyu aralar, içerideki mermi çekirdeğini/yabancı cismi bularak cerrahi kaba çıkartır.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me bistüri ve koter cihazını kullanarak iç kanama odağını yakar ve kanamayı tamamen durdurur.</div>
                                <div class="command-desc">İç kanamayı durdurmak için damar yakma işlemi.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me bistüri ve koter cihazını kullanarak iç kanama odağını yakar ve kanamayı tamamen durdurur.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me portegüyü eline alır, iğne ipliği geçirerek kesilen doku katmanlarını anatomik olarak dikmeye başlar.</div>
                                <div class="command-desc">Operasyon sonu dikiş atma aşaması.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me portegüyü eline alır, iğne ipliği geçirerek kesilen doku katmanlarını anatomik olarak dikmeye başlar.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/do cerrahi müdahale başarılı geçmiş ve hastanın durumu normale dönmüştür.</div>
                                <div class="command-desc">Operasyonun nihai ve olumlu sonucunu belirten durum rolü.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/do cerrahi müdahale başarılı geçmiş ve hastanın durumu normale dönmüştür.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                    </div>
                </div>

                <div id="section-personel" class="panel-section">
                    <div class="page-header"><h1>Personel Yönetim Sistemi</h1></div>
                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-users-gear"></i> Aktif Görevli Listesi</div>
                        <div class="table-responsive">
                            <table class="data-table" id="staff-table">
                                <thead><tr><th>Sicil / ID</th><th>Departman ve Yetki</th><th>Durum</th></tr></thead>
                                <tbody>
                                    <tr><td>#01</td><td>Yönetici / Kurucu</td><td><span class="badge">Sistem Sahibi</span></td></tr>
                                    <tr><td>#02</td><td>Sağlık Personeli</td><td><span class="badge">Aktif</span></td></tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>

                <div id="section-about" class="panel-section">
                    <div class="page-header"><h1>Sistem Hakkında</h1></div>
                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-circle-nodes"></i> Operasyonel Panel Detayları</div>
                        <div style="line-height: 1.8; color: #cbd5e1; font-size: 0.95rem;">
                            <p>Bu güvenli altyapı, acil durum müdahale ekiplerinin sahadaki rol kalıplarını ve komut akışlarını tek bir merkezden yönetebilmesi için dizayn edilmiştir.</p>
                            <p>Tüm hakları saklıdır. Sistemin dikey esnekliği ve arama altyapısı mobil cihazların kaydırma motorlarına entegre edilmiştir.</p>
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
                document.getElementById('main-panel').style.display = window.innerWidth >= 768 ? 'grid' : 'block';
            } else {
                document.getElementById('error-text').style.display = 'block';
            }
        }
        document.getElementById('password-field').addEventListener('keypress', function(e) { if (e.key === 'Enter') { checkPassword(); } });
        
        function switchTab(tabName) {
            document.querySelectorAll('.panel-section').forEach(sec => sec.classList.remove('active-section'));
            document.querySelectorAll('.menu-item').forEach(item => item.classList.remove('active'));
            document.getElementById('section-' + tabName).classList.add('active-section');
            document.getElementById('menu-' + tabName).classList.add('active');
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
                if (text.toUpperCase().indexOf(filter) > -1 || desc.toUpperCase().indexOf(filter) > -1) { item.style.display = "flex"; } else { item.style.display = "none"; }
            });
        }
    </script>
</body>
</html>
