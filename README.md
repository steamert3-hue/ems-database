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
            font-size: 1rem; font-weight: 600; color: #38bdf8; margin-
