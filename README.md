<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TFMS IPTV Panel Deployment Guide</title>
    <style>
        :root {
            --bg-main: #0b0f19;
            --bg-card: #151d30;
            --bg-code: #070a12;
            --text-main: #f3f4f6;
            --text-muted: #9ca3af;
            --primary: #f38020;
            --primary-glow: rgba(243, 128, 32, 0.15);
            --accent: #3b82f6;
            --accent-glow: rgba(59, 130, 246, 0.2);
            --border: #24324f;
            --success: #10b981;
            --success-bg: rgba(16, 185, 129, 0.1);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            line-height: 1.7;
            color: var(--text-main);
            background-color: var(--bg-main);
            padding: 40px 20px;
        }

        .container {
            max-width: 850px;
            margin: 0 auto;
        }

        header {
            text-align: center;
            margin-bottom: 50px;
        }

        h1 {
            font-size: 2.5rem;
            font-weight: 800;
            color: #fff;
            letter-spacing: -0.5px;
            margin-bottom: 12px;
        }

        h1 span {
            color: var(--primary);
            text-shadow: 0 0 20px var(--primary-glow);
        }

        .subtitle {
            color: var(--text-muted);
            font-size: 1.1rem;
        }

        .step {
            background: var(--bg-card);
            border: 1px solid var(--border);
            padding: 30px;
            margin-bottom: 30px;
            border-radius: 16px;
            position: relative;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            transition: transform 0.2s ease, border-color 0.2s ease;
        }

        .step:hover {
            transform: translateY(-2px);
            border-color: var(--primary);
        }

        h2 {
            font-size: 1.4rem;
            color: #fff;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 12px;
        }

        ul {
            list-style: none;
        }

        li {
            margin-bottom: 12px;
            position: relative;
            padding-left: 28px;
            color: var(--text-main);
        }

        li::before {
            content: "→";
            position: absolute;
            left: 0;
            color: var(--primary);
            font-weight: bold;
        }

        strong {
            color: #fff;
            background: rgba(255, 255, 255, 0.05);
            padding: 2px 6px;
            border-radius: 4px;
        }

        code {
            background-color: var(--bg-code);
            color: #e2e8f0;
            padding: 3px 8px;
            border-radius: 6px;
            font-family: 'Fira Code', Consolas, Monaco, monospace;
            font-size: 0.85em;
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        .code-container {
            position: relative;
            margin: 20px 0;
        }

        pre {
            background-color: var(--bg-code);
            border: 1px solid var(--border);
            padding: 20px;
            border-radius: 12px;
            overflow-x: auto;
        }

        pre code {
            background: none;
            padding: 0;
            border: none;
            color: #cbd5e1;
            font-size: 0.9em;
            line-height: 1.5;
        }

        .copy-btn {
            position: absolute;
            top: 12px;
            right: 12px;
            background: var(--bg-card);
            border: 1px solid var(--border);
            color: var(--text-main);
            padding: 6px 12px;
            font-size: 0.8rem;
            border-radius: 6px;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .copy-btn:hover {
            background: var(--primary);
            color: #fff;
            border-color: var(--primary);
        }

        .copy-btn.copied {
            background: var(--success);
            color: #fff;
            border-color: var(--success);
        }

        .credentials {
            background-color: var(--success-bg);
            border: 1px solid var(--success);
            padding: 20px;
            border-radius: 12px;
            margin-top: 20px;
        }

        .credentials h3 {
            color: var(--success);
            font-size: 1.1rem;
            margin-bottom: 10px;
        }

        .credentials ul li::before {
            color: var(--success);
        }

        .link-highlight {
            color: var(--accent);
            text-decoration: none;
            border-bottom: 1px dashed var(--accent);
        }

        .link-highlight:hover {
            background: var(--accent-glow);
        }
    </style>
</head>
<body>

    <div class="container">
        <header>
            <h1>TFMS <span>IPTV Panel</span> v1.0.1</h1>
            <p class="subtitle">A modernized Cloudflare step-by-step setup and deployment guide.<br>DEMO Site <a href="https://tfms-tv-panel-v1-0-1.citymcfc.workers.dev" target="_blank"><button>Enter Here</button></a><strong>User: admin & Pass: SecretPassword123</strong><br>
            Note: DO NOT use the Demo Site to stream your media it is just so you can see it working</p>
        </header>

        <!-- Step 0 -->
        <div class="step">
            <h2>Whats included<br>Deploy The Script To Cloudflare Serverless Workers</h2>
            <ul>
                <li>TFMS IPTV Dashboard</li>
                <li>Add/Remove/Edit, Users, Streams, Proxies & VOD</li>
                <li>1 Click Proxy Creation Tools (Cloudflare, Codesandbox, More)</li>
                <li>Mass Import Streams & VOD, Sticky Admin Notes & Quick Links</li>
                <li>Free Stream Links (No streams come preinstalled)</li>
                <li>Tools, M3U Analyzer & M3U Url Formatter, JW & ClappR Players</li>
            </ul>
        </div>

        <!-- Step 1 -->
        <div class="step">
            <h2>Step 1: Create Your D1 Database</h2>
            <ul>
                <li>Log into your Cloudflare dashboard</li>
                <li>Go to <strong>Storage & Databases</strong> on the left menu</li>
                <li>Click <strong>D1 SQL Database</strong></li>
                <li>Click <strong>Create database</strong></li>
                <li>Enter <strong>tfms-tv-v1-0-1</strong> for the name of your database</li>
                <li>Click <strong>Create</strong></li>
            </ul>
        </div>

        <!-- Step 2 -->
        <div class="step">
            <h2>Step 2: Initialize Database Tables</h2>
            <ul>
                <li>Click <strong>Console</strong> on the database navigation bar</li>
                <li>Paste the following SQL script into the console editor</li>
                <li>Then Click <strong>Execute</strong></li>
            </ul>
            <div class="code-container">
                <button class="copy-btn" onclick="copyCode(this)">Copy Script</button>
                <pre><code id="sqlScript">CREATE TABLE IF NOT EXISTS users (id INTEGER PRIMARY KEY AUTOINCREMENT,username TEXT UNIQUE NOT NULL,password TEXT NOT NULL,status TEXT DEFAULT 'active',exp_date TEXT);

CREATE TABLE IF NOT EXISTS streams (id INTEGER PRIMARY KEY AUTOINCREMENT,name TEXT NOT NULL,url TEXT NOT NULL,category TEXT DEFAULT 'Live');

CREATE TABLE IF NOT EXISTS proxies (id INTEGER PRIMARY KEY AUTOINCREMENT,name TEXT NOT NULL,url TEXT NOT NULL);

CREATE TABLE IF NOT EXISTS users (id INTEGER PRIMARY KEY AUTOINCREMENT,username TEXT UNIQUE NOT NULL,password TEXT NOT NULL,status TEXT DEFAULT 'active',exp_date TEXT,max_connections INTEGER DEFAULT 1);

CREATE TABLE IF NOT EXISTS streams (id INTEGER PRIMARY KEY AUTOINCREMENT,name TEXT NOT NULL,url TEXT NOT NULL,category TEXT DEFAULT 'Live');

CREATE TABLE IF NOT EXISTS proxies (id INTEGER PRIMARY KEY AUTOINCREMENT,name TEXT NOT NULL,url TEXT NOT NULL);

CREATE TABLE IF NOT EXISTS comments ( id INTEGER PRIMARY KEY, content TEXT, updated_at TEXT);

CREATE TABLE IF NOT EXISTS settings ( id INTEGER PRIMARY KEY, admin_user TEXT, admin_pass TEXT);

INSERT OR IGNORE INTO settings (id, admin_user, admin_pass) VALUES (1, 'admin', 'SecretPassword123');

ALTER TABLE users ADD COLUMN max_connections INTEGER DEFAULT 1;</code></pre>
            </div>
        </div>

        <!-- Step 3 -->
        <div class="step">
            <h2>Step 3: Create the Worker Application</h2>
            <ul>
                <li>Return to the main Cloudflare dashboard</li>
                <li>Navigate to <strong>Compute</strong> &gt; <strong>Workers &amp; Pages</strong></li>
                <li>Click <strong>Create application</strong></li>
                <li>Select <strong>Start with Hello World</strong></li>
                <li>Name your application: <strong>tfms-tv-v1-0-1</strong></li>
                <li>Click <strong>Deploy</strong></li>
            </ul>
        </div>

        <!-- Step 4 -->
        <div class="step">
            <h2>Step 4: Deploy the Source Code</h2>
            <ul>
                <li>Click <strong>Edit Code</strong> in the top-right area</li>
                <li>On the left panel script editor, Select and clear all existing code</li>
                <li>Open the txt link below & Copy all the text code (Make sure to copy ALL the code)<br>
                <a href="https://tfms.xyz/firestick/core/files/tfms-tv-panel-v1-0-1-worker.txt" class="link-highlight" target="_blank"><code>https://tfms.xyz/firestick/core/files/tfms-tv-panel-v1-0-1-worker.txt</code></a></li>
                <li>Paste the copied text into the Cloudflare code editor</li>
                <li>Click the <strong>Deploy</strong> button</li>
            </ul>
        </div>

        <!-- Step 5 -->
        <div class="step">
            <h2>Step 5: Configure Database Bindings</h2>
            <ul>
                <li>Click your <strong>Worker's name</strong> in the top-left area to return to worker settings</li>
                <li>Click <strong>Bindings Its on the nav-bar</strong></li>
                <li>Click the <strong>Add Binding</strong> button</li>
                <li>Select <strong>D1 Database</strong></li>
                <li>Click <strong>Add binding</strong></li>
                <li>Enter <code>DB</code> in the <strong>Variable Name</strong> field, Only enter the letters <b>DB</b></li>
                <li>Select your newly created database from the <strong>D1 database</strong> dropdown <strong>tfms-tv-v1-0-1</strong></li>
                <li>Click <strong>Add Binding</strong></li>
            </ul>
        </div>

        <!-- Step 6 -->
        <div class="step">
            <h2>Step 6: Access Your Application</h2>
            <ul>
                <li>Locate your live deployment URL on the Worker dashboard</li>
                <li>Open the URL in your web browser</li>
                <li>Change default user & pass on the settings page</li>
            </ul>
            <div class="credentials">
                <h3>Default Login Credentials</h3>
                <ul>
                    <li><strong>Username:</strong> <code>admin</code></li>
                    <li><strong>Password:</strong> <code>SecretPassword123</code></li>
                </ul>
            </div>
        </div>
    </div>

    <script>
        function copyCode(button) {
            const codeText = document.getElementById('sqlScript').innerText;
            navigator.clipboard.writeText(codeText).then(() => {
                button.textContent = 'Copied!';
                button.classList.add('copied');
                
                setTimeout(() => {
                    button.textContent = 'Copy Script';
                    button.classList.remove('copied');
                }, 2000);
            }).catch(err => {
                console.error('Failed to copy text: ', err);
            });
        }
    </script>
</body>
</html>






<center><h1><b><u>TFMS IPTV Panel v1.0.1 With D1 SQL & Add & Create More Proxies Section</u></b></h1></center>
<b>For a full install guide with DEMO</b> <a href="https://tfms.xyz/firestick/core/tuts/tfms-tv-panel-v1-0-1.TUT.GUIDE.html">See Here</a><br><br>
<h2><b>Cloudflare Hosted</b></h2>
.JS With D1 Database for storing your user details<br>
With add more proxies section<br>
Easy To Deploy in under 2 minutes<br>
Lightweight fast & very usable<br>
Add/Remove/Edit Users/Streams & proxies<br>
Create Personal Playlists for anyone!<br>
Set Playlist connection limits & expiry dates<br><br>
<b>No streams</b> come preinstalled on this panel<br>
<b>However</b> i have added a Get Stream link where you can find some streams to use<br>
<b>Note: Only use streams that have a good connection limit!<br>This panel plays direct streams through a proxy & does not restream</b>
<h2><b>It is upto you to use this application responsibly</b></h2>

<img width="1257" height="807" alt="1" src="https://github.com/user-attachments/assets/949b2333-2b1d-437d-adba-a994a9100425" />

<img width="1257" height="845" alt="2" src="https://github.com/user-attachments/assets/9ae5a4fe-2bc1-45c9-a519-4780d83cb37b" />

<img width="1257" height="1183" alt="3" src="https://github.com/user-attachments/assets/ac4bb600-4bc2-4626-b684-f1d91228ed50" />

<img width="1257" height="1805" alt="4" src="https://github.com/user-attachments/assets/045d10ec-331c-4fbc-a778-9bcfd94b3064" />

<img width="1257" height="3406" alt="5" src="https://github.com/user-attachments/assets/ac43a02a-84fd-406d-8cc2-e64f73047fed" />
