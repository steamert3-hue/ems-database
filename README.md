<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>USMS & EMS ULTRA SURGICAL DATABASE v9.5</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --bg-main: #030712;
            --bg-sidebar: #111827;
            --bg-card: #1f2937;
            --accent-color: #38bdf8;
            --accent-hover: #0ea5e9;
            --text-main: #e2e8f0;
            --text-muted: #6b7280;
            --border-color: #334155;
            --code-bg: #020617;
            --code-text: #34d399;
        }

        html, body {
            background-color: var(--bg-main) !important;
            color: var(--text-main) !important;
            margin: 0 !important;
            padding: 0 !important;
            font-family: 'Inter', sans-serif;
            height: 100vh !important;
            overflow: hidden !important;
        }

        /* --- ŞİFRE EKRANI --- */
        #login-overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background-color: #030712;
            z-index: 9999;
            display: flex; justify-content: center; align-items: center;
            transition: opacity 0.5s ease;
        }
        .login-box {
            background-color: var(--bg-sidebar); padding: 40px; border-radius: 12px;
            border: 2px solid var(--border-color); box-shadow: 0 20px 25px -5px rgba(0,0,0,0.5);
            text-align: center; width: 90%; max-width: 380px;
        }
        .login-box h1 { color: var(--accent-color); font-size: 18px; margin-bottom: 5px; letter-spacing: 2px; }
        .login-box p { color: var(--text-muted); font-size: 11px; margin-bottom: 25px; font-weight: bold; }
        .login-box input[type="password"] {
            width: 100%; padding: 12px; background-color: #030712; border: 1px solid var(--border-color);
            border-radius: 6px; color: #ffffff; font-size: 16px; text-align: center; outline: none; box-sizing: border-box; margin-bottom: 15px;
        }
        .login-box button {
            width: 100%; padding: 12px; background-color: var(--accent-color); color: #030712;
            border: none; border-radius: 6px; font-size: 14px; font-weight: bold; cursor: pointer;
        }
        #error-msg { color: #f87171; font-size: 13px; margin-top: 15px; display: none; }

        /* --- PANEL --- */
        #main-app { display: none; height: 100vh; grid-template-columns: 350px 1fr; }
        .sidebar { background-color: var(--bg-sidebar); border-right: 2px solid var(--border-color); overflow-y: auto; }
        .content-area { padding: 40px; overflow-y: auto; background-color: var(--bg-main); }
        .section-card { background-color: var(--bg-sidebar); border-radius: 8px; padding: 30px; margin-bottom: 35px; border: 1px solid var(--border-color); }
        .section-card h2 { color: var(--accent-color); border-bottom: 2px solid var(--border-color); padding-bottom: 12px; font-size:
