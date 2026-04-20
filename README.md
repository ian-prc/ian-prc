<!DOCTYPE html>
<html>
<head>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Space+Mono:ital,wght@0,400;0,700;1,400&family=Syne:wght@400;600;800&display=swap');

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: #0a0a0f;
    color: #e0dff5;
    font-family: 'Space Mono', monospace;
    min-height: 100vh;
    overflow-x: hidden;
  }

  .bg-grid {
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(120,80,255,0.05) 1px, transparent 1px),
      linear-gradient(90deg, rgba(120,80,255,0.05) 1px, transparent 1px);
    background-size: 40px 40px;
    pointer-events: none;
    z-index: 0;
  }

  .scan-line {
    position: fixed;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, transparent, rgba(160,100,255,0.6), transparent);
    animation: scan 6s linear infinite;
    z-index: 1;
    pointer-events: none;
  }

  @keyframes scan {
    0% { top: -2px; }
    100% { top: 100vh; }
  }

  .wrapper {
    position: relative;
    z-index: 2;
    max-width: 680px;
    margin: 0 auto;
    padding: 0 0 60px;
  }

  .hero {
    position: relative;
    padding: 48px 32px 32px;
    border-bottom: 1px solid rgba(140,80,255,0.2);
    overflow: hidden;
  }

  .hero-glow {
    position: absolute;
    top: -60px; left: 50%;
    transform: translateX(-50%);
    width: 400px; height: 200px;
    background: radial-gradient(ellipse, rgba(120,60,255,0.3) 0%, transparent 70%);
    pointer-events: none;
  }

  .prompt-line {
    font-size: 11px;
    color: rgba(140,80,255,0.7);
    letter-spacing: 0.08em;
    margin-bottom: 16px;
  }

  .prompt-line span { color: #7c5cbf; }

  .hero-name {
    font-family: 'Syne', sans-serif;
    font-size: clamp(38px, 8vw, 64px);
    font-weight: 800;
    line-height: 0.95;
    letter-spacing: -0.02em;
    background: linear-gradient(135deg, #fff 30%, #b080ff 70%, #7040cc 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    margin-bottom: 12px;
  }

  .hero-sub {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 12px;
    color: rgba(200,180,255,0.6);
    letter-spacing: 0.1em;
    margin-bottom: 28px;
  }

  .hero-sub .dot { color: rgba(140,80,255,0.5); }

  .badge-row { display: flex; gap: 10px; flex-wrap: wrap; }

  .badge {
    font-size: 11px;
    letter-spacing: 0.06em;
    padding: 5px 12px;
    border-radius: 2px;
    border: 1px solid rgba(140,80,255,0.3);
    color: rgba(200,180,255,0.7);
    background: rgba(80,40,160,0.15);
    transition: all 0.2s;
    cursor: default;
  }

  .badge:hover {
    border-color: rgba(180,120,255,0.6);
    color: #d0b0ff;
    background: rgba(100,50,200,0.25);
  }

  .badge.active {
    background: rgba(120,60,255,0.3);
    border-color: rgba(160,100,255,0.6);
    color: #c090ff;
  }

  .stats-bar {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    border-bottom: 1px solid rgba(140,80,255,0.15);
  }

  .stat-item {
    padding: 20px 24px;
    border-right: 1px solid rgba(140,80,255,0.15);
    position: relative;
  }

  .stat-item:last-child { border-right: none; }

  .stat-item::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, transparent, rgba(140,80,255,0.5), transparent);
    opacity: 0;
    transition: opacity 0.3s;
  }

  .stat-item:hover::before { opacity: 1; }

  .stat-label {
    font-size: 10px;
    color: rgba(160,130,255,0.5);
    letter-spacing: 0.12em;
    margin-bottom: 4px;
  }

  .stat-val {
    font-family: 'Syne', sans-serif;
    font-size: 28px;
    font-weight: 800;
    color: #c090ff;
  }

  .stat-sub {
    font-size: 10px;
    color: rgba(160,130,255,0.4);
    margin-top: 2px;
  }

  .section {
    padding: 28px 32px;
    border-bottom: 1px solid rgba(140,80,255,0.12);
  }

  .section-tag {
    font-size: 10px;
    color: rgba(140,80,255,0.6);
    letter-spacing: 0.16em;
    margin-bottom: 16px;
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .section-tag::after {
    content: '';
    flex: 1;
    height: 1px;
    background: rgba(140,80,255,0.15);
  }

  .code-block {
    background: rgba(20,12,40,0.8);
    border: 1px solid rgba(100,60,200,0.25);
    border-radius: 4px;
    padding: 20px;
    font-size: 12px;
    line-height: 1.8;
  }

  .code-key { color: #9066cc; }
  .code-str { color: #66ccaa; }
  .code-arr { color: rgba(180,160,255,0.5); }
  .code-comment { color: rgba(160,140,255,0.35); font-style: italic; }
  .code-indent { padding-left: 20px; display: block; }

  .facts-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
  }

  .fact-card {
    background: rgba(20,12,40,0.6);
    border: 1px solid rgba(100,60,200,0.2);
    border-radius: 4px;
    padding: 14px 16px;
    font-size: 11px;
    line-height: 1.6;
    color: rgba(200,180,255,0.65);
    transition: border-color 0.2s, background 0.2s;
  }

  .fact-card:hover {
    border-color: rgba(160,100,255,0.4);
    background: rgba(40,20,80,0.5);
  }

  .fact-icon { font-size: 14px; margin-bottom: 6px; display: block; }

  .lang-row { margin-bottom: 12px; }

  .lang-header {
    display: flex;
    justify-content: space-between;
    font-size: 11px;
    margin-bottom: 5px;
    color: rgba(200,180,255,0.7);
  }

  .lang-pct { color: rgba(160,130,255,0.5); }

  .lang-bar-track {
    height: 3px;
    background: rgba(100,60,200,0.15);
    border-radius: 2px;
    overflow: hidden;
  }

  .lang-bar-fill {
    height: 100%;
    border-radius: 2px;
    animation: growBar 1.2s ease-out forwards;
    transform-origin: left;
  }

  @keyframes growBar {
    from { transform: scaleX(0); }
    to { transform: scaleX(1); }
  }

  .contrib-wrap { overflow-x: auto; }

  .contrib-grid {
    display: grid;
    grid-template-columns: repeat(52, 11px);
    grid-template-rows: repeat(7, 11px);
    gap: 2px;
    grid-auto-flow: column;
    width: max-content;
  }

  .contrib-cell {
    width: 11px; height: 11px;
    border-radius: 2px;
    background: rgba(60,30,120,0.2);
    transition: transform 0.15s;
  }

  .contrib-cell:hover { transform: scale(1.4); }
  .contrib-cell.l1 { background: rgba(100,50,200,0.35); }
  .contrib-cell.l2 { background: rgba(120,60,220,0.55); }
  .contrib-cell.l3 { background: rgba(150,80,255,0.75); }
  .contrib-cell.l4 { background: #a060ff; }

  .streak-row {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 12px;
    margin-top: 20px;
  }

  .streak-card {
    background: rgba(20,12,40,0.6);
    border: 1px solid rgba(100,60,200,0.2);
    border-radius: 4px;
    padding: 16px;
    text-align: center;
  }

  .streak-num {
    font-family: 'Syne', sans-serif;
    font-size: 32px;
    font-weight: 800;
    color: #b080ff;
    display: block;
  }

  .streak-lbl {
    font-size: 10px;
    color: rgba(160,130,255,0.5);
    letter-spacing: 0.1em;
    margin-top: 4px;
  }

  .streak-date {
    font-size: 10px;
    color: rgba(140,110,220,0.4);
    margin-top: 2px;
  }

  .quote-block {
    border-left: 2px solid rgba(140,80,255,0.5);
    padding: 16px 20px;
    background: rgba(20,12,40,0.5);
    border-radius: 0 4px 4px 0;
    font-style: italic;
    font-size: 12px;
    line-height: 1.8;
    color: rgba(200,180,255,0.6);
  }

  .quote-author {
    margin-top: 10px;
    font-style: normal;
    font-size: 11px;
    color: rgba(140,80,255,0.6);
    letter-spacing: 0.08em;
  }

  .connect-grid { display: flex; gap: 10px; flex-wrap: wrap; }

  .connect-btn {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.08em;
    padding: 8px 16px;
    border: 1px solid rgba(140,80,255,0.35);
    border-radius: 2px;
    background: rgba(80,40,160,0.1);
    color: rgba(200,180,255,0.7);
    cursor: pointer;
    transition: all 0.2s;
    text-decoration: none;
    display: inline-flex;
    align-items: center;
    gap: 6px;
  }

  .connect-btn:hover {
    background: rgba(120,60,240,0.25);
    border-color: rgba(180,120,255,0.6);
    color: #d0b0ff;
    transform: translateY(-1px);
  }

  .connect-btn.primary {
    border-color: rgba(160,100,255,0.6);
    background: rgba(100,50,200,0.25);
    color: #c090ff;
  }

  .cursor {
    display: inline-block;
    width: 8px; height: 14px;
    background: rgba(160,100,255,0.8);
    animation: blink 1s step-end infinite;
    vertical-align: middle;
    margin-left: 2px;
  }

  @keyframes blink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0; }
  }

  ::-webkit-scrollbar { width: 4px; height: 4px; }
  ::-webkit-scrollbar-track { background: rgba(20,12,40,0.5); }
  ::-webkit-scrollbar-thumb { background: rgba(120,60,200,0.5); border-radius: 2px; }
</style>
</head>
<body>
<div class="bg-grid"></div>
<div class="scan-line"></div>

<div class="wrapper">

  <!-- HERO -->
  <div class="hero">
    <div class="hero-glow"></div>
    <div class="prompt-line"><span>~/</span>ianpurcia<span> $</span> whoami</div>
    <div class="hero-name">Ian<br>Purcia<span class="cursor"></span></div>
    <div class="hero-sub">
      Full-Stack Developer
      <span class="dot">&#9670;</span>
      MERN Stack
      <span class="dot">&#9670;</span>
      Philippines &#127477;&#127469;
    </div>
    <div class="badge-row">
      <div class="badge active">React</div>
      <div class="badge active">TypeScript</div>
      <div class="badge active">Node.js</div>
      <div class="badge">MongoDB</div>
      <div class="badge">Express</div>
      <div class="badge">Tailwind CSS</div>
      <div class="badge">Zustand</div>
      <div class="badge">JWT</div>
    </div>
  </div>

  <!-- STATS BAR -->
  <div class="stats-bar">
    <div class="stat-item">
      <div class="stat-label">FOLLOWERS</div>
      <div class="stat-val">1</div>
      <div class="stat-sub">github.com/ianpurcia</div>
    </div>
    <div class="stat-item">
      <div class="stat-label">PUBLIC REPOS</div>
      <div class="stat-val">9</div>
      <div class="stat-sub">and growing</div>
    </div>
    <div class="stat-item">
      <div class="stat-label">PROFILE VIEWS</div>
      <div class="stat-val">223</div>
      <div class="stat-sub">all-time</div>
    </div>
  </div>

  <!-- ABOUT ME -->
  <div class="section">
    <div class="section-tag">// about_me</div>
    <div class="code-block">
      <span><span class="code-key">name</span><span class="code-arr">: </span><span class="code-str">"Ian Purcia"</span></span><br>
      <span><span class="code-key">location</span><span class="code-arr">: </span><span class="code-str">"Philippines &#127477;&#127469;"</span></span><br>
      <span><span class="code-key">role</span><span class="code-arr">: </span><span class="code-str">"Student &amp; Full-Stack Developer (in progress)"</span></span><br>
      <span><span class="code-key">education</span><span class="code-arr">: </span><span class="code-str">"Currently studying"</span></span><br>
      <br>
      <span><span class="code-key">currently_building</span><span class="code-arr">: </span><span class="code-arr">[</span></span><br>
      <span class="code-indent"><span class="code-str">"Tasked &amp; Confused — full-stack task manager"</span><span class="code-arr">,</span></span><br>
      <span class="code-indent"><span class="code-str">"Because my own life needed a CRUD app"</span></span><br>
      <span><span class="code-arr">]</span></span><br>
      <br>
      <span><span class="code-key">stack</span><span class="code-arr">: </span><span class="code-arr">{</span></span><br>
      <span class="code-indent"><span class="code-key">frontend</span><span class="code-arr">: </span><span class="code-str">"React, TypeScript, Tailwind, Zustand"</span></span><br>
      <span class="code-indent"><span class="code-key">backend</span><span class="code-arr">: </span><span class="code-str">"Express, MongoDB, Mongoose, JWT"</span></span><br>
      <span><span class="code-arr">}</span></span><br>
      <br>
      <span class="code-comment">// 2026 goal: deploy to production without --force pushing &#128128;</span>
    </div>
  </div>

  <!-- QUICK FACTS -->
  <div class="section">
    <div class="section-tag">// quick_facts</div>
    <div class="facts-grid">
      <div class="fact-card">
        <span class="fact-icon">&#9889;</span>
        Superpower: Googling error messages faster than a Grab rider on EDSA
      </div>
      <div class="fact-card">
        <span class="fact-icon">&#128737;&#65039;</span>
        Backend philosophy: if it doesn't have helmet, cors, and rate-limit — it's not production
      </div>
      <div class="fact-card">
        <span class="fact-icon">&#128269;</span>
        Debug strategy: console.log("BAKIT GANITO") &#8592; certified Filipino dev move
      </div>
      <div class="fact-card">
        <span class="fact-icon">&#128156;</span>
        Life lesson: git stash has saved more relationships than therapy
      </div>
      <div class="fact-card">
        <span class="fact-icon">&#9749;</span>
        Powered by Kopiko 78°C and well-placed console.log statements
      </div>
      <div class="fact-card">
        <span class="fact-icon">&#128561;</span>
        Worst fear: merge conflict at 5PM on a Friday
      </div>
    </div>
  </div>

  <!-- LANGUAGES -->
  <div class="section">
    <div class="section-tag">// most_used_languages</div>
    <div class="lang-row">
      <div class="lang-header"><span>Blade</span><span class="lang-pct">49.38%</span></div>
      <div class="lang-bar-track"><div class="lang-bar-fill" style="width:49.38%;background:linear-gradient(90deg,#9060dd,#b080ff);animation-delay:0.1s"></div></div>
    </div>
    <div class="lang-row">
      <div class="lang-header"><span>CSS</span><span class="lang-pct">19.21%</span></div>
      <div class="lang-bar-track"><div class="lang-bar-fill" style="width:19.21%;background:linear-gradient(90deg,#4480cc,#6699ee);animation-delay:0.2s"></div></div>
    </div>
    <div class="lang-row">
      <div class="lang-header"><span>PHP</span><span class="lang-pct">15.89%</span></div>
      <div class="lang-bar-track"><div class="lang-bar-fill" style="width:15.89%;background:linear-gradient(90deg,#7070bb,#9090cc);animation-delay:0.3s"></div></div>
    </div>
    <div class="lang-row">
      <div class="lang-header"><span>TypeScript</span><span class="lang-pct">9.51%</span></div>
      <div class="lang-bar-track"><div class="lang-bar-fill" style="width:9.51%;background:linear-gradient(90deg,#2288bb,#44aadd);animation-delay:0.4s"></div></div>
    </div>
    <div class="lang-row">
      <div class="lang-header"><span>JavaScript</span><span class="lang-pct">2.42%</span></div>
      <div class="lang-bar-track"><div class="lang-bar-fill" style="width:2.42%;background:linear-gradient(90deg,#cc9900,#eecc22);animation-delay:0.5s"></div></div>
    </div>
    <div class="lang-row">
      <div class="lang-header"><span>Hack / HTML / Java</span><span class="lang-pct">~3.6%</span></div>
      <div class="lang-bar-track"><div class="lang-bar-fill" style="width:3.6%;background:rgba(140,80,255,0.4);animation-delay:0.6s"></div></div>
    </div>
  </div>

  <!-- CONTRIBUTIONS -->
  <div class="section">
    <div class="section-tag">// contribution_activity</div>
    <div class="contrib-wrap">
      <div class="contrib-grid" id="contribGrid"></div>
    </div>
    <div class="streak-row">
      <div class="streak-card">
        <span class="streak-num">293</span>
        <div class="streak-lbl">TOTAL CONTRIBUTIONS</div>
        <div class="streak-date">Sep 2022 – Present</div>
      </div>
      <div class="streak-card">
        <span class="streak-num">0</span>
        <div class="streak-lbl">CURRENT STREAK</div>
        <div class="streak-date">Apr 20</div>
      </div>
      <div class="streak-card">
        <span class="streak-num">6</span>
        <div class="streak-lbl">LONGEST STREAK</div>
        <div class="streak-date">Feb 16 – Feb 21</div>
      </div>
    </div>
  </div>

  <!-- QUOTE -->
  <div class="section">
    <div class="section-tag">// random_dev_quote</div>
    <div class="quote-block">
      "Testing can be a very effective way to show the presence of bugs, but it is hopelessly inadequate for showing their absence."
      <div class="quote-author">— Edsger W. Dijkstra</div>
    </div>
  </div>

  <!-- CONNECT -->
  <div class="section" style="border-bottom:none;">
    <div class="section-tag">// lets_connect</div>
    <div class="connect-grid">
      <a class="connect-btn primary" href="https://github.com/ianpurcia" target="_blank">&#8997; GitHub</a>
      <a class="connect-btn" href="mailto:ianpurcia@gmail.com">@ Gmail</a>
      <div class="connect-btn" style="opacity:0.5;cursor:not-allowed;">&#8599; Portfolio — coming soon</div>
    </div>
  </div>

</div>

<script>
  const grid = document.getElementById('contribGrid');
  const levels = [0,0,0,0,1,0,0,1,2,1,0,1,2,3,4,3,2,1,0,0,1,2,1,0,1,0,0,2,3,4,2,1,0,0,1,2,4,3,2,1,0,0,1,2,1,0,0,1,2,3,0,0,1,0,0,1,0,0,0,1,2,1,0,0,1,0,1,2,3,0,1,0,0,0,0,0,0,1,0,0,0,1,0,0,0,0,1,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0];
  for (let i = 0; i < 364; i++) {
    const cell = document.createElement('div');
    cell.className = 'contrib-cell' + (levels[i] ? ' l' + levels[i] : '');
    grid.appendChild(cell);
  }
</script>
</body>
</html>
