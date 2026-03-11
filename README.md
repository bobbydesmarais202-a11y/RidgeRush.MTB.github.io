<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>RidgeRush.com — Ride. Play. Explore.</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Barlow+Condensed:wght@300;400;600;700&family=Barlow:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --dirt: #8B5E3C;
    --pine: #2D5016;
    --pine-light: #3d6b1f;
    --rock: #4A4A4A;
    --sky: #1a2f4a;
    --sky-mid: #0f1e30;
    --amber: #E8A020;
    --ember: #FF6B2B;
    --cream: #F0E8D8;
    --mist: rgba(240,232,216,0.07);
    --mud: #5C3D1E;
    --snow: #E8EFF5;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }
  html { scroll-behavior: smooth; }
  body {
    background: var(--sky-mid);
    color: var(--cream);
    font-family: 'Barlow', sans-serif;
    overflow-x: hidden;
  }

  /* ── NAV ── */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 1000;
    display: flex; align-items: center; justify-content: space-between;
    padding: 1rem 2.5rem;
    background: rgba(15,30,48,0.85);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid rgba(232,160,32,0.2);
  }
  .logo {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 2rem; letter-spacing: 3px;
    color: var(--amber);
    text-shadow: 0 0 20px rgba(232,160,32,0.4);
  }
  .logo span { color: var(--cream); }
  nav ul { list-style: none; display: flex; gap: 2rem; }
  nav ul a {
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.95rem; font-weight: 600; letter-spacing: 2px;
    color: var(--cream); text-decoration: none; text-transform: uppercase;
    transition: color 0.2s;
  }
  nav ul a:hover { color: var(--amber); }

  /* ── HERO ── */
  #hero {
    height: 100vh; position: relative; overflow: hidden;
    display: flex; flex-direction: column; align-items: center; justify-content: center;
  }
  .mountain-bg {
    position: absolute; inset: 0;
    background: linear-gradient(to bottom, #0a1829 0%, #1a3a5c 30%, #2d5576 50%, #1a2f4a 70%, #0f1e30 100%);
  }
  .mountains { position: absolute; bottom: 0; left: 0; right: 0; }
  .stars {
    position: absolute; inset: 0;
    background-image:
      radial-gradient(1px 1px at 10% 15%, rgba(255,255,255,0.8), transparent),
      radial-gradient(1px 1px at 25% 8%, rgba(255,255,255,0.6), transparent),
      radial-gradient(1px 1px at 40% 20%, rgba(255,255,255,0.9), transparent),
      radial-gradient(1px 1px at 60% 5%, rgba(255,255,255,0.7), transparent),
      radial-gradient(1px 1px at 75% 18%, rgba(255,255,255,0.5), transparent),
      radial-gradient(1px 1px at 85% 10%, rgba(255,255,255,0.8), transparent),
      radial-gradient(1px 1px at 92% 22%, rgba(255,255,255,0.6), transparent),
      radial-gradient(2px 2px at 18% 30%, rgba(255,255,255,0.4), transparent),
      radial-gradient(1px 1px at 55% 12%, rgba(255,255,255,0.7), transparent);
  }
  .hero-content {
    position: relative; z-index: 2;
    text-align: center; padding: 0 1rem;
  }
  .hero-eyebrow {
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.85rem; letter-spacing: 5px; text-transform: uppercase;
    color: var(--amber); margin-bottom: 1rem;
    opacity: 0; animation: fadeUp 0.8s 0.3s forwards;
  }
  .hero-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(5rem, 14vw, 11rem);
    letter-spacing: 6px; line-height: 0.9;
    color: var(--cream);
    text-shadow: 0 4px 30px rgba(0,0,0,0.5);
    opacity: 0; animation: fadeUp 0.8s 0.5s forwards;
  }
  .hero-title .rush { color: var(--amber); }
  .hero-sub {
    font-size: 1.1rem; font-weight: 300; letter-spacing: 3px;
    color: rgba(240,232,216,0.65); margin-top: 1.2rem;
    opacity: 0; animation: fadeUp 0.8s 0.7s forwards;
  }
  .hero-ctas {
    display: flex; gap: 1.2rem; justify-content: center;
    margin-top: 2.5rem;
    opacity: 0; animation: fadeUp 0.8s 0.9s forwards;
  }
  .btn {
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.9rem; font-weight: 700; letter-spacing: 3px; text-transform: uppercase;
    padding: 0.85rem 2.2rem; border: none; cursor: pointer;
    text-decoration: none; display: inline-block; transition: all 0.25s;
  }
  .btn-primary {
    background: var(--amber); color: var(--sky-mid);
    clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%);
  }
  .btn-primary:hover { background: var(--ember); transform: translateY(-2px); }
  .btn-secondary {
    background: transparent; color: var(--cream);
    border: 1.5px solid rgba(240,232,216,0.4);
    clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%);
  }
  .btn-secondary:hover { border-color: var(--amber); color: var(--amber); }
  .scroll-hint {
    position: absolute; bottom: 2rem; left: 50%; transform: translateX(-50%);
    display: flex; flex-direction: column; align-items: center; gap: 0.5rem;
    opacity: 0; animation: fadeIn 1s 1.5s forwards;
  }
  .scroll-hint span {
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.7rem; letter-spacing: 3px; color: rgba(240,232,216,0.4);
  }
  .scroll-arrow {
    width: 1px; height: 40px;
    background: linear-gradient(to bottom, var(--amber), transparent);
    animation: scrollPulse 1.5s infinite;
  }

  /* ── SECTION COMMONS ── */
  section { padding: 6rem 2.5rem; }
  .section-label {
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.75rem; letter-spacing: 5px; text-transform: uppercase;
    color: var(--amber); margin-bottom: 0.75rem;
  }
  .section-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(3rem, 7vw, 5.5rem);
    line-height: 0.95; letter-spacing: 2px;
  }
  .divider {
    width: 60px; height: 3px;
    background: linear-gradient(to right, var(--amber), var(--ember));
    margin: 1.5rem 0 2.5rem;
  }

  /* ── TRAILS ── */
  #trails {
    background: linear-gradient(135deg, #0d1e10 0%, #1a3318 40%, #0f1e30 100%);
    position: relative; overflow: hidden;
  }
  #trails::before {
    content: '';
    position: absolute; inset: 0;
    background-image: repeating-linear-gradient(
      45deg, transparent, transparent 40px,
      rgba(45,80,22,0.07) 40px, rgba(45,80,22,0.07) 41px
    );
  }

  /* ── TRAIL FILTERS ── */
  .trail-filters {
    display: flex; flex-wrap: wrap; gap: 0.6rem;
    margin-bottom: 1.5rem; position: relative; z-index: 1;
  }
  .filter-group {
    display: flex; gap: 0.4rem; align-items: center; flex-wrap: wrap;
  }
  .filter-label {
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.7rem; letter-spacing: 3px; text-transform: uppercase;
    color: rgba(240,232,216,0.35); margin-right: 0.2rem;
  }
  .filter-btn {
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.75rem; font-weight: 700; letter-spacing: 2px; text-transform: uppercase;
    padding: 0.4rem 1rem;
    background: rgba(255,255,255,0.04);
    border: 1px solid rgba(240,232,216,0.12);
    color: rgba(240,232,216,0.5);
    cursor: pointer; transition: all 0.2s;
    clip-path: polygon(6px 0%, 100% 0%, calc(100% - 6px) 100%, 0% 100%);
  }
  .filter-btn:hover { border-color: var(--amber); color: var(--amber); }
  .filter-btn.active { background: rgba(232,160,32,0.15); border-color: var(--amber); color: var(--amber); }
  .filter-btn.active-cat-markham { background: rgba(52,211,153,0.12); border-color: #34d399; color: #34d399; }
  .filter-btn.active-cat-quietwaters { background: rgba(244,114,182,0.12); border-color: #f472b6; color: #f472b6; }
  .filter-btn.active-cat-northamerica { background: rgba(96,165,250,0.12); border-color: #60a5fa; color: #60a5fa; }

  .trail-search {
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.85rem; letter-spacing: 1px;
    padding: 0.5rem 1.2rem;
    background: rgba(255,255,255,0.05);
    border: 1px solid rgba(240,232,216,0.12);
    color: var(--cream);
    outline: none; transition: border-color 0.2s;
    min-width: 220px;
    clip-path: polygon(6px 0%, 100% 0%, calc(100% - 6px) 100%, 0% 100%);
  }
  .trail-search::placeholder { color: rgba(240,232,216,0.3); }
  .trail-search:focus { border-color: var(--amber); }

  .trail-count {
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.8rem; letter-spacing: 2px;
    color: rgba(240,232,216,0.3);
    margin-bottom: 1.5rem; position: relative; z-index: 1;
  }
  .trail-count span { color: var(--amber); }

  .trails-grid {
    display: grid; grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 1.2rem; position: relative; z-index: 1;
  }
  .trail-card {
    background: rgba(15,30,20,0.7);
    border: 1px solid rgba(232,160,32,0.12);
    padding: 1.6rem;
    position: relative; overflow: hidden;
    transition: transform 0.3s, border-color 0.3s;
    clip-path: polygon(0 0, calc(100% - 14px) 0, 100% 14px, 100% 100%, 14px 100%, 0 calc(100% - 14px));
    cursor: pointer;
  }
  .trail-card:hover { transform: translateY(-3px); border-color: rgba(232,160,32,0.4); }
  .trail-card.expanded { border-color: var(--amber); background: rgba(15,35,22,0.9); }
  .trail-card::before {
    content: ''; position: absolute; top: 0; left: 0; right: 0; height: 3px;
  }
  .trail-card.diff-black::before { background: #444; }
  .trail-card.diff-red::before { background: var(--ember); }
  .trail-card.diff-blue::before { background: #3a7bd5; }
  .trail-card.diff-green::before { background: var(--pine-light); }
  .trail-card.diff-yellow::before { background: var(--amber); }

  /* Category stripe on left */
  .trail-card::after {
    content: ''; position: absolute; top: 0; left: 0; bottom: 0; width: 3px;
  }
  .trail-card.cat-markham::after { background: #34d399; }
  .trail-card.cat-quietwaters::after { background: #f472b6; }
  .trail-card.cat-northamerica::after { background: #60a5fa; }

  .trail-card-top {
    display: flex; justify-content: space-between; align-items: flex-start; gap: 0.5rem;
    margin-bottom: 0.5rem;
  }
  .trail-badges { display: flex; gap: 0.4rem; flex-wrap: wrap; margin-bottom: 0.75rem; align-items: center; }
  .trail-difficulty {
    display: inline-flex; align-items: center; gap: 0.4rem;
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.7rem; font-weight: 700; letter-spacing: 2px; text-transform: uppercase;
  }
  .diff-dot { width: 10px; height: 10px; border-radius: 50%; flex-shrink: 0; }
  .diff-dot.black { background: #666; }
  .diff-dot.red { background: var(--ember); }
  .diff-dot.blue { background: #3a7bd5; }
  .diff-dot.green { background: var(--pine-light); }
  .diff-dot.yellow { background: var(--amber); }

  .trail-category-badge {
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.65rem; letter-spacing: 2px; text-transform: uppercase;
    padding: 0.15rem 0.6rem;
    border-radius: 2px;
  }
  .cat-badge-markham { background: rgba(52,211,153,0.12); color: #34d399; border: 1px solid rgba(52,211,153,0.25); }
  .cat-badge-quietwaters { background: rgba(244,114,182,0.12); color: #f472b6; border: 1px solid rgba(244,114,182,0.25); }
  .cat-badge-northamerica { background: rgba(96,165,250,0.12); color: #60a5fa; border: 1px solid rgba(96,165,250,0.25); }

  .trail-type-badge {
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.65rem; letter-spacing: 2px; text-transform: uppercase;
    padding: 0.15rem 0.6rem;
    background: rgba(255,255,255,0.05);
    border: 1px solid rgba(255,255,255,0.1);
    color: rgba(240,232,216,0.5);
    border-radius: 2px;
  }

  .trail-name {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 1.7rem; letter-spacing: 1px;
    color: var(--cream); margin-bottom: 0.3rem; line-height: 1;
  }
  .trail-park {
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.75rem; letter-spacing: 1px;
    color: rgba(240,232,216,0.35); margin-bottom: 0.85rem;
  }
  .trail-desc {
    font-size: 0.82rem; line-height: 1.65;
    color: rgba(240,232,216,0.55);
    display: none;
    margin-bottom: 1.2rem;
  }
  .trail-card.expanded .trail-desc { display: block; }
  .trail-stats {
    display: flex; gap: 1.2rem; flex-wrap: wrap;
  }
  .stat { display: flex; flex-direction: column; gap: 0.1rem; }
  .stat-val {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 1.25rem; letter-spacing: 1px; color: var(--amber);
  }
  .stat-key {
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.6rem; letter-spacing: 2px; text-transform: uppercase;
    color: rgba(240,232,216,0.35);
  }
  .trail-expand-hint {
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.65rem; letter-spacing: 2px; text-transform: uppercase;
    color: rgba(232,160,32,0.4);
    margin-top: 0.75rem;
    transition: color 0.2s;
  }
  .trail-card:hover .trail-expand-hint,
  .trail-card.expanded .trail-expand-hint { color: var(--amber); }

  .no-results {
    grid-column: 1 / -1;
    text-align: center; padding: 4rem;
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 1.2rem; letter-spacing: 3px;
    color: rgba(240,232,216,0.2);
  }

  /* ── GAMES ── */
  #games { background: var(--sky-mid); position: relative; }
  .games-layout { display: flex; flex-direction: column; gap: 3rem; margin-top: 3rem; }
  .game-panel {
    background: rgba(255,255,255,0.03);
    border: 1px solid rgba(232,160,32,0.15);
    padding: 0;
    display: flex; flex-direction: column;
    clip-path: polygon(0 0, calc(100% - 20px) 0, 100% 20px, 100% 100%, 20px 100%, 0 calc(100% - 20px));
    overflow: hidden;
  }
  .game-header {
    padding: 1.5rem 2rem 1rem;
    border-bottom: 1px solid rgba(232,160,32,0.1);
    background: rgba(0,0,0,0.2);
  }
  .game-tag {
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.7rem; letter-spacing: 4px; text-transform: uppercase;
    color: var(--amber); margin-bottom: 0.5rem;
  }
  .game-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 2.4rem; letter-spacing: 2px; color: var(--cream);
  }
  .game-canvas-area {
    flex: 1; position: relative; min-height: 380px;
    background: #050d14;
    display: flex; align-items: center; justify-content: center;
  }
  canvas { display: block; }
  .game-controls {
    padding: 0.75rem 2rem;
    background: rgba(0,0,0,0.3);
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.75rem; letter-spacing: 1px;
    color: rgba(240,232,216,0.4);
    border-top: 1px solid rgba(232,160,32,0.1);
  }
  .game-controls kbd {
    background: rgba(232,160,32,0.15); border: 1px solid rgba(232,160,32,0.3);
    padding: 0.1rem 0.4rem; border-radius: 3px; font-size: 0.7rem;
    color: var(--amber);
  }

  /* ── FOOTER ── */
  footer {
    background: #070e17;
    border-top: 1px solid rgba(232,160,32,0.1);
    padding: 3rem 2.5rem;
    display: flex; flex-wrap: wrap; align-items: center; justify-content: space-between;
    gap: 1.5rem;
  }
  .footer-logo {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 2.5rem; letter-spacing: 4px; color: var(--amber);
  }
  .footer-links { display: flex; gap: 2rem; }
  .footer-links a {
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.8rem; letter-spacing: 2px; text-transform: uppercase;
    color: rgba(240,232,216,0.4); text-decoration: none; transition: color 0.2s;
  }
  .footer-links a:hover { color: var(--amber); }
  .footer-copy { font-size: 0.75rem; color: rgba(240,232,216,0.25); width: 100%; }

  /* ── ANIMATIONS ── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
  @keyframes scrollPulse {
    0%, 100% { opacity: 1; transform: scaleY(1); }
    50% { opacity: 0.3; transform: scaleY(0.6); }
  }
  @keyframes blink { 50% { opacity: 0; } }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <div class="logo">Ridge<span>Rush</span>.com</div>
  <ul>
    <li><a href="#trails">Trails</a></li>
    <li><a href="#games">Arcade</a></li>
    <li><a href="#hero">Home</a></li>
  </ul>
</nav>

<!-- HERO -->
<section id="hero">
  <div class="mountain-bg"></div>
  <div class="stars"></div>
  <svg class="mountains" viewBox="0 0 1440 500" xmlns="http://www.w3.org/2000/svg" preserveAspectRatio="none">
    <polygon points="0,500 200,220 400,320 600,180 800,280 1000,150 1200,260 1440,200 1440,500" fill="#1a3a28" opacity="0.5"/>
    <polygon points="0,500 150,300 350,380 550,240 750,360 950,200 1150,320 1300,260 1440,310 1440,500" fill="#1e4430" opacity="0.7"/>
    <polygon points="0,500 100,360 280,420 480,310 680,400 880,280 1080,380 1280,320 1440,370 1440,500" fill="#162d1e"/>
    <rect x="0" y="470" width="1440" height="30" fill="#0d1e10"/>
    <polygon points="600,180 570,220 630,220" fill="rgba(232,239,245,0.6)"/>
    <polygon points="1000,150 970,195 1030,195" fill="rgba(232,239,245,0.5)"/>
    <polygon points="200,220 175,255 225,255" fill="rgba(232,239,245,0.4)"/>
  </svg>
  <div class="hero-content">
    <p class="hero-eyebrow">Welcome to</p>
    <h1 class="hero-title">Ridge<span class="rush">Rush</span></h1>
    <p class="hero-sub">RIDE THE RIDGE · PLAY THE PEAK · EXPLORE THE EDGE</p>
    <div class="hero-ctas">
      <a href="#trails" class="btn btn-primary">View Trails</a>
      <a href="#games" class="btn btn-secondary">Play Games</a>
    </div>
  </div>
  <div class="scroll-hint">
    <span>Scroll</span>
    <div class="scroll-arrow"></div>
  </div>
</section>

<!-- TRAILS -->
<section id="trails">
  <div class="section-label">Trail Directory</div>
  <h2 class="section-title">Ride the<br>Ridge</h2>
  <div class="divider"></div>
  <p style="max-width:600px;color:rgba(240,232,216,0.65);font-size:0.95rem;line-height:1.8;margin-bottom:2.5rem;position:relative;z-index:1;">
    From iconic North American routes to every trail at Markham Park and Quiet Waters Park in Florida — your complete trail directory. Click any card for details.
  </p>

  <!-- Filters -->
  <div class="trail-filters">
    <input class="trail-search" type="text" id="trailSearch" placeholder="Search trails, parks, locations…" oninput="filterTrails()">
    <div class="filter-group">
      <span class="filter-label">Category:</span>
      <button class="filter-btn active" data-filter="cat" data-val="all" onclick="setFilter('cat','all',this)">All</button>
      <button class="filter-btn" data-filter="cat" data-val="northamerica" onclick="setFilter('cat','northamerica',this)">🌎 North America</button>
      <button class="filter-btn" data-filter="cat" data-val="markham" onclick="setFilter('cat','markham',this)">🌿 Markham Park</button>
      <button class="filter-btn" data-filter="cat" data-val="quietwaters" onclick="setFilter('cat','quietwaters',this)">💧 Quiet Waters</button>
    </div>
    <div class="filter-group">
      <span class="filter-label">Difficulty:</span>
      <button class="filter-btn active" data-filter="diff" data-val="all" onclick="setFilter('diff','all',this)">All</button>
      <button class="filter-btn" data-filter="diff" data-val="Easy" onclick="setFilter('diff','Easy',this)">Easy</button>
      <button class="filter-btn" data-filter="diff" data-val="Moderate" onclick="setFilter('diff','Moderate',this)">Moderate</button>
      <button class="filter-btn" data-filter="diff" data-val="Hard" onclick="setFilter('diff','Hard',this)">Hard</button>
    </div>
    <div class="filter-group">
      <span class="filter-label">Type:</span>
      <button class="filter-btn active" data-filter="type" data-val="all" onclick="setFilter('type','all',this)">All</button>
      <button class="filter-btn" data-filter="type" data-val="Hiking" onclick="setFilter('type','Hiking',this)">🥾 Hiking</button>
      <button class="filter-btn" data-filter="type" data-val="MTB" onclick="setFilter('type','MTB',this)">🚵 Mountain Biking</button>
    </div>
  </div>

  <div class="trail-count" id="trailCount"><span id="trailCountNum">50</span> trails shown</div>
  <div class="trails-grid" id="trailsGrid"></div>
</section>

<!-- GAMES -->
<section id="games">
  <div class="section-label">Ridge Arcade</div>
  <h2 class="section-title">Play the<br>Peak</h2>
  <div class="divider"></div>
  <p style="max-width:500px;color:rgba(240,232,216,0.65);font-size:0.95rem;line-height:1.8;">
    Two games, built right here on the mountain. Unwind at the lodge, or compete for the leaderboard on your phone. Fully playable below.
  </p>
  <div class="games-layout">
    <div class="game-panel">
      <div class="game-header">
        <div class="game-tag">Sandbox · Simulation · 188 Elements</div>
        <div class="game-title">⬡ Elemental</div>
      </div>
      <div style="position:relative;width:100%;height:700px;background:#07080c;">
        <iframe src="elemental.html" style="width:100%;height:100%;border:none;display:block;" title="Elemental Sandbox Game" allowfullscreen></iframe>
      </div>
      <div class="game-controls">Click/drag to place elements &nbsp;·&nbsp; 188+ real elements + special materials &nbsp;·&nbsp; Full Periodic Table included &nbsp;·&nbsp; Heat · Cool · Zap · Grind tools</div>
    </div>
    <div class="game-panel">
      <div class="game-header">
        <div class="game-tag">Arcade · Classic</div>
        <div class="game-title">Ridge Serpent</div>
      </div>
      <div class="game-canvas-area">
        <canvas id="serpentCanvas" width="400" height="340"></canvas>
      </div>
      <div class="game-controls">
        <kbd>↑</kbd><kbd>↓</kbd><kbd>←</kbd><kbd>→</kbd> to move &nbsp;·&nbsp; <kbd>Space</kbd> to start/pause &nbsp;·&nbsp; Score: <span id="serpentScore">0</span> &nbsp;·&nbsp; High: <span id="serpentHigh">0</span>
      </div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-logo">RidgeRush</div>
  <div class="footer-links">
    <a href="#trails">Trails</a>
    <a href="#games">Arcade</a>
    <a href="#">Trail Map</a>
    <a href="#">Contact</a>
  </div>
  <p class="footer-copy">© 2026 RidgeRush.com — All trails rated by difficulty. Ride at your own risk. Wear a helmet.</p>
</footer>

<script>
/* ══════════════════════════════════
   TRAIL DATA
══════════════════════════════════ */
const TRAILS = [
  // ── NORTH AMERICA ──
  { name:"Angels Landing", park:"Zion National Park", location:"Utah", difficulty:"Hard", distance:"5.4 mi", type:"Hiking", cat:"northamerica", desc:"Iconic chain-assisted scramble to a narrow sandstone ridge with 1,000-ft drop-offs and panoramic canyon views. Permit required." },
  { name:"The Narrows", park:"Zion National Park", location:"Utah", difficulty:"Moderate", distance:"9.6 mi", type:"Hiking", cat:"northamerica", desc:"Hike through the Virgin River as 1,000-ft canyon walls close in around you in Zion's legendary slot canyon." },
  { name:"Bright Angel Trail", park:"Grand Canyon NP", location:"Arizona", difficulty:"Hard", distance:"19 mi", type:"Hiking", cat:"northamerica", desc:"Descend into the Grand Canyon on this iconic trail with rest houses and water stations. Stunning layered geology." },
  { name:"South Kaibab Trail", park:"Grand Canyon NP", location:"Arizona", difficulty:"Hard", distance:"14.4 mi", type:"Hiking", cat:"northamerica", desc:"Ridge-top descent with the best panoramic views in the Grand Canyon. No shade or water — start early." },
  { name:"Half Dome Trail", park:"Yosemite NP", location:"California", difficulty:"Hard", distance:"16 mi", type:"Hiking", cat:"northamerica", desc:"Yosemite's signature hike climbs nearly 5,000 ft to a granite dome with an exposed cable section near the summit. Permit required." },
  { name:"Mist Trail to Nevada Fall", park:"Yosemite NP", location:"California", difficulty:"Moderate", distance:"7 mi", type:"Hiking", cat:"northamerica", desc:"Pass Vernal Fall and Nevada Fall on granite steps with spectacular spray. One of Yosemite's most rewarding day hikes." },
  { name:"Highline Trail", park:"Glacier NP", location:"Montana", difficulty:"Moderate", distance:"11.8 mi", type:"Hiking", cat:"northamerica", desc:"Traverse a ledge trail cut into the Garden Wall with sweeping Continental Divide views and frequent bighorn sheep sightings." },
  { name:"Appalachian Trail", park:"Multi-State", location:"Georgia to Maine", difficulty:"Hard", distance:"2,190 mi", type:"Hiking", cat:"northamerica", desc:"America's most famous long-distance trail spanning 14 states. Thru-hikers average 5–7 months. Roughly 3 million hikers enjoy sections each year." },
  { name:"Pacific Crest Trail", park:"Multi-State", location:"CA to Washington", difficulty:"Hard", distance:"2,650 mi", type:"Hiking", cat:"northamerica", desc:"Triple Crown trail running from the Mexican border to Canada through the Sierra Nevada and Cascades." },
  { name:"Continental Divide Trail", park:"Multi-State", location:"NM to Montana", difficulty:"Hard", distance:"3,100 mi", type:"Hiking", cat:"northamerica", desc:"The longest and most remote Triple Crown trail, following the Rocky Mountain spine through five states." },
  { name:"Emerald Lake Trail", park:"Rocky Mountain NP", location:"Colorado", difficulty:"Easy", distance:"3.6 mi", type:"Hiking", cat:"northamerica", desc:"Pass Dream Lake and Nymph Lake before reaching stunning alpine Emerald Lake. Best beginner hike in Rocky Mountain NP." },
  { name:"Observation Point", park:"Zion National Park", location:"Utah", difficulty:"Hard", distance:"8 mi", type:"Hiking", cat:"northamerica", desc:"Climb 2,000 ft for Zion's best summit view, looking down at Angels Landing from above." },
  { name:"West Rim Trail", park:"Zion National Park", location:"Utah", difficulty:"Hard", distance:"16 mi", type:"Hiking", cat:"northamerica", desc:"Long-distance rim traverse through the full length of Zion with dramatic canyon views and far fewer crowds." },
  { name:"The Enchantments", park:"Alpine Lakes Wilderness", location:"Washington", difficulty:"Hard", distance:"18.6 mi", type:"Hiking", cat:"northamerica", desc:"Point-to-point through alpine lakes, granite peaks, and golden larches. One of the most demanding hikes in the Pacific Northwest." },
  { name:"Rim-to-Rim", park:"Grand Canyon NP", location:"Arizona", difficulty:"Hard", distance:"24 mi", type:"Hiking", cat:"northamerica", desc:"Cross the entire Grand Canyon from South Rim to North Rim. Typically requires an overnight at Phantom Ranch." },
  { name:"Sliding Sands Trail", park:"Haleakalā NP", location:"Hawaii", difficulty:"Moderate", distance:"5 mi", type:"Hiking", cat:"northamerica", desc:"Descend into the volcanic crater of Haleakalā through an otherworldly alien landscape of shifting colored sands." },

  // ── MARKHAM PARK ──
  { name:"Nature Trail", park:"Markham Park", location:"Sunrise, FL", difficulty:"Easy", distance:"1.6 mi", type:"Hiking", cat:"markham", desc:"A birder's delight looping through pine forests with Everglades views from the levee. Includes the Silent Wings butterfly garden." },
  { name:"Lakeside Trail", park:"Markham Park", location:"Sunrise, FL", difficulty:"Easy", distance:"1.1 mi", type:"Hiking", cat:"markham", desc:"Linear footpath winding along the water's edge through dense Australian pines. Benches and a small dock provide lake views." },
  { name:"Conservation Levee Greenway", park:"Markham Park", location:"Sunrise, FL", difficulty:"Easy", distance:"Multi-mile", type:"Hiking", cat:"markham", desc:"Flat gravel-topped levee along the edge of the Everglades extending north toward Parkland. Outstanding birding and wildlife watching." },
  { name:"Warm Up Loop", park:"Markham Park", location:"Sunrise, FL", difficulty:"Easy", distance:"0.5 mi", type:"MTB", cat:"markham", desc:"The perfect intro to Markham's MTB system. Intermediate terrain with an advanced split-off near the start. Begins across from the pump track." },
  { name:"Deep Dark Forest", park:"Markham Park", location:"Sunrise, FL", difficulty:"Moderate", distance:"0.4 mi", type:"MTB", cat:"markham", desc:"Winding singletrack with plenty of roots. Connects to Rock Garden and can serve as a smoother bypass option." },
  { name:"Rock Garden", park:"Markham Park", location:"Sunrise, FL", difficulty:"Hard", distance:"0.3 mi", type:"MTB", cat:"markham", desc:"Technical rocky sections and challenging drops for riders looking to test their maneuvering skills. One of Markham's most beloved trails." },
  { name:"Armadillo", park:"Markham Park", location:"Sunrise, FL", difficulty:"Moderate", distance:"0.5 mi", type:"MTB", cat:"markham", desc:"Short climbs followed by fast, flowing berms. The trail with the most elevation gain at Markham at 33 ft." },
  { name:"Iguana Ridge", park:"Markham Park", location:"Sunrise, FL", difficulty:"Hard", distance:"0.2 mi", type:"MTB", cat:"markham", desc:"Advanced ridgeline with tight turns and an optional drop. A steep climb entry makes it demanding even for intermediate riders." },
  { name:"Iguana Return", park:"Markham Park", location:"Sunrise, FL", difficulty:"Hard", distance:"0.2 mi", type:"MTB", cat:"markham", desc:"The steepest trail at Markham Park at 3% average grade. Expert-level terrain that tests even seasoned riders." },
  { name:"OBX Advanced", park:"Markham Park", location:"Sunrise, FL", difficulty:"Hard", distance:"0.6 mi", type:"MTB", cat:"markham", desc:"The highest-rated trail at Markham Park. Expert-level singletrack with challenging features — the top choice for advanced riders." },
  { name:"Redback", park:"Markham Park", location:"Sunrise, FL", difficulty:"Hard", distance:"0.4 mi", type:"MTB", cat:"markham", desc:"The trail with the most descent at Markham (-25 ft). Fast descending singletrack rated among the park's very best." },
  { name:"Traverse Trail", park:"Markham Park", location:"Sunrise, FL", difficulty:"Moderate", distance:"0.5 mi", type:"MTB", cat:"markham", desc:"Third-highest rated trail at Markham. Connects key sections of the trail system heading left by the lake." },
  { name:"Area 51", park:"Markham Park", location:"Sunrise, FL", difficulty:"Hard", distance:"0.4 mi", type:"MTB", cat:"markham", desc:"Rock gardens, jumps and rapid berms make this a favorite for technical riders looking beyond the main loop." },
  { name:"Outback", park:"Markham Park", location:"Sunrise, FL", difficulty:"Hard", distance:"0.6 mi", type:"MTB", cat:"markham", desc:"Gut-buster climbs and an exciting outback extension. One of the park's most adventurous sections — described as 'REALLY fun'." },
  { name:"Gun Range", park:"Markham Park", location:"Sunrise, FL", difficulty:"Hard", distance:"1.3 mi", type:"MTB", cat:"markham", desc:"The longest trail at Markham at 1.3 miles and widely considered the most technical section in the park." },
  { name:"Pipeline", park:"Markham Park", location:"Sunrise, FL", difficulty:"Hard", distance:"0.2 mi", type:"MTB", cat:"markham", desc:"Features an optional wooden bridge and technical challenges designed to refine the skills of experienced riders." },
  { name:"Crime Scene", park:"Markham Park", location:"Sunrise, FL", difficulty:"Hard", distance:"0.3 mi", type:"MTB", cat:"markham", desc:"Steep technical climbs and descents. Connects to Jet Ski and Ted's Twisted Trail at the far end of the park." },
  { name:"Las Olas", park:"Markham Park", location:"Sunrise, FL", difficulty:"Moderate", distance:"0.1 mi", type:"MTB", cat:"markham", desc:"A 549 ft intermediate trail with flowing sections, quick transitions, and interesting obstacles for intermediate riders." },
  { name:"Jet Ski", park:"Markham Park", location:"Sunrise, FL", difficulty:"Hard", distance:"0.2 mi", type:"MTB", cat:"markham", desc:"You'll be zooming! A severe-difficulty trail featuring a 9m incline climb leading straight into a challenging drop." },
  { name:"Black Snake", park:"Markham Park", location:"Sunrise, FL", difficulty:"Hard", distance:"0.4 mi", type:"MTB", cat:"markham", desc:"Features the challenging Big Gulp section. Often combined with RTE 66 and Armadillo for a popular sequence." },
  { name:"RTE 66", park:"Markham Park", location:"Sunrise, FL", difficulty:"Moderate", distance:"0.3 mi", type:"MTB", cat:"markham", desc:"Fast, flowing trail commonly linked with Black Snake and Armadillo for a well-rounded loop through the park's best terrain." },
  { name:"Supercross", park:"Markham Park", location:"Sunrise, FL", difficulty:"Hard", distance:"0.3 mi", type:"MTB", cat:"markham", desc:"Among the trails with the biggest jumps at Markham Park. Fast, high-energy terrain that rewards speed." },
  { name:"Washing Machine", park:"Markham Park", location:"Sunrise, FL", difficulty:"Moderate", distance:"0.4 mi", type:"MTB", cat:"markham", desc:"Connects to Lost Ring and leads back toward the entrance — a useful return route after exploring the far end of the network." },
  { name:"Fishing Hole Loop", park:"Markham Park", location:"Sunrise, FL", difficulty:"Easy", distance:"0.5 mi", type:"MTB", cat:"markham", desc:"Scenic lakeside loop with wildlife sightings and a relaxed ride through open meadows near the water. Great for all skill levels." },
  { name:"Ted's Twisted Trail", park:"Markham Park", location:"Sunrise, FL", difficulty:"Hard", distance:"0.3 mi", type:"MTB", cat:"markham", desc:"Fast downhill with technical turns — don't carry too much speed or you can lose it easily. Located at the far end of the park." },

  // ── QUIET WATERS PARK ──
  { name:"Full MTB Loop", park:"Quiet Waters Park", location:"Deerfield Beach, FL", difficulty:"Easy", distance:"4.6 mi", type:"MTB", cat:"quietwaters", desc:"The main loop connecting singletrack trails with coral rock features, boardwalks, and optional advanced sections. Over 7 miles of total trails." },
  { name:"Paved Lakeside Path", park:"Quiet Waters Park", location:"Deerfield Beach, FL", difficulty:"Easy", distance:"2.1 mi", type:"Hiking", cat:"quietwaters", desc:"Accessible paved out-and-back path along the east side of the lake. Beautiful lake views. Wheelchair and stroller accessible." },
  { name:"Warm Up Trail", park:"Quiet Waters Park", location:"Deerfield Beach, FL", difficulty:"Easy", distance:"0.7 mi", type:"MTB", cat:"quietwaters", desc:"Green-rated singletrack at the entrance to the trail system. 3,596 ft long — can be ridden in both directions. Average completion: 2 minutes." },
  { name:"Corkscrew", park:"Quiet Waters Park", location:"Deerfield Beach, FL", difficulty:"Moderate", distance:"0.9 mi", type:"MTB", cat:"quietwaters", desc:"The longest individual trail at Quiet Waters at 4,751 ft. Most elevation gain and descent in the park — winding and technical." },
  { name:"Anaconda", park:"Quiet Waters Park", location:"Deerfield Beach, FL", difficulty:"Moderate", distance:"0.6 mi", type:"MTB", cat:"quietwaters", desc:"The highest-rated trail at Quiet Waters (4.1/5). Described as 'perfect for all riders' with numerous challenging features." },
  { name:"Power Drop", park:"Quiet Waters Park", location:"Deerfield Beach, FL", difficulty:"Hard", distance:"0.3 mi", type:"MTB", cat:"quietwaters", desc:"Technical drops make this a standout feature in the park's otherwise mostly flat terrain. The best-rated trail for technical challenge." },
  { name:"Horseshoe Extension", park:"Quiet Waters Park", location:"Deerfield Beach, FL", difficulty:"Moderate", distance:"0.4 mi", type:"MTB", cat:"quietwaters", desc:"The steepest trail at Quiet Waters with a 1.1% average grade. An extension loop adding variety and challenge to the main network." },
  { name:"Turnpike Extension", park:"Quiet Waters Park", location:"Deerfield Beach, FL", difficulty:"Moderate", distance:"0.5 mi", type:"MTB", cat:"quietwaters", desc:"Features notable boardwalk sections in the back of the park — one of the highlights for riders who love elevated wooden trail features." },
  { name:"Cool Down Trail", park:"Quiet Waters Park", location:"Deerfield Beach, FL", difficulty:"Easy", distance:"0.4 mi", type:"MTB", cat:"quietwaters", desc:"The natural ending to the full Quiet Waters loop. Helps riders wind down after the technical sections on the 8-mile full lap." },
  { name:"Eagle's Nest Nature Trail", park:"Quiet Waters Park", location:"Deerfield Beach, FL", difficulty:"Easy", distance:"1.0 mi", type:"Hiking", cat:"quietwaters", desc:"Interpretive nature walk through South Florida's diverse trees, plants, and animals. Perfect for families and nature enthusiasts of all ages." },
];

/* ══════════════════════════════════
   FILTER STATE
══════════════════════════════════ */
let activeFilters = { cat: 'all', diff: 'all', type: 'all' };

function setFilter(group, val, btn) {
  activeFilters[group] = val;
  // Update button states for that group
  document.querySelectorAll(`[data-filter="${group}"]`).forEach(b => {
    b.className = 'filter-btn';
    if (b.dataset.val === val) {
      if (group === 'cat' && val === 'markham') b.classList.add('active-cat-markham');
      else if (group === 'cat' && val === 'quietwaters') b.classList.add('active-cat-quietwaters');
      else if (group === 'cat' && val === 'northamerica') b.classList.add('active-cat-northamerica');
      else b.classList.add('active');
    }
  });
  filterTrails();
}

function filterTrails() {
  const q = document.getElementById('trailSearch').value.toLowerCase();
  const { cat, diff, type } = activeFilters;
  const results = TRAILS.filter(t => {
    const matchCat  = cat  === 'all' || t.cat === cat;
    const matchDiff = diff === 'all' || t.difficulty === diff;
    const matchType = type === 'all' || t.type === type;
    const matchQ = !q || t.name.toLowerCase().includes(q) || t.park.toLowerCase().includes(q) || t.location.toLowerCase().includes(q) || t.desc.toLowerCase().includes(q);
    return matchCat && matchDiff && matchType && matchQ;
  });
  renderTrails(results);
}

/* ══════════════════════════════════
   RENDER TRAILS
══════════════════════════════════ */
const diffMap = {
  'Easy':     { dot: 'green', bar: 'diff-green' },
  'Moderate': { dot: 'blue',  bar: 'diff-blue'  },
  'Hard':     { dot: 'red',   bar: 'diff-red'   },
};
const catBadge = {
  northamerica: '<span class="trail-category-badge cat-badge-northamerica">North America</span>',
  markham:      '<span class="trail-category-badge cat-badge-markham">Markham Park</span>',
  quietwaters:  '<span class="trail-category-badge cat-badge-quietwaters">Quiet Waters</span>',
};
const typeIcon = { Hiking: '🥾', MTB: '🚵' };

function renderTrails(list) {
  const grid = document.getElementById('trailsGrid');
  document.getElementById('trailCountNum').textContent = list.length;
  if (!list.length) {
    grid.innerHTML = '<div class="no-results">No trails match your filters</div>';
    return;
  }
  grid.innerHTML = list.map((t, i) => {
    const d = diffMap[t.difficulty] || diffMap['Moderate'];
    return `<div class="trail-card ${d.bar} cat-${t.cat}" onclick="toggleCard(this)">
      <div class="trail-badges">
        <span class="trail-difficulty"><span class="diff-dot ${d.dot}"></span>${t.difficulty}</span>
        ${catBadge[t.cat] || ''}
        <span class="trail-type-badge">${typeIcon[t.type] || ''} ${t.type}</span>
      </div>
      <div class="trail-name">${t.name}</div>
      <div class="trail-park">${t.park} &nbsp;·&nbsp; ${t.location}</div>
      <div class="trail-desc">${t.desc}</div>
      <div class="trail-stats">
        <div class="stat"><div class="stat-val">${t.distance}</div><div class="stat-key">Distance</div></div>
      </div>
      <div class="trail-expand-hint">▾ Tap for details</div>
    </div>`;
  }).join('');
}

function toggleCard(card) {
  card.classList.toggle('expanded');
  const hint = card.querySelector('.trail-expand-hint');
  hint.textContent = card.classList.contains('expanded') ? '▴ Close' : '▾ Tap for details';
}

// Initial render
renderTrails(TRAILS);

/* ══════════════════════════════════
   SERPENT GAME
══════════════════════════════════ */
(function() {
  const canvas = document.getElementById('serpentCanvas');
  const ctx = canvas.getContext('2d');
  const W = canvas.width, H = canvas.height;
  const CELL = 20;
  const COLS = W / CELL, ROWS = H / CELL;
  const scoreEl = document.getElementById('serpentScore');
  const highEl  = document.getElementById('serpentHigh');
  let snake, dir, nextDir, food, score, highScore = 0, running = false, gameOver = false, interval = null;

  function init() {
    snake = [{x:5,y:10},{x:4,y:10},{x:3,y:10}];
    dir = {x:1,y:0}; nextDir = {x:1,y:0};
    score = 0; gameOver = false;
    spawnFood(); scoreEl.textContent = 0; draw();
  }
  function spawnFood() {
    let pos;
    do { pos = {x: Math.floor(Math.random()*COLS), y: Math.floor(Math.random()*ROWS)}; }
    while (snake.some(s => s.x===pos.x && s.y===pos.y));
    food = pos;
  }
  function step() {
    dir = nextDir;
    const head = {x: snake[0].x + dir.x, y: snake[0].y + dir.y};
    if (head.x < 0 || head.x >= COLS || head.y < 0 || head.y >= ROWS || snake.some(s=>s.x===head.x&&s.y===head.y)) {
      endGame(); return;
    }
    snake.unshift(head);
    if (head.x === food.x && head.y === food.y) {
      score++; scoreEl.textContent = score;
      if (score > highScore) { highScore = score; highEl.textContent = highScore; }
      spawnFood();
    } else { snake.pop(); }
    draw();
  }
  function endGame() {
    running = false; gameOver = true; clearInterval(interval); draw();
  }
  function draw() {
    ctx.fillStyle = '#050d14'; ctx.fillRect(0, 0, W, H);
    ctx.strokeStyle = 'rgba(232,160,32,0.04)'; ctx.lineWidth = 0.5;
    for (let x = 0; x <= W; x += CELL) { ctx.beginPath(); ctx.moveTo(x,0); ctx.lineTo(x,H); ctx.stroke(); }
    for (let y = 0; y <= H; y += CELL) { ctx.beginPath(); ctx.moveTo(0,y); ctx.lineTo(W,y); ctx.stroke(); }
    if (!running && !gameOver) {
      ctx.fillStyle = 'rgba(232,160,32,0.08)'; ctx.fillRect(0,0,W,H);
      ctx.font = "bold 26px 'Bebas Neue', sans-serif"; ctx.fillStyle = '#E8A020'; ctx.textAlign = 'center';
      ctx.fillText('RIDGE SERPENT', W/2, H/2 - 20);
      ctx.font = "14px 'Barlow Condensed', sans-serif"; ctx.fillStyle = 'rgba(240,232,216,0.5)';
      ctx.fillText('Press SPACE to begin', W/2, H/2 + 15); ctx.textAlign = 'left'; return;
    }
    const t = Date.now() / 500;
    const pulse = 0.85 + 0.15 * Math.sin(t * Math.PI * 2);
    ctx.save(); ctx.translate(food.x * CELL + CELL/2, food.y * CELL + CELL/2);
    ctx.scale(pulse, pulse); ctx.fillStyle = '#FF6B2B';
    ctx.beginPath(); ctx.moveTo(0,-7); ctx.lineTo(7,0); ctx.lineTo(0,7); ctx.lineTo(-7,0);
    ctx.closePath(); ctx.fill(); ctx.restore();
    snake.forEach((seg, i) => {
      const isHead = i === 0;
      const ratio = 1 - (i / snake.length) * 0.5;
      const r = Math.round(45 + ratio * 15), g = Math.round(160 + ratio * 40), b = Math.round(60 + ratio * 20);
      ctx.fillStyle = isHead ? '#78e050' : `rgb(${r},${g},${b})`;
      const pad = isHead ? 1 : 2; const cornerR = isHead ? 4 : 3;
      roundRect(ctx, seg.x*CELL+pad, seg.y*CELL+pad, CELL-pad*2, CELL-pad*2, cornerR); ctx.fill();
      if (isHead) {
        ctx.fillStyle = '#050d14';
        ctx.fillRect(seg.x*CELL+5, seg.y*CELL+5, 3, 3);
        ctx.fillRect(seg.x*CELL+12, seg.y*CELL+5, 3, 3);
      }
    });
    if (gameOver) {
      ctx.fillStyle = 'rgba(5,13,20,0.75)'; ctx.fillRect(0,0,W,H);
      ctx.font = "bold 30px 'Bebas Neue', sans-serif"; ctx.fillStyle = '#FF6B2B'; ctx.textAlign = 'center';
      ctx.fillText('GAME OVER', W/2, H/2 - 25);
      ctx.font = "16px 'Barlow Condensed', sans-serif"; ctx.fillStyle = 'rgba(240,232,216,0.7)';
      ctx.fillText(`Score: ${score}   High: ${highScore}`, W/2, H/2 + 5);
      ctx.fillStyle = 'rgba(240,232,216,0.4)';
      ctx.fillText('Press SPACE to play again', W/2, H/2 + 30); ctx.textAlign = 'left';
    }
  }
  function roundRect(ctx, x, y, w, h, r) {
    ctx.beginPath();
    ctx.moveTo(x+r,y); ctx.lineTo(x+w-r,y); ctx.quadraticCurveTo(x+w,y,x+w,y+r);
    ctx.lineTo(x+w,y+h-r); ctx.quadraticCurveTo(x+w,y+h,x+w-r,y+h);
    ctx.lineTo(x+r,y+h); ctx.quadraticCurveTo(x,y+h,x,y+h-r);
    ctx.lineTo(x,y+r); ctx.quadraticCurveTo(x,y,x+r,y); ctx.closePath();
  }
  function startGame() {
    if (running) return; init(); running = true; clearInterval(interval); interval = setInterval(step, 140);
  }
  document.addEventListener('keydown', e => {
    if (e.code === 'Space') { e.preventDefault(); if (!running || gameOver) startGame(); }
    if (!running) return;
    if (e.key==='ArrowUp'    && dir.y!==1)  nextDir={x:0,y:-1};
    if (e.key==='ArrowDown'  && dir.y!==-1) nextDir={x:0,y:1};
    if (e.key==='ArrowLeft'  && dir.x!==1)  nextDir={x:-1,y:0};
    if (e.key==='ArrowRight' && dir.x!==-1) nextDir={x:1,y:0};
  });
  let touchStart = null;
  canvas.addEventListener('touchstart', e => { e.preventDefault(); touchStart={x:e.touches[0].clientX,y:e.touches[0].clientY}; if(!running||gameOver) startGame(); },{passive:false});
  canvas.addEventListener('touchend', e => {
    if (!touchStart||!running) return;
    const dx=e.changedTouches[0].clientX-touchStart.x, dy=e.changedTouches[0].clientY-touchStart.y;
    if (Math.abs(dx)>Math.abs(dy)) {
      if (dx>20&&dir.x!==-1) nextDir={x:1,y:0};
      if (dx<-20&&dir.x!==1) nextDir={x:-1,y:0};
    } else {
      if (dy>20&&dir.y!==-1) nextDir={x:0,y:1};
      if (dy<-20&&dir.y!==1) nextDir={x:0,y:-1};
    }
    touchStart=null;
  },{passive:false});
  function animateStart() { if (!running) { draw(); requestAnimationFrame(animateStart); } }
  init(); animateStart();
})();
</script>
</body>
</html>
