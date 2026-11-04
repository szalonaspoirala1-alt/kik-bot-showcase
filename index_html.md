<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ZIEMIA 2.0 – Centrum Społeczności & Hall of Fame</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&family=JetBrains+Mono:wght@500;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-dark: #07090e;
            --bg-card: rgba(16, 20, 29, 0.78);
            --bg-card-hover: rgba(24, 30, 44, 0.92);
            --kick-green: #53fc18;
            --kick-green-dim: rgba(83, 252, 24, 0.14);
            --twitch-purple: #9146ff;
            --twitch-purple-dim: rgba(145, 70, 255, 0.16);
            --text-main: #f3f5f8;
            --text-muted: #8b95a8;
            --border-subtle: rgba(255, 255, 255, 0.08);
            --gold: #fbbf24;
            --silver: #cbd5e1;
            --bronze: #d97706;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
            background-color: var(--bg-dark);
            background-image: 
                radial-gradient(circle at 15% 15%, rgba(83, 252, 24, 0.08) 0%, transparent 40%),
                radial-gradient(circle at 85% 20%, rgba(145, 70, 255, 0.09) 0%, transparent 42%),
                radial-gradient(circle at 50% 90%, rgba(83, 252, 24, 0.05) 0%, transparent 45%);
            color: var(--text-main);
            min-height: 100vh;
            line-height: 1.5;
            overflow-x: hidden;
        }

        .container {
            max-width: 1180px;
            margin: 0 auto;
            padding: 28px 20px 64px;
        }

        /* NAVBAR */
        .navbar {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 16px 24px;
            background: rgba(13, 17, 25, 0.82);
            backdrop-filter: blur(14px);
            border: 1px solid var(--border-subtle);
            border-radius: 18px;
            margin-bottom: 36px;
        }

        .brand {
            display: flex;
            align-items: center;
            gap: 14px;
            font-weight: 900;
            font-size: 1.35rem;
            letter-spacing: -0.02em;
        }

        .brand-logo {
            height: 40px;
            width: auto;
            border-radius: 8px;
            object-fit: contain;
        }

        .brand-badge {
            display: inline-flex;
            align-items: center;
            gap: 6px;
            font-size: 0.75rem;
            font-weight: 700;
            padding: 4px 10px;
            border-radius: 999px;
            background: var(--kick-green-dim);
            color: var(--kick-green);
            border: 1px solid rgba(83, 252, 24, 0.3);
        }

        .pulse-dot {
            width: 8px;
            height: 8px;
            background-color: var(--kick-green);
            border-radius: 50%;
            box-shadow: 0 0 10px var(--kick-green);
            animation: pulse 1.8s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(0.95); opacity: 0.8; }
            50% { transform: scale(1.25); opacity: 1; }
            100% { transform: scale(0.95); opacity: 0.8; }
        }

        /* HERO */
        .hero {
            text-align: center;
            margin-bottom: 42px;
        }

        .hero h1 {
            font-size: clamp(2rem, 4.5vw, 3.25rem);
            font-weight: 900;
            letter-spacing: -0.03em;
            margin-bottom: 12px;
            background: linear-gradient(135deg, #ffffff 30%, #a5b4fc 70%, var(--kick-green) 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .hero p {
            color: var(--text-muted);
            font-size: 1.05rem;
            max-width: 680px;
            margin: 0 auto;
        }

        /* INTRO VIDEO */
        #intro-video-wrapper {
            display: none;
            margin: 0 auto 40px;
            max-width: 860px;
            border-radius: 20px;
            overflow: hidden;
            border: 1px solid var(--border-subtle);
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.65);
            background: #000;
        }

        #intro-video-wrapper video {
            width: 100%;
            display: block;
            max-height: 480px;
        }

        /* STATS CARDS */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
            gap: 20px;
            margin-bottom: 48px;
        }

        .stat-card {
            background: var(--bg-card);
            backdrop-filter: blur(12px);
            border: 1px solid var(--border-subtle);
            border-radius: 20px;
            padding: 26px 24px;
            position: relative;
            overflow: hidden;
            transition: transform 0.2s ease, border-color 0.2s ease;
        }

        .stat-card:hover {
            transform: translateY(-4px);
            border-color: rgba(83, 252, 24, 0.35);
        }

        .stat-card.purple-card:hover {
            border-color: rgba(145, 70, 255, 0.45);
        }

        .stat-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 12px;
        }

        .stat-title {
            font-size: 0.85rem;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 0.06em;
            color: var(--text-muted);
        }

        .stat-icon {
            font-size: 1.5rem;
        }

        .stat-value {
            font-family: 'JetBrains Mono', monospace;
            font-size: 2.5rem;
            font-weight: 800;
            color: var(--text-main);
            line-height: 1.1;
        }

        .stat-sub {
            margin-top: 8px;
            font-size: 0.8rem;
            color: var(--text-muted);
        }

        /* TERMINAL SECTION */
        .terminal-section {
            background: var(--bg-card);
            border: 1px solid var(--border-subtle);
            border-radius: 20px;
            padding: 24px;
            margin-bottom: 48px;
        }

        .terminal-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 16px;
        }

        .terminal-title {
            font-size: 1.15rem;
            font-weight: 800;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .terminal-box {
            background: #030406;
            border: 1px solid rgba(255, 255, 255, 0.06);
            border-radius: 14px;
            padding: 18px;
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.85rem;
            max-height: 280px;
            overflow-y: auto;
            color: #a7f3d0;
        }

        .terminal-row {
            display: flex;
            gap: 12px;
            margin-bottom: 8px;
            line-height: 1.4;
            border-bottom: 1px dashed rgba(255, 255, 255, 0.04);
            padding-bottom: 6px;
        }

        .terminal-row:last-child {
            margin-bottom: 0;
            border-bottom: none;
            padding-bottom: 0;
        }

        .t-time {
            color: var(--text-muted);
            flex-shrink: 0;
        }

        .t-user {
            color: var(--kick-green);
            font-weight: 700;
            flex-shrink: 0;
        }

        .t-text {
            color: var(--text-main);
            word-break: break-word;
        }

        .t-pts {
            color: var(--gold);
            margin-left: auto;
            flex-shrink: 0;
            font-weight: 700;
        }

        /* HALL OF FAME */
        .section-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 12px;
            margin-bottom: 24px;
        }

        .section-title {
            font-size: 1.55rem;
            font-weight: 800;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .scoring-pill {
            font-size: 0.8rem;
            color: var(--text-muted);
            background: rgba(255, 255, 255, 0.04);
            border: 1px solid var(--border-subtle);
            padding: 6px 14px;
            border-radius: 999px;
        }

        /* PODIUM TOP 3 */
        .podium-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
            margin-bottom: 28px;
        }

        .podium-card {
            background: var(--bg-card);
            border: 1px solid var(--border-subtle);
            border-radius: 20px;
            padding: 24px;
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;
            position: relative;
            transition: transform 0.2s ease, background 0.2s ease;
        }

        .podium-card:hover {
            transform: translateY(-4px);
            background: var(--bg-card-hover);
        }

        .podium-card.rank-1 {
            border-color: rgba(251, 191, 36, 0.45);
            box-shadow: 0 12px 35px rgba(251, 191, 36, 0.08);
        }

        .podium-card.rank-2 {
            border-color: rgba(203, 213, 225, 0.35);
        }

        .podium-card.rank-3 {
            border-color: rgba(217, 119, 6, 0.4);
        }

        .rank-badge {
            position: absolute;
            top: 16px;
            right: 16px;
            font-family: 'JetBrains Mono', monospace;
            font-weight: 800;
            font-size: 0.85rem;
            padding: 4px 10px;
            border-radius: 999px;
            background: rgba(255, 255, 255, 0.07);
        }

        .podium-avatar {
            width: 76px;
            height: 76px;
            border-radius: 50%;
            object-fit: cover;
            margin-bottom: 14px;
            border: 3px solid var(--border-subtle);
        }

        .rank-1 .podium-avatar { border-color: var(--gold); }
        .rank-2 .podium-avatar { border-color: var(--silver); }
        .rank-3 .podium-avatar { border-color: var(--bronze); }

        .podium-name {
            font-size: 1.15rem;
            font-weight: 800;
            margin-bottom: 6px;
            word-break: break-word;
        }

        .podium-score {
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.9rem;
            font-weight: 700;
            color: var(--kick-green);
            background: var(--kick-green-dim);
            padding: 4px 12px;
            border-radius: 999px;
            margin-bottom: 16px;
        }

        .podium-metrics {
            display: flex;
            justify-content: center;
            gap: 14px;
            width: 100%;
            padding-top: 14px;
            border-top: 1px solid var(--border-subtle);
            font-size: 0.85rem;
            color: var(--text-muted);
        }

        .podium-metrics span strong {
            color: var(--text-main);
            font-family: 'JetBrains Mono', monospace;
        }

        /* LEADERBOARD LIST */
        .leaderboard-card {
            background: var(--bg-card);
            border: 1px solid var(--border-subtle);
            border-radius: 20px;
            overflow: hidden;
        }

        .leaderboard-row {
            display: grid;
            grid-template-columns: 56px 1fr auto;
            align-items: center;
            gap: 16px;
            padding: 14px 22px;
            border-bottom: 1px solid var(--border-subtle);
            transition: background 0.15s ease;
        }

        .leaderboard-row:last-child {
            border-bottom: none;
        }

        .leaderboard-row:hover {
            background: var(--bg-card-hover);
        }

        .row-rank {
            font-family: 'JetBrains Mono', monospace;
            font-weight: 700;
            color: var(--text-muted);
            font-size: 0.95rem;
        }

        .row-user {
            display: flex;
            align-items: center;
            gap: 12px;
            min-width: 0;
        }

        .row-avatar {
            width: 38px;
            height: 38px;
            border-radius: 50%;
            object-fit: cover;
            flex-shrink: 0;
            border: 1px solid var(--border-subtle);
        }

        .row-name {
            font-weight: 700;
            font-size: 0.98rem;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .row-stats {
            display: flex;
            align-items: center;
            gap: 16px;
            font-size: 0.85rem;
            color: var(--text-muted);
        }

        .row-stats .stat-pill {
            background: rgba(255, 255, 255, 0.04);
            padding: 4px 10px;
            border-radius: 8px;
            font-family: 'JetBrains Mono', monospace;
        }

        .row-score {
            font-family: 'JetBrains Mono', monospace;
            font-weight: 800;
            color: var(--kick-green);
            min-width: 85px;
            text-align: right;
        }

        .footer {
            margin-top: 56px;
            text-align: center;
            color: var(--text-muted);
            font-size: 0.85rem;
        }

        @media (max-width: 680px) {
            .leaderboard-row {
                grid-template-columns: 42px 1fr;
                gap: 10px;
            }
            .row-stats {
                grid-column: 1 / -1;
                justify-content: space-between;
                padding-top: 6px;
            }
        }
    </style>
</head>
<body>

    <div class="container">
        <nav class="navbar">
            <div class="brand">
                <img src="logo.png" alt="ZIEMIA 2.0" class="brand-logo" onerror="this.style.display='none'">
                <span>ZIEMIA 2.0</span>
            </div>
            <div class="brand-badge">
                <span class="pulse-dot"></span>
                <span>KICK & TWITCH LIVE BOT</span>
            </div>
        </nav>

        <header class="hero">
            <h1>CENTRUM SPOŁECZNOŚCI ZIEMIA 2.0</h1>
            <p>Automatyczne shoty 1080p Full HD, zrzuty ekranu PNG oraz animacje GIF 640p tworzone na żywo przez społeczność Discorda.</p>
        </header>

        <div id="intro-video-wrapper">
            <video id="intro-video" controls preload="metadata"></video>
        </div>

        <section class="stats-grid">
            <div class="stat-card">
                <div class="stat-header">
                    <span class="stat-title">Wycięte Shoty 1080p</span>
                    <span class="stat-icon">🎬</span>
                </div>
                <div class="stat-value" id="stat-shots">—</div>
                <div class="stat-sub">Klipów wideo nagranych na serwerze</div>
            </div>

            <div class="stat-card">
                <div class="stat-header">
                    <span class="stat-title">Zrzuty Ekranu HD</span>
                    <span class="stat-icon">📸</span>
                </div>
                <div class="stat-value" id="stat-screens">—</div>
                <div class="stat-sub">Bezstratnych klatek PNG ze streamów</div>
            </div>

            <div class="stat-card purple-card">
                <div class="stat-header">
                    <span class="stat-title">Animacje GIF 640p</span>
                    <span class="stat-icon">🎞️</span>
                </div>
                <div class="stat-value" id="stat-gifs">—</div>
                <div class="stat-sub">Wygenerowanych animacji z transmisji</div>
            </div>
        </section>

        <section class="terminal-section">
            <div class="terminal-header">
                <h3 class="terminal-title">💻 Terminal na żywo & Aktywność</h3>
                <span style="font-size: 0.8rem; color: var(--text-muted);">Ostatnie zdarzenia na serwerze</span>
            </div>
            <div class="terminal-box" id="terminal-box">
                <div style="color: var(--text-muted); text-align: center; padding: 20px;">Ładowanie aktywności...</div>
            </div>
        </section>

        <section>
            <div class="section-header">
                <h2 class="section-title">🏆 Hall of Fame – Najaktywniejsi Twórcy</h2>
                <div class="scoring-pill">Punktacja: 🎬 Shot = <strong>3 pkt</strong> &bull; 🎞️ GIF = <strong>2 pkt</strong> &bull; 📸 Screen = <strong>1 pkt</strong></div>
            </div>

            <div class="podium-grid" id="podium-container"></div>
            <div class="leaderboard-card" id="leaderboard-container"></div>
        </section>

        <footer class="footer">
            <p>ZIEMIA 2.0 &bull; Statystyki synchronizowane automatycznie z serwerem Discord</p>
        </footer>
    </div>

    <script>
        const API_BASE = "";

        function escapeHtml(str) {
            if (!str) return "";
            return String(str)
                .replace(/&/g, "&amp;")
                .replace(/</g, "&lt;")
                .replace(/>/g, "&gt;")
                .replace(/"/g, "&quot;");
        }

        async function fetchAllData() {
            try {
                const [statsRes, topRes, actRes] = await Promise.all([
                    fetch(`${API_BASE}/api/stats`),
                    fetch(`${API_BASE}/api/top`),
                    fetch(`${API_BASE}/api/activity`)
                ]);

                if (statsRes.ok) {
                    const stats = await statsRes.json();
                    document.getElementById("stat-shots").textContent = (stats.shots ?? 0).toLocaleString("pl-PL");
                    document.getElementById("stat-screens").textContent = (stats.screens ?? 0).toLocaleString("pl-PL");
                    document.getElementById("stat-gifs").textContent = (stats.gifs ?? 0).toLocaleString("pl-PL");

                    const videoWrapper = document.getElementById("intro-video-wrapper");
                    const videoEl = document.getElementById("intro-video");
                    if (stats.intro_video_url && !videoEl.getAttribute("src")) {
                        videoEl.setAttribute("src", stats.intro_video_url);
                        videoWrapper.style.display = "block";
                    }
                }

                if (topRes.ok) {
                    const users = await topRes.json();
                    renderLeaderboard(Array.isArray(users) ? users : []);
                }

                if (actRes.ok) {
                    const activity = await actRes.json();
                    renderActivity(Array.isArray(activity) ? activity : []);
                }
            } catch (err) {
                console.warn("Błąd pobierania danych:", err);
            }
        }

        function renderActivity(events) {
            const box = document.getElementById("terminal-box");
            if (!events.length) {
                box.innerHTML = `<div style="color: var(--text-muted); text-align: center;">Brak ostatnich zdarzeń...</div>`;
                return;
            }

            box.innerHTML = events.map(ev => `
                <div class="terminal-row">
                    <span class="t-time">[${escapeHtml(ev.time)}]</span>
                    <span class="t-user">${escapeHtml(ev.user)}</span>
                    <span class="t-text">${escapeHtml(ev.text)}</span>
                    <span class="t-pts">${escapeHtml(ev.pts)}</span>
                </div>
            `).join("");
        }

        function renderLeaderboard(users) {
            const podiumEl = document.getElementById("podium-container");
            const listEl = document.getElementById("leaderboard-container");

            if (!users.length) {
                podiumEl.innerHTML = "";
                listEl.innerHTML = `<div style="padding: 28px; text-align: center; color: var(--text-muted);">Trwa ładowanie rankingu Hall of Fame...</div>`;
                return;
            }

            const top3 = users.slice(0, 3);
            const rest = users.slice(3, 25);
            const medals = ["🥇 #1", "🥈 #2", "🥉 #3"];

            podiumEl.innerHTML = top3.map((u, idx) => `
                <div class="podium-card rank-${idx + 1}">
                    <span class="rank-badge">${medals[idx]}</span>
                    <img src="${escapeHtml(u.avatar)}" alt="${escapeHtml(u.name)}" class="podium-avatar" onerror="this.src='https://cdn.discordapp.com/embed/avatars/0.png'">
                    <div class="podium-name">${escapeHtml(u.name)}</div>
                    <div class="podium-score">${u.score} PKT</div>
                    <div class="podium-metrics">
                        <span>🎬 <strong>${u.shots}</strong></span>
                        <span>🎞️ <strong>${u.gifs}</strong></span>
                        <span>📸 <strong>${u.screens}</strong></span>
                    </div>
                </div>
            `).join("");

            if (rest.length > 0) {
                listEl.style.display = "block";
                listEl.innerHTML = rest.map(u => `
                    <div class="leaderboard-row">
                        <div class="row-rank">#${u.rank}</div>
                        <div class="row-user">
                            <img src="${escapeHtml(u.avatar)}" alt="${escapeHtml(u.name)}" class="row-avatar" onerror="this.src='https://cdn.discordapp.com/embed/avatars/0.png'">
                            <span class="row-name">${escapeHtml(u.name)}</span>
                        </div>
                        <div class="row-stats">
                            <span class="stat-pill">🎬 ${u.shots}</span>
                            <span class="stat-pill">🎞️ ${u.gifs}</span>
                            <span class="stat-pill">📸 ${u.screens}</span>
                            <span class="row-score">${u.score} PKT</span>
                        </div>
                    </div>
                `).join("");
            } else {
                listEl.style.display = "none";
            }
        }

        fetchAllData();
        setInterval(fetchAllData, 10000);
    </script>
</body>
</html>