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

        /* Tüm ekranı kaplayan ve taşmayı ana gövdede engelleyen ayar */
        html, body {
            background-color: var(--bg-main);
            color: var(--text-main);
            margin: 0;
            padding: 0;
            font-family: 'Inter', sans-serif;
            height: 100vh;
            width: 100vw;
            overflow: hidden !important; /* Dış çerçevenin bozulmasını engeller */
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

        .input-group { position: relative; margin-bottom: 1.
