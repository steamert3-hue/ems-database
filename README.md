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
                
                <!-- BÖLÜM 1: MUAYENE -->
                <div id="section-muayene" class="panel-section active-section">
                    <div class="page-header"><h1>Detaylı Muayene Komutları</h1></div>
                    
                    <!-- Grup A -->
                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-heart-pulse"></i> Grup A: Olay Yeri İlk Temas ve Bilinç Kontrolü</div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me hızlı adımlarla yaralının yanına çöker, çevre güvenliğini kontrol ettikten sonra hastanın omuzlarından sarsar.</div>
                                <div class="command-desc">Olay yerine varışta çevre güvenliği ve ilk fiziksel temas.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me hızlı adımlarla yaralının yanına çöker, çevre güvenliğini kontrol ettikten sonra hastanın omuzlarından sarsar.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me "Beni duyuyor musunuz? İyi misiniz?" diyerek yüksek sesle hastaya seslenir ve tepkisini ölçer.</div>
                                <div class="command-desc">Sesli uyarana cevap arama aşaması.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me \"Beni duyuyor musunuz? İyi misiniz?\" diyerek yüksek sesle hastaya seslenir ve tepkisini ölçer.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/do yaralının bilinci yerinde midir, herhangi bir sese veya sarsıntıya tepki veriyor mu?</div>
                                <div class="command-desc">Karşı oyuncudan bilinç ve refleks durumu talep eder.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/do yaralının bilinci yerinde midir, herhangi bir sese veya sarsıntıya tepki veriyor mu?')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                    </div>

                    <!-- Grup B -->
                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-wave-square"></i> Grup B: Nabız ve Hayati Belirti Ölçümü</div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me sağ elinin işaret ve orta parmağını hastanın şah damarına (karotis arter) bastırarak nabız almaya çalışır.</div>
                                <div class="command-desc">Şah damarı üzerinden ilk mekanik nabız kontrolü.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me sağ elinin işaret ve orta parmağını hastanın şah damarına (karotis arter) bastırarak nabız almaya çalışır.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me diğer eliyle hastanın bileğindeki radyal arteri bularak nabız ritmini saniye üzerinden takip eder.</div>
                                <div class="command-desc">Bilek üzerinden destekleyici nabız kontrolü.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me diğer eliyle hastanın bileğindeki radyal arteri bularak nabız ritmini saniye üzerinden takip eder.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/do şah damarından ve bilekten alınan nabız stabil midir, dakikada ortalama kaç atıyor?</div>
                                <div class="command-desc">Nabzın hızı ve kalitesini öğrenmek için kullanılan durum sorusu.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/do şah damarından ve bilekten alınan nabız stabil midir, dakikada ortalama kaç atıyor?')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                    </div>

                    <!-- Grup C -->
                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-stethoscopes"></i> Grup C: Solunum Analizi (Bak-Dinle-Hisset)</div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me kulağını hastanın ağız ve burun bölgesine yaklaştırır, gözleriyle göğüs kafesinin hareketlerini gözlemler.</div>
                                <div class="command-desc">Bak-Dinle-Hisset yöntemiyle solunum tespiti.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me kulağını hastanın ağzına yaklaştırır, gözleriyle göğüs kafesinin inip kalkışını izler (Bak-Dinle-Hisset).')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/do hastanın solunumu var mıdır, nefes alıp verirken göğüs kafesi düzenli hareket ediyor mu?</div>
                                <div class="command-desc">Solunum ritmini öğrenmek üzere yöneltilen /do sorusu.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/do hastanın solunumu var mıdır, nefes alıp verirken göğüs kafesi düzenli hareket ediyor mu?')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me travma çantasını açıp stetoskopu çıkartır, kulaklığı takarak diyaframı hastanın göğüs ve sırt bölgelerine koyar.</div>
                                <div class="command-desc">Akciğer seslerini dinlemek için stetoskop hazırlığı ve kullanımı.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me travma çantasını açıp stetoskopu çıkartır, kulaklığı takarak diyaframı hastanın göğüs ve sırt bölgelerine koyar.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/do stetoskop ile dinlenen akciğerlerden hırıltı, sıvı sesi veya anormal bir sürtünme sesi geliyor mu?</div>
                                <div class="command-desc">Akciğer yaralanması veya iç kanama tespiti için durum sorusu.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/do stetoskop ile dinlenen akciğerlerden hırıltı, sıvı sesi veya anormal bir sürtünme sesi geliyor mu?')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                    </div>

                    <!-- Grup D -->
                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-eye"></i> Grup D: Göz Bebekleri ve Nörolojik Değerlendirme</div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me cebinden muayene fenerini (pupila feneri) çıkartır, hastanın göz kapaklarını parmaklarıyla aralayarak ışık tutar.</div>
                                <div class="command-desc">Göz bebeklerinin ışık refleks ölçümü.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me cebinden muayene fenerini (pupila feneri) çıkartır, hastanın göz kapaklarını parmaklarıyla aralayarak ışık tutar.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/do göz bebeklerinin ışığa tepkisi nasıldır? (İzokorik mi, ışıkta küçülme refleksi gösteriyor mu?)</div>
                                <div class="command-desc">Kafa travması ve beyin fonksiyonları tespiti için /do sorusu.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/do göz bebeklerinin ışığa tepkisi nasıldır? (İzokorik mi, ışıkta küçülme refleksi gösteriyor mu?)')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                    </div>
                </div>

                <!-- BÖLÜM 2: TEDAVİ -->
                <div id="section-tedavi" class="panel-section">
                    <div class="page-header"><h1>Tedavi ve Operasyonlar</h1></div>
                    
                    <!-- Grup A -->
                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-droplet-slash"></i> Grup A: Aktif Kanama Durdurma ve Pansuman</div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me çantasından steril gazlı bezleri hızla çıkarıp yaralı ve kanamalı bölgenin üzerine kapatarak iki eliyle baskı uygular.</div>
                                <div class="command-desc">Açık yaraya elle kompresyon/baskı uygulama aşaması.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me çantasından steril gazlı bezleri hızla çıkarıp yaralı ve kanamalı bölgenin üzerine kapatarak iki eliyle baskı uygular.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/do yapılan yoğun baskı neticesinde kanama durmuş mu yoksa gazlı bezleri aşarak devam ediyor mu?</div>
                                <div class="command-desc">Kanamayı kontrol altına alma durum sorusu.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/do yapılan yoğun baskı neticesinde kanama durmuş mu yoksa gazlı bezleri aşarak devam ediyor mu?')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me ilk katmanı kaldırmadan üzerine ek sargı bezi koyar, rulo bandajla baskıyı bozmadan yarayı sıkıca sarar.</div>
                                <div class="command-desc">Sargı bezini sabitleme ve bandajlama rölü.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me ilk katmanı kaldırmadan üzerine ek sargı bezi koyar, rulo bandajla baskıyı bozmadan yarayı sıkıca sarar.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                    </div>

                    <!-- Grup B -->
                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-syringe"></i> Grup B: Damar Yolu Açma ve İlaç/Serum Enjeksiyonu</div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me turnikeyi çıkartıp hastanın dirsek üstüne bağlar, alkollü pamukla el bileği veya dirsek önü damar hattını dezenfekte eder.</div>
                                <div class="command-desc">Turnike bağlama ve bölge sterilizasyonu.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me turnikeyi çıkartıp hastanın dirsek üstüne bağlar, alkollü pamukla el bileği veya dirsek önü damar hattını dezenfekte eder.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me steril paketinden çıkardığı uygun boyuttaki intraketi (branül) 30 derecelik açıyla damara doğru batırır.</div>
                                <div class="command-desc">Damar çeperine girme anı rolü.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me steril paketinden çıkardığı uygun boyuttaki intraketi (branül) 30 derecelik açıyla damara doğru batırır.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/do intraketin şeffaf haznesine (arkasına) kan gelmiş midir, damar yolu başarılı mıdır?</div>
                                <div class="command-desc">Damar yolunun yerinde olup olmadığını teyit eden soru.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/do intraketin şeffaf haznesine (arkasına) kan gelmiş midir, damar yolu başarılı mıdır?')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me kılavuz iğneyi geri çekip plastik kanülü damarda bırakır, serum setinin ucunu takarak vanasını sonuna kadar açar.</div>
                                <div class="command-desc">Serumu aktif olarak bağlama ve akış başlatma.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me kılavuz iğneyi geri çekip plastik kanülü damarda bırakır, serum setinin ucunu takarak vanasını sonuna kadar açar.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me ampul halindeki ağrı kesici ve morfini kırar, enjektöre çekerek serumun ilaç verme portundan sisteme aktarır.</div>
                                <div class="command-desc">Hastanın acısını dindirmek için morfin/ağrı kesici enjeksiyonu.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me ampul halindeki ağrı kesici ve morfini kırar, enjektöre çekerek serumun ilaç verme portundan sisteme aktarır.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                    </div>

                    <!-- Grup C -->
                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-heart-crack"></i> Grup C: İleri Yaşam Desteği - CPR ve Defibrilatör (Şok)</div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me ellerini üst üste getirip kenetler, hastanın sternum kemiğinin ortasına yerleştirerek dakikada 100 bası olacak şekilde CPR'a başlar.</div>
                                <div class="command-desc">Kalp masajı ritmini başlatma komutu.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me ellerini üst üste getirip kenetler, hastanın sternum kemiğinin ortasına yerleştirerek dakikada 100 bası olacak şekilde CPR\'a başlar.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me defibrilatör cihazının güç düğmesine basar, jel sürdüğü pedleri hastanın sağ köprücük kemiği altına ve sol meme altına yapıştırır.</div>
                                <div class="command-desc">Şok cihazı pedlerinin yerleştirilmesi.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me defibrilatör cihazının güç düğmesine basar, jel sürdüğü pedleri hastanın sağ köprücük kemiği altına ve sol meme altına yapıştırır.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me "Cihaz analiz ediyor, alandan çekilin!" diyerek çevredekileri uzaklaştırır ve şarj olan kırmızı şok butonuna basar.</div>
                                <div class="command-desc">Elektroşok akımını hastanın vücuduna verme rolü.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me \"Cihaz analiz ediyor, alandan çekilin!\" diyerek çevredekileri uzaklaştırır ve şarj olan kırmızı şok butonuna basar.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/do verilen elektroşok ve aralıksız CPR uygulaması neticesinde hastanın kalbi geri dönmüş müdür, monitörde ritim var mı?</div>
                                <div class="command-desc">Kritik canlandırma işleminin sonucunu soran /do sorusu.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/do verilen elektroşok ve aralıksız CPR uygulaması neticesinde hastanın kalbi geri dönmüş müdür, monitörde ritim var mı?')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                    </div>

                    <!-- Grup D -->
                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-crutch"></i> Grup D: Kemik Kırıkları, Çıkıklar ve Atelleme Prosedürü</div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me kırık şüphesi olan bölgeyi (kol/bacak) iki eliyle uç kısımlardan stabil tutarak anatomik hizaya getirmeye çalışır.</div>
                                <div class="command-desc">Kırık uzvu sabitleme ve düzeltme hareketi.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me kırık şüphesi olan bölgeyi (kol/bacak) iki eliyle uç kısımlardan stabil tutarak anatomik hizaya getirmeye çalışır.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me travma çantasından uygun boyuttaki vakumlu/şişme ateli çıkarır, kırık uzvun altına yerleştirerek sargılarla kilitler.</div>
                                <div class="command-desc">Uzuv oynamasın diye atel montajı yapma.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me travma çantasından uygun boyuttaki vakumlu/şişme ateli çıkarır, kırık uzvun altına yerleştirerek sargılarla kilitler.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/do kırık kemik uçları sabitlenmiş midir, uzuvda herhangi bir iç/dış hareket kalmış mıdır?</div>
                                <div class="command-desc">Atelleme işleminin başarısını kontrol eden /do sorusu.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/do kırık kemik uçları sabitlenmiş midir, uzuvda herhangi bir iç/dış hareket kalmış mıdır?')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                    </div>

                    <!-- Grup E -->
                    <div class="group-container">
                        <div class="group-title"><i class="fa-solid fa-scissors"></i> Grup E: İleri Cerrahi Müdahale ve Ameliyathane İşlemleri</div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me steril neşteri (bistüri) sağ eline alır, dezenfekte edilen hat üzerinden deriyi pürüzsüzce keserek cerrahi sahayı açar.</div>
                                <div class="command-desc">Ameliyatı başlatma, ilk kesiyi atma rolü.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me steril neşteri (bistüri) sağ eline alır, dezenfekte edilen hat üzerinden deriyi pürüzsüzce keserek cerrahi sahayı açar.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me ekartörleri yerleştirerek dokuyu iki yana açar, içeride hasar gören kas ve organ dokularını görünür hale getirir.</div>
                                <div class="command-desc">Cerrahi sahayı genişletme aşaması.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me ekartörleri yerleştirerek dokuyu iki yana açar, içeride hasar gören kas ve organ dokularını görünür hale getirir.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me cerrahi penset yardımıyla doku derinliklerine iner, içeride sıkışan mermi çekirdeğini/yabancı cismi kavrayarak dışarı çıkartır.</div>
                                <div class="command-desc">Vücuttan kurşun veya yabancı cisim çıkarma anı.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me cerrahi penset yardımıyla doku derinliklerine iner, içeride sıkışan mermi çekirdeğini/yabancı cismi kavrayarak dışarı çıkartır.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me koter cihazını kullanarak yırtılan iç damar uçlarını tek tek yakar ve batın içindeki kanamayı tamamen durdurur.</div>
                                <div class="command-desc">İç kanamayı koterle yakarak durdurma aşaması.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me koter cihazını kullanarak yırtılan iç damar uçlarını tek tek yakar ve batın içindeki kanamayı tamamen durdurur.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/me portegüyü eline alıp ucuna emilebilir cerrahi ipliği takar, kesilen tüm doku katmanlarını içeriden dışarıya doğru diker.</div>
                                <div class="command-desc">İç dokuları ve cildi cerrahi dikişle kapatma.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/me portegüyü eline alıp ucuna emilebilir cerrahi ipliği takar, kesilen tüm doku katmanlarını içeriden dışarıya doğru diker.')"><i class="fa-solid fa-copy"></i> Kopyala</button>
                        </div>
                        <div class="command-row">
                            <div>
                                <div class="command-text">/do operasyon esnasında hastanın hayati fonksiyonları ne durumdadır, cerrahi işlem başarıyla tamamlanmış mıdır?</div>
                                <div class="command-desc">Ameliyatın bittiğini ve hastanın stabil olduğunu bildiren nihai durum rolü.</div>
                            </div>
                            <button class="copy-btn" onclick="copyToClipboard('/do operasyon esnasında hastanın hayati fonksiyonları ne durumdadır, cerrahi işlem başarıyla tamamlanmış mıdır?')"><i class="fa-solid fa-copy"></i> Kopyala</button>
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
                                <thead><tr><th>Sicil / ID</th><th>Departman ve Yetki</th><th>Durum</th></tr></thead>
                                <tbody>
                                    <tr><td>#01</td><td>Yönetici / Kurucu</td><td><span class="badge">Sistem Sahibi</span></td></tr>
                                    <tr><td>#02</td><td>Sağlık Personeli</td><td><span class="badge">Aktif</span></td></tr>
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
                            <p>Bu güvenli altyapı, acil durum müdahale ekiplerinin sahadaki rol kalıplarını ve komut akışlarını tek bir merkezden yönetebilmesi için dizayn edilmiştir.</p>
                            <p>Sistem genelindeki arama motoru, girilen kelimeleri hem komut satırlarında hem de açıklamalarında gerçek zamanlı olarak süzer.</p>
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
