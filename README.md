<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>RidgeRush-MTB — Ride. Play. Explore.</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Barlow+Condensed:wght@300;400;600;700&family=Barlow:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --teal: #00b4a0;
    --teal-dark: #007a6e;
    --sand: #e8c97a;
    --coral: #ff6b4a;
    --sky-blue: #1a8fb5;
    --deep-ocean: #0a2a3a;
    --ocean-mid: #0d3348;
    --ocean-light: #0f4a60;
    --palm-green: #2d7a3a;
    --sunset-orange: #f0823a;
    --cream: #f0ece0;
    --amber: #e8a020;
    --ember: #ff6b2b;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }
  html { scroll-behavior: smooth; }
  body {
    background: var(--deep-ocean);
    color: var(--cream);
    font-family: 'Barlow', sans-serif;
    overflow-x: hidden;
  }

  /* ── NAV ── */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 1000;
    display: flex; align-items: center; justify-content: space-between;
    padding: 1rem 2.5rem;
    background: rgba(10,42,58,0.88);
    backdrop-filter: blur(14px);
    border-bottom: 1px solid rgba(0,180,160,0.25);
  }
  .logo {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 1.9rem; letter-spacing: 3px;
    color: var(--teal);
    text-shadow: 0 0 22px rgba(0,180,160,0.5);
  }
  .logo .dash { color: var(--sand); }
  .logo .mtb  { color: var(--coral); }
  nav ul { list-style: none; display: flex; gap: 2rem; }
  nav ul a {
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.95rem; font-weight: 600; letter-spacing: 2px;
    color: var(--cream); text-decoration: none; text-transform: uppercase;
    transition: color 0.2s;
  }
  nav ul a:hover { color: var(--teal); }

  /* ── HERO ── */
  #hero {
    height: 100vh; position: relative; overflow: hidden;
    display: flex; flex-direction: column; align-items: center; justify-content: center;
  }

  /* Florida sky gradient */
  .hero-bg {
    position: absolute; inset: 0;
    background: linear-gradient(
      to bottom,
      #0a1a2e 0%,
      #0d2d4a 20%,
      #0e3d60 38%,
      #1a6888 50%,
      #2496c0 62%,
      #1a7a9e 72%,
      #0e4a6a 82%,
      #0a2a3a 100%
    );
  }

  /* Animated sun / sunset glow */
  .sun {
    position: absolute;
    width: 160px; height: 160px;
    border-radius: 50%;
    background: radial-gradient(circle, #ffe066 0%, #ffb830 40%, #ff7a20 70%, transparent 100%);
    bottom: 38%; left: 50%; transform: translateX(-50%);
    box-shadow: 0 0 80px 40px rgba(255,180,40,0.22), 0 0 200px 100px rgba(255,120,20,0.10);
    opacity: 0.85;
  }
  .sun-glow {
    position: absolute;
    width: 600px; height: 300px;
    border-radius: 50%;
    background: radial-gradient(ellipse, rgba(255,160,40,0.18) 0%, transparent 70%);
    bottom: 35%; left: 50%; transform: translateX(-50%);
  }

  /* Ocean water with shimmer */
  .ocean {
    position: absolute; bottom: 0; left: 0; right: 0; height: 42%;
    background: linear-gradient(
      to bottom,
      #1a8fb5 0%,
      #0e6080 30%,
      #0a3a55 70%,
      #071e2e 100%
    );
    overflow: hidden;
  }
  .ocean::before {
    content: '';
    position: absolute; top: 0; left: -100%; right: -100%; height: 4px;
    background: linear-gradient(to right, transparent, rgba(255,255,255,0.3), rgba(255,230,100,0.4), rgba(255,255,255,0.3), transparent);
    animation: shimmer 4s linear infinite;
  }
  .wave {
    position: absolute; left: -100%; right: -100%; height: 12px;
    border-radius: 50%;
    background: rgba(255,255,255,0.06);
    animation: wave 6s ease-in-out infinite;
  }
  .wave:nth-child(2) { top: 18%; animation-delay: -2s; animation-duration: 8s; height: 8px; opacity: 0.5; }
  .wave:nth-child(3) { top: 40%; animation-delay: -4s; animation-duration: 10s; height: 6px; opacity: 0.3; }

  /* Sun reflection on water */
  .sun-reflection {
    position: absolute; top: 0; left: 50%; transform: translateX(-50%);
    width: 120px; height: 100%;
    background: linear-gradient(to bottom, rgba(255,200,60,0.25), rgba(255,150,30,0.08), transparent);
    clip-path: polygon(30% 0%, 70% 0%, 100% 100%, 0% 100%);
  }

  /* Palm trees SVG silhouettes */
  .palms {
    position: absolute; bottom: 40%; left: 0; right: 0;
    pointer-events: none;
  }

  /* Stars */
  .stars {
    position: absolute; inset: 0; top: 0; height: 55%;
    background-image:
      radial-gradient(1px 1px at 8% 10%, rgba(255,255,255,0.9), transparent),
      radial-gradient(1px 1px at 22% 6%, rgba(255,255,255,0.7), transparent),
      radial-gradient(1.5px 1.5px at 38% 14%, rgba(255,255,255,0.85), transparent),
      radial-gradient(1px 1px at 55% 4%, rgba(255,255,255,0.6), transparent),
      radial-gradient(1px 1px at 72% 12%, rgba(255,255,255,0.8), transparent),
      radial-gradient(1px 1px at 88% 8%, rgba(255,255,255,0.7), transparent),
      radial-gradient(1px 1px at 15% 22%, rgba(255,255,255,0.5), transparent),
      radial-gradient(1px 1px at 65% 18%, rgba(255,255,255,0.6), transparent),
      radial-gradient(2px 2px at 45% 9%, rgba(255,230,180,0.7), transparent);
  }

  .hero-content {
    position: relative; z-index: 10;
    text-align: center; padding: 0 1rem;
    margin-bottom: 8rem;
  }
  .hero-eyebrow {
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.85rem; letter-spacing: 5px; text-transform: uppercase;
    color: var(--teal); margin-bottom: 1rem;
    opacity: 0; animation: fadeUp 0.8s 0.3s forwards;
  }
  .hero-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(4rem, 12vw, 10rem);
    letter-spacing: 6px; line-height: 0.9;
    color: var(--cream);
    text-shadow: 0 4px 40px rgba(0,0,0,0.6), 0 0 80px rgba(0,180,160,0.2);
    opacity: 0; animation: fadeUp 0.8s 0.5s forwards;
  }
  .hero-title .dash-mtb { color: var(--coral); }
  .hero-sub {
    font-size: 1rem; font-weight: 300; letter-spacing: 3px;
    color: rgba(240,236,224,0.65); margin-top: 1.2rem;
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
    background: var(--teal); color: var(--deep-ocean);
    clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%);
  }
  .btn-primary:hover { background: var(--coral); transform: translateY(-2px); }
  .btn-secondary {
    background: transparent; color: var(--cream);
    border: 1.5px solid rgba(240,236,224,0.35);
    clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%);
  }
  .btn-secondary:hover { border-color: var(--teal); color: var(--teal); }
  .scroll-hint {
    position: absolute; bottom: 2rem; left: 50%; transform: translateX(-50%);
    display: flex; flex-direction: column; align-items: center; gap: 0.5rem;
    opacity: 0; animation: fadeIn 1s 1.5s forwards; z-index: 10;
  }
  .scroll-hint span {
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.7rem; letter-spacing: 3px; color: rgba(240,236,224,0.4);
  }
  .scroll-arrow {
    width: 1px; height: 40px;
    background: linear-gradient(to bottom, var(--teal), transparent);
    animation: scrollPulse 1.5s infinite;
  }

  /* ── SECTION COMMONS ── */
  section { padding: 6rem 2.5rem; }
  .section-label {
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.75rem; letter-spacing: 5px; text-transform: uppercase;
    color: var(--teal); margin-bottom: 0.75rem;
  }
  .section-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(3rem, 7vw, 5.5rem);
    line-height: 0.95; letter-spacing: 2px;
  }
  .divider {
    width: 60px; height: 3px;
    background: linear-gradient(to right, var(--teal), var(--coral));
    margin: 1.5rem 0 2.5rem;
  }

  /* ── PRACTICE AREAS ── */
  #practice {
    background: linear-gradient(160deg, #071e2e 0%, #0a2d3e 40%, #0d3a28 100%);
    position: relative; overflow: hidden;
  }
  #practice::before {
    content: '';
    position: absolute; inset: 0;
    background-image: repeating-linear-gradient(
      -45deg, transparent, transparent 50px,
      rgba(0,180,160,0.04) 50px, rgba(0,180,160,0.04) 51px
    );
  }
  .practice-intro {
    max-width: 640px; color: rgba(240,236,224,0.65); font-size: 0.95rem;
    line-height: 1.8; margin-bottom: 2.5rem; position: relative; z-index: 1;
  }
  .practice-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 1.2rem; position: relative; z-index: 1;
  }
  .practice-card {
    background: rgba(10,30,40,0.75);
    border: 1px solid rgba(0,180,160,0.15);
    padding: 1.6rem;
    position: relative; overflow: hidden;
    clip-path: polygon(0 0, calc(100% - 14px) 0, 100% 14px, 100% 100%, 14px 100%, 0 calc(100% - 14px));
    transition: transform 0.25s, border-color 0.25s;
  }
  .practice-card:hover { transform: translateY(-3px); border-color: rgba(0,180,160,0.4); }
  .practice-card::before {
    content: ''; position: absolute; top: 0; left: 0; right: 0; height: 3px;
  }
  .practice-card.type-pump::before    { background: linear-gradient(to right, var(--teal), #00d4bb); }
  .practice-card.type-skills::before  { background: linear-gradient(to right, var(--sky-blue), #4ab8e0); }
  .practice-card.type-jumps::before   { background: linear-gradient(to right, var(--coral), #ff9060); }
  .practice-card.type-rock::before    { background: linear-gradient(to right, #8b7355, #c4a870); }
  .practice-card.type-freeride::before{ background: linear-gradient(to right, var(--sunset-orange), #ffb840); }
  .practice-card.type-wash::before    { background: linear-gradient(to right, #3a8fd5, #70c0f0); }
  .practice-icon {
    font-size: 2.2rem; margin-bottom: 0.8rem; display: block;
  }
  .practice-name {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 1.5rem; letter-spacing: 1px; color: var(--cream);
    margin-bottom: 0.3rem; line-height: 1;
  }
  .practice-tag {
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.65rem; letter-spacing: 3px; text-transform: uppercase;
    color: var(--teal); margin-bottom: 0.75rem;
  }
  .practice-desc {
    font-size: 0.84rem; line-height: 1.68; color: rgba(240,236,224,0.58);
  }
  .practice-features {
    margin-top: 1rem; display: flex; flex-wrap: wrap; gap: 0.4rem;
  }
  .pf-chip {
    font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.62rem; letter-spacing: 1.5px; text-transform: uppercase;
    padding: 0.2rem 0.65rem;
    background: rgba(0,180,160,0.1);
    border: 1px solid rgba(0,180,160,0.2);
    color: rgba(240,236,224,0.55);
    border-radius: 2px;
  }

  /* ── TRAILS ── */
  #trails {
    background: linear-gradient(160deg, #071e2e 0%, #0a3040 50%, #071520 100%);
    position: relative; overflow: hidden;
  }
  #trails::before {
    content: '';
    position: absolute; inset: 0;
    background-image: repeating-linear-gradient(
      45deg, transparent, transparent 40px,
      rgba(0,180,160,0.04) 40px, rgba(0,180,160,0.04) 41px
    );
  }

  /* FILTERS */
  .trail-filters { display: flex; flex-wrap: wrap; gap: 0.6rem; margin-bottom: 1.5rem; position: relative; z-index: 1; align-items: center; }
  .filter-group { display: flex; gap: 0.4rem; align-items: center; flex-wrap: wrap; }
  .filter-label { font-family: 'Barlow Condensed', sans-serif; font-size: 0.7rem; letter-spacing: 3px; text-transform: uppercase; color: rgba(240,236,224,0.35); margin-right: 0.2rem; }
  .filter-btn { font-family: 'Barlow Condensed', sans-serif; font-size: 0.75rem; font-weight: 700; letter-spacing: 2px; text-transform: uppercase; padding: 0.4rem 1rem; background: rgba(255,255,255,0.04); border: 1px solid rgba(240,236,224,0.12); color: rgba(240,236,224,0.5); cursor: pointer; transition: all 0.2s; clip-path: polygon(6px 0%, 100% 0%, calc(100% - 6px) 100%, 0% 100%); }
  .filter-btn:hover { border-color: var(--teal); color: var(--teal); }
  .filter-btn.active { background: rgba(0,180,160,0.15); border-color: var(--teal); color: var(--teal); }
  .filter-btn.active-markham { background: rgba(45,210,140,0.12); border-color: #2dd28c; color: #2dd28c; }
  .filter-btn.active-quietwaters { background: rgba(70,160,240,0.12); border-color: #46a0f0; color: #46a0f0; }
  .filter-btn.active-northamerica { background: rgba(240,130,60,0.12); border-color: var(--coral); color: var(--coral); }
  .trail-search { font-family: 'Barlow Condensed', sans-serif; font-size: 0.85rem; letter-spacing: 1px; padding: 0.5rem 1.2rem; background: rgba(255,255,255,0.05); border: 1px solid rgba(240,236,224,0.12); color: var(--cream); outline: none; transition: border-color 0.2s; min-width: 220px; clip-path: polygon(6px 0%, 100% 0%, calc(100% - 6px) 100%, 0% 100%); }
  .trail-search::placeholder { color: rgba(240,236,224,0.3); }
  .trail-search:focus { border-color: var(--teal); }
  .trail-count { font-family: 'Barlow Condensed', sans-serif; font-size: 0.8rem; letter-spacing: 2px; color: rgba(240,236,224,0.3); margin-bottom: 1.5rem; position: relative; z-index: 1; }
  .trail-count span { color: var(--teal); }

  /* GRID */
  .trails-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 1.2rem; position: relative; z-index: 1; }
  .trail-card { background: rgba(8,24,36,0.8); border: 1px solid rgba(0,180,160,0.12); padding: 1.5rem; position: relative; overflow: hidden; transition: transform 0.25s, border-color 0.25s, box-shadow 0.25s; clip-path: polygon(0 0, calc(100% - 14px) 0, 100% 14px, 100% 100%, 14px 100%, 0 calc(100% - 14px)); cursor: pointer; }
  .trail-card:hover { transform: translateY(-4px); border-color: rgba(0,180,160,0.4); box-shadow: 0 10px 35px rgba(0,0,0,0.5); }
  .trail-card::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 3px; }
  .trail-card.diff-green::before  { background: #2dd28c; }
  .trail-card.diff-blue::before   { background: #46a0f0; }
  .trail-card.diff-red::before    { background: var(--coral); }
  .trail-card.diff-black::before  { background: #666; }
  .trail-card::after { content: ''; position: absolute; top: 0; left: 0; bottom: 0; width: 3px; }
  .trail-card.cat-markham::after      { background: #2dd28c; }
  .trail-card.cat-quietwaters::after  { background: #46a0f0; }
  .trail-card.cat-northamerica::after { background: var(--coral); }
  .trail-badges { display: flex; gap: 0.4rem; flex-wrap: wrap; margin-bottom: 0.65rem; align-items: center; }
  .trail-diff-label { display: inline-flex; align-items: center; gap: 0.4rem; font-family: 'Barlow Condensed', sans-serif; font-size: 0.68rem; font-weight: 700; letter-spacing: 2px; text-transform: uppercase; }
  .diff-dot { width: 9px; height: 9px; border-radius: 50%; flex-shrink: 0; }
  .diff-dot.green { background: #2dd28c; }
  .diff-dot.blue  { background: #46a0f0; }
  .diff-dot.red   { background: var(--coral); }
  .diff-dot.black { background: #888; }
  .cat-badge { font-family: 'Barlow Condensed', sans-serif; font-size: 0.62rem; letter-spacing: 2px; text-transform: uppercase; padding: 0.12rem 0.55rem; border-radius: 2px; }
  .cat-badge.markham     { background: rgba(45,210,140,0.1);  color: #2dd28c; border: 1px solid rgba(45,210,140,0.25); }
  .cat-badge.quietwaters { background: rgba(70,160,240,0.1);  color: #46a0f0; border: 1px solid rgba(70,160,240,0.25); }
  .cat-badge.northamerica{ background: rgba(255,107,74,0.1);  color: var(--coral); border: 1px solid rgba(255,107,74,0.25); }
  .trail-name { font-family: 'Bebas Neue', sans-serif; font-size: 1.6rem; letter-spacing: 1px; color: var(--cream); margin-bottom: 0.2rem; line-height: 1; }
  .trail-park { font-family: 'Barlow Condensed', sans-serif; font-size: 0.72rem; letter-spacing: 1px; color: rgba(240,236,224,0.32); margin-bottom: 0.7rem; }
  .trail-stat-row { display: flex; gap: 1.2rem; flex-wrap: wrap; margin-bottom: 0.6rem; }
  .stat { display: flex; flex-direction: column; gap: 0.05rem; }
  .stat-val { font-family: 'Bebas Neue', sans-serif; font-size: 1.15rem; letter-spacing: 1px; color: var(--teal); }
  .stat-key { font-family: 'Barlow Condensed', sans-serif; font-size: 0.58rem; letter-spacing: 2px; text-transform: uppercase; color: rgba(240,236,224,0.3); }
  .trail-map-hint { font-family: 'Barlow Condensed', sans-serif; font-size: 0.65rem; letter-spacing: 2px; text-transform: uppercase; color: rgba(0,180,160,0.45); margin-top: 0.6rem; transition: color 0.2s; }
  .trail-card:hover .trail-map-hint { color: var(--teal); }
  .no-results { grid-column: 1/-1; text-align: center; padding: 4rem; font-family: 'Barlow Condensed', sans-serif; font-size: 1.2rem; letter-spacing: 3px; color: rgba(240,236,224,0.2); }

  /* MAP MODAL */
  .modal-overlay { position: fixed; inset: 0; z-index: 2000; background: rgba(5,10,18,0.93); display: flex; align-items: center; justify-content: center; opacity: 0; pointer-events: none; transition: opacity 0.25s; backdrop-filter: blur(8px); }
  .modal-overlay.open { opacity: 1; pointer-events: all; }
  .modal-box { background: #071520; border: 1px solid rgba(0,180,160,0.28); width: min(96vw,980px); max-height: 93vh; display: flex; flex-direction: column; clip-path: polygon(0 0,calc(100% - 22px) 0,100% 22px,100% 100%,22px 100%,0 calc(100% - 22px)); overflow: hidden; transform: scale(0.94); transition: transform 0.25s; }
  .modal-overlay.open .modal-box { transform: scale(1); }
  .modal-header { padding: 1.2rem 1.8rem; border-bottom: 1px solid rgba(0,180,160,0.12); background: rgba(0,0,0,0.35); display: flex; align-items: flex-start; justify-content: space-between; gap: 1rem; flex-shrink: 0; }
  .modal-title { font-family: 'Bebas Neue', sans-serif; font-size: 2.2rem; letter-spacing: 2px; color: var(--cream); line-height: 1; }
  .modal-sub { font-family: 'Barlow Condensed', sans-serif; font-size: 0.75rem; letter-spacing: 2px; color: rgba(240,236,224,0.38); margin-top: 0.3rem; }
  .modal-badges { display: flex; gap: 0.5rem; flex-wrap: wrap; margin-top: 0.5rem; align-items: center; }
  .modal-close { background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.12); color: rgba(240,236,224,0.55); font-family: 'Barlow Condensed', sans-serif; font-size: 0.8rem; letter-spacing: 2px; padding: 0.4rem 0.9rem; cursor: pointer; transition: all 0.2s; flex-shrink: 0; margin-top: 0.2rem; }
  .modal-close:hover { border-color: var(--teal); color: var(--teal); }
  .modal-body { flex: 1; overflow: auto; display: flex; flex-direction: column; }
  .modal-stats { display: flex; gap: 2rem; flex-wrap: wrap; padding: 0.9rem 1.8rem; border-bottom: 1px solid rgba(0,180,160,0.08); background: rgba(0,0,0,0.2); }
  .modal-desc { padding: 1rem 1.8rem; font-size: 0.875rem; line-height: 1.75; color: rgba(240,236,224,0.58); border-bottom: 1px solid rgba(0,180,160,0.07); }
  .modal-map { flex: 1; min-height: 400px; background: #071520; }
  .modal-map iframe { width: 100%; height: 100%; min-height: 400px; border: none; display: block; }

  /* GAMES */
  #games { background: linear-gradient(160deg, #07101a 0%, #0a1e2e 100%); position: relative; }
  .games-layout { display: flex; flex-direction: column; gap: 3rem; margin-top: 3rem; }
  .game-panel { background: rgba(255,255,255,0.03); border: 1px solid rgba(0,180,160,0.15); padding: 0; display: flex; flex-direction: column; clip-path: polygon(0 0,calc(100% - 20px) 0,100% 20px,100% 100%,20px 100%,0 calc(100% - 20px)); overflow: hidden; }
  .game-header { padding: 1.5rem 2rem 1rem; border-bottom: 1px solid rgba(0,180,160,0.1); background: rgba(0,0,0,0.2); }
  .game-tag { font-family: 'Barlow Condensed', sans-serif; font-size: 0.7rem; letter-spacing: 4px; text-transform: uppercase; color: var(--teal); margin-bottom: 0.5rem; }
  .game-title { font-family: 'Bebas Neue', sans-serif; font-size: 2.4rem; letter-spacing: 2px; color: var(--cream); }
  .game-canvas-area { flex: 1; position: relative; min-height: 380px; background: #050d14; display: flex; align-items: center; justify-content: center; }
  canvas { display: block; }
  .game-controls { padding: 0.75rem 2rem; background: rgba(0,0,0,0.3); font-family: 'Barlow Condensed', sans-serif; font-size: 0.75rem; letter-spacing: 1px; color: rgba(240,236,224,0.4); border-top: 1px solid rgba(0,180,160,0.1); }
  .game-controls kbd { background: rgba(0,180,160,0.15); border: 1px solid rgba(0,180,160,0.3); padding: 0.1rem 0.4rem; border-radius: 3px; font-size: 0.7rem; color: var(--teal); }




  /* D-PAD */
  .dpad { display:grid; grid-template-columns:repeat(3,44px); grid-template-rows:repeat(3,44px); gap:4px; margin:0.8rem auto 0; justify-content:center; }
  .dpad-btn { background:rgba(0,180,160,0.12); border:1px solid rgba(0,180,160,0.25); color:var(--teal); font-size:1.1rem; cursor:pointer; border-radius:4px; display:flex; align-items:center; justify-content:center; user-select:none; transition:background 0.15s; }
  .dpad-btn:active { background:rgba(0,180,160,0.35); }
  .dpad-center { background:transparent; border:none; cursor:default; }
  /* FULLSCREEN */
  .game-panel { position: relative; }
  .fs-btn {
    position: absolute; top: 1.1rem; right: 1.2rem;
    background: rgba(0,180,160,0.12); border: 1px solid rgba(0,180,160,0.3);
    color: var(--teal); font-family: 'Barlow Condensed', sans-serif;
    font-size: 0.68rem; letter-spacing: 2px; text-transform: uppercase;
    padding: 0.35rem 0.85rem; cursor: pointer; z-index: 10;
    transition: all 0.2s;
    clip-path: polygon(5px 0%, 100% 0%, calc(100% - 5px) 100%, 0% 100%);
  }
  .fs-btn:hover { background: rgba(0,180,160,0.28); border-color: var(--teal); }
  .game-panel:-webkit-full-screen { background: #050d14; display: flex; flex-direction: column; }
  .game-panel:-moz-full-screen    { background: #050d14; display: flex; flex-direction: column; }
  .game-panel:fullscreen           { background: #050d14; display: flex; flex-direction: column; }
  .game-panel:fullscreen .game-canvas-area,
  .game-panel:-webkit-full-screen .game-canvas-area,
  .game-panel:-moz-full-screen .game-canvas-area {
    flex: 1; display: flex; align-items: center; justify-content: center;
  }
  .game-panel:fullscreen canvas,
  .game-panel:-webkit-full-screen canvas,
  .game-panel:-moz-full-screen canvas {
    max-width: 100%; max-height: 100%; object-fit: contain;
  }
  .game-panel:fullscreen .fs-btn,
  .game-panel:-webkit-full-screen .fs-btn,
  .game-panel:-moz-full-screen .fs-btn { top: 1rem; right: 1rem; }
  /* CONTACT */
  #contact { background: linear-gradient(160deg, #040c14 0%, #071520 60%, #0a2a1a 100%); position: relative; overflow: hidden; }
  #contact::before { content:''; position:absolute; inset:0; background-image: repeating-linear-gradient(-45deg, transparent, transparent 60px, rgba(0,180,160,0.03) 60px, rgba(0,180,160,0.03) 61px); }
  .contact-grid { display:grid; grid-template-columns:repeat(auto-fit,minmax(260px,1fr)); gap:1.5rem; margin-top:2.5rem; position:relative; z-index:1; }
  .contact-card { background:rgba(10,30,40,0.8); border:1px solid rgba(0,180,160,0.15); padding:2rem 1.8rem; clip-path:polygon(0 0,calc(100% - 14px) 0,100% 14px,100% 100%,14px 100%,0 calc(100% - 14px)); transition:transform 0.25s,border-color 0.25s; text-decoration:none; display:block; }
  .contact-card:hover { transform:translateY(-4px); border-color:rgba(0,180,160,0.4); }
  .contact-card::before { content:''; position:absolute; top:0; left:0; right:0; height:3px; }
  .contact-card.c-email::before   { background:linear-gradient(to right,var(--teal),#00d4bb); }
  .contact-card.c-phone::before   { background:linear-gradient(to right,var(--coral),#ff9060); }
  .contact-card.c-youtube::before { background:linear-gradient(to right,#ff0000,#ff6060); }
  .contact-icon { font-size:2.8rem; margin-bottom:1rem; display:block; }
  .contact-label { font-family:'Barlow Condensed',sans-serif; font-size:0.7rem; letter-spacing:4px; text-transform:uppercase; color:var(--teal); margin-bottom:0.4rem; }
  .contact-value { font-family:'Bebas Neue',sans-serif; font-size:1.6rem; letter-spacing:1px; color:var(--cream); line-height:1.1; word-break:break-all; }
  .contact-sub { font-family:'Barlow Condensed',sans-serif; font-size:0.75rem; letter-spacing:1px; color:rgba(240,236,224,0.35); margin-top:0.5rem; }
  /* FOOTER */
  footer { background: #040c14; border-top: 1px solid rgba(0,180,160,0.1); padding: 3rem 2.5rem; display: flex; flex-wrap: wrap; align-items: center; justify-content: space-between; gap: 1.5rem; }
  .footer-logo { font-family: 'Bebas Neue', sans-serif; font-size: 2.2rem; letter-spacing: 3px; color: var(--teal); }
  .footer-logo .dash { color: var(--sand); }
  .footer-logo .mtb  { color: var(--coral); }
  .footer-links { display: flex; gap: 2rem; }
  .footer-links a { font-family: 'Barlow Condensed', sans-serif; font-size: 0.8rem; letter-spacing: 2px; text-transform: uppercase; color: rgba(240,236,224,0.4); text-decoration: none; transition: color 0.2s; }
  .footer-links a:hover { color: var(--teal); }
  .footer-copy { font-size: 0.75rem; color: rgba(240,236,224,0.2); width: 100%; }

  @keyframes fadeUp   { from { opacity:0; transform:translateY(24px); } to { opacity:1; transform:translateY(0); } }
  @keyframes fadeIn   { from { opacity:0; } to { opacity:1; } }
  @keyframes scrollPulse { 0%,100% { opacity:1; } 50% { opacity:0.3; } }
  @keyframes shimmer  { from { transform: translateX(0); } to { transform: translateX(50%); } }
  @keyframes wave     { 0%,100% { transform: translateX(0); } 50% { transform: translateX(5%); } }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <div class="logo">RidgeRush<span class="dash">-</span><span class="mtb">MTB</span></div>
  <ul>
    <li><a href="#practice">Skills Areas</a></li>
    <li><a href="#trails">Trails</a></li>
    <li><a href="#games">Arcade</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>

<!-- HERO -->
<section id="hero">
  <div class="hero-bg"></div>
  <div class="stars"></div>
  <div class="sun"></div>
  <div class="sun-glow"></div>

  <!-- Palm trees SVG -->
  <svg class="palms" viewBox="0 0 1440 280" xmlns="http://www.w3.org/2000/svg" preserveAspectRatio="none" style="position:absolute;bottom:38%;left:0;right:0;z-index:3;">
    <!-- Left palm -->
    <g opacity="0.9">
      <path d="M80,280 Q85,200 90,160" stroke="#1a3d1a" stroke-width="8" fill="none" stroke-linecap="round"/>
      <path d="M90,160 Q60,130 20,125" stroke="#1a3d1a" stroke-width="5" fill="none"/>
      <path d="M90,160 Q55,145 30,155" stroke="#1a3d1a" stroke-width="4" fill="none"/>
      <path d="M90,160 Q75,135 55,120" stroke="#1a3d1a" stroke-width="4" fill="none"/>
      <path d="M90,160 Q110,130 140,128" stroke="#1a3d1a" stroke-width="4" fill="none"/>
      <path d="M90,160 Q105,148 125,155" stroke="#1a3d1a" stroke-width="3" fill="none"/>
      <ellipse cx="20" cy="124" rx="22" ry="8" fill="#1d5c1d" transform="rotate(-15,20,124)"/>
      <ellipse cx="30" cy="154" rx="20" ry="7" fill="#1d5c1d" transform="rotate(10,30,154)"/>
      <ellipse cx="55" cy="119" rx="20" ry="7" fill="#1d5c1d" transform="rotate(-25,55,119)"/>
      <ellipse cx="140" cy="127" rx="22" ry="8" fill="#1d5c1d" transform="rotate(20,140,127)"/>
      <ellipse cx="125" cy="154" rx="18" ry="7" fill="#1d5c1d" transform="rotate(15,125,154)"/>
    </g>
    <!-- Right palm -->
    <g opacity="0.9">
      <path d="M1360,280 Q1355,195 1348,150" stroke="#1a3d1a" stroke-width="8" fill="none" stroke-linecap="round"/>
      <path d="M1348,150 Q1380,120 1420,118" stroke="#1a3d1a" stroke-width="5" fill="none"/>
      <path d="M1348,150 Q1385,138 1415,148" stroke="#1a3d1a" stroke-width="4" fill="none"/>
      <path d="M1348,150 Q1370,122 1400,115" stroke="#1a3d1a" stroke-width="4" fill="none"/>
      <path d="M1348,150 Q1315,120 1285,118" stroke="#1a3d1a" stroke-width="4" fill="none"/>
      <path d="M1348,150 Q1325,140 1305,148" stroke="#1a3d1a" stroke-width="3" fill="none"/>
      <ellipse cx="1420" cy="117" rx="22" ry="8" fill="#1d5c1d" transform="rotate(15,1420,117)"/>
      <ellipse cx="1415" cy="147" rx="20" ry="7" fill="#1d5c1d" transform="rotate(-10,1415,147)"/>
      <ellipse cx="1400" cy="114" rx="20" ry="7" fill="#1d5c1d" transform="rotate(25,1400,114)"/>
      <ellipse cx="1285" cy="117" rx="22" ry="8" fill="#1d5c1d" transform="rotate(-20,1285,117)"/>
      <ellipse cx="1305" cy="147" rx="18" ry="7" fill="#1d5c1d" transform="rotate(-15,1305,147)"/>
    </g>
    <!-- Small mid-left palm -->
    <g opacity="0.7">
      <path d="M250,280 Q255,230 258,205" stroke="#152e15" stroke-width="6" fill="none" stroke-linecap="round"/>
      <path d="M258,205 Q235,185 210,183" stroke="#152e15" stroke-width="4" fill="none"/>
      <path d="M258,205 Q275,182 295,180" stroke="#152e15" stroke-width="4" fill="none"/>
      <path d="M258,205 Q265,188 280,192" stroke="#152e15" stroke-width="3" fill="none"/>
      <ellipse cx="210" cy="182" rx="18" ry="6" fill="#1a4a1a" transform="rotate(-10,210,182)"/>
      <ellipse cx="295" cy="179" rx="18" ry="6" fill="#1a4a1a" transform="rotate(15,295,179)"/>
      <ellipse cx="280" cy="191" rx="15" ry="6" fill="#1a4a1a" transform="rotate(10,280,191)"/>
    </g>
  </svg>

  <!-- Ocean -->
  <div class="ocean" style="z-index:2;">
    <div class="sun-reflection"></div>
    <div class="wave"></div>
    <div class="wave"></div>
    <div class="wave"></div>
  </div>

  <div class="hero-content" style="z-index:10;">
    <p class="hero-eyebrow">Welcome to</p>
    <h1 class="hero-title">RidgeRush<span class="dash-mtb">-MTB</span></h1>
    <p class="hero-sub">RIDE THE TRAILS · SHRED THE SKILLS · EXPLORE FLORIDA</p>
    <div class="hero-ctas">
      <a href="#practice" class="btn btn-primary">Skills Areas</a>
      <a href="#trails"   class="btn btn-secondary">All Trails</a>
      <a href="#games"    class="btn btn-secondary">Arcade</a>
      <a href="#contact"  class="btn btn-secondary">Contact</a>
    </div>
  </div>
  <div class="scroll-hint"><span>Scroll</span><div class="scroll-arrow"></div></div>
</section>

<!-- PRACTICE AREAS -->
<section id="practice">
  <div class="section-label">Markham Park · Practice Zones</div>
  <h2 class="section-title">Skills &amp;<br>Practice Areas</h2>
  <div class="divider"></div>
  <p class="practice-intro">
    Before you hit the singletrack, sharpen your skills in Markham Park's dedicated practice zones — all located near the trailhead and free to use with your trail pass. Perfect for warming up, learning new techniques, or just having fun between laps.
  </p>
  <div class="practice-grid">

    <div class="practice-card type-pump">
      <span class="practice-icon">🔄</span>
      <div class="practice-name">Pump Track</div>
      <div class="practice-tag">Skills · Flow · All Levels</div>
      <div class="practice-desc">A continuous loop of rollers and banked turns located right at the trailhead, directly across from the start of the Warm Up Loop. Practice generating speed through pumping rather than pedalling — the foundation of efficient MTB riding.</div>
      <div class="practice-features">
        <span class="pf-chip">Rollers</span>
        <span class="pf-chip">Banked Turns</span>
        <span class="pf-chip">Momentum Training</span>
        <span class="pf-chip">All Levels</span>
      </div>
    </div>

    <div class="practice-card type-jumps">
      <span class="practice-icon">🚀</span>
      <div class="practice-name">Freeride &amp; Dirt Jump Area</div>
      <div class="practice-tag">Aerial Skills · Advanced</div>
      <div class="practice-desc">A small but well-built freeride and dirt jump area adjacent to the pump track. Progressive jumps and ramps let riders practice aerial maneuvers, work on their style, and build confidence before hitting Supercross or the Jumpline.</div>
      <div class="practice-features">
        <span class="pf-chip">Dirt Jumps</span>
        <span class="pf-chip">Ramps</span>
        <span class="pf-chip">Progressions</span>
        <span class="pf-chip">Freestyle</span>
      </div>
    </div>

    <div class="practice-card type-skills">
      <span class="practice-icon">🎯</span>
      <div class="practice-name">Skills Park</div>
      <div class="practice-tag">Technical · 15 Features · All Levels</div>
      <div class="practice-desc">A dedicated skills area with 15 easy-to-moderate features designed to help riders develop and refine technique. Updated with new obstacles including wooden berms, elevated rails, rolling bumps, rock jumps, a teeter-totter, and balance beams.</div>
      <div class="practice-features">
        <span class="pf-chip">Wooden Berms</span>
        <span class="pf-chip">Elevated Rails</span>
        <span class="pf-chip">Rolling Bumps</span>
        <span class="pf-chip">Rock Jumps</span>
        <span class="pf-chip">Teeter-Totter</span>
        <span class="pf-chip">Balance Beams</span>
        <span class="pf-chip">Bridges</span>
      </div>
    </div>

    <div class="practice-card type-rock">
      <span class="practice-icon">🪨</span>
      <div class="practice-name">Rock Garden Practice</div>
      <div class="practice-tag">Technical · Intermediate–Advanced</div>
      <div class="practice-desc">A dedicated rock garden section near the trailhead featuring rocks of varying sizes to simulate the natural, rocky terrain you'll encounter on Rock Garden, Area 51, and Gun Range. Perfect for building confidence on technical, uneven surfaces.</div>
      <div class="practice-features">
        <span class="pf-chip">Varied Rock Sizes</span>
        <span class="pf-chip">Natural Terrain</span>
        <span class="pf-chip">Line Choice</span>
        <span class="pf-chip">Technical Skills</span>
      </div>
    </div>

    <div class="practice-card type-freeride">
      <span class="practice-icon">📉</span>
      <div class="practice-name">Drop Zone</div>
      <div class="practice-tag">Drop Features · Intermediate–Expert</div>
      <div class="practice-desc">Various drop-off features of progressive heights designed to get riders comfortable with sudden elevation changes. Start with the smallest drops and work your way up — the same muscle memory you'll need on Iguana Ridge, Pipeline, and Redback.</div>
      <div class="practice-features">
        <span class="pf-chip">Progressive Drops</span>
        <span class="pf-chip">Step-Up Difficulty</span>
        <span class="pf-chip">Landing Practice</span>
        <span class="pf-chip">Commitment Training</span>
      </div>
    </div>

    <div class="practice-card type-wash">
      <span class="practice-icon">🚿</span>
      <div class="practice-name">Bike Wash &amp; Repair Station</div>
      <div class="practice-tag">Amenity · Trailhead</div>
      <div class="practice-desc">An upgraded bike wash station and tools area at the trailhead, plus new picnic benches and Florida-friendly landscaping. Clean your bike after a muddy session and do quick repairs before heading home. Part of the 2023 trailhead improvements.</div>
      <div class="practice-features">
        <span class="pf-chip">Bike Wash</span>
        <span class="pf-chip">Tool Station</span>
        <span class="pf-chip">Bike Rack Storage</span>
        <span class="pf-chip">Picnic Benches</span>
      </div>
    </div>

  </div>
</section>

<!-- TRAILS -->
<section id="trails">
  <div class="section-label">MTB Trail Directory</div>
  <h2 class="section-title">All Trails</h2>
  <div class="divider"></div>
  <p style="max-width:600px;color:rgba(240,236,224,0.65);font-size:0.95rem;line-height:1.8;margin-bottom:2.5rem;position:relative;z-index:1;">
    Every MTB trail at Markham Park &amp; Quiet Waters, plus North America's most iconic rides. <strong style="color:var(--teal)">Click any card to open the trail on a live map.</strong>
  </p>
  <div class="trail-filters">
    <input class="trail-search" type="text" id="trailSearch" placeholder="Search trails, parks…" oninput="filterTrails()">
    <div class="filter-group">
      <span class="filter-label">Park:</span>
      <button class="filter-btn active" data-filter="cat" data-val="all" onclick="setFilter('cat','all',this)">All</button>
      <button class="filter-btn" data-filter="cat" data-val="northamerica" onclick="setFilter('cat','northamerica',this)">🌴 North America</button>
      <button class="filter-btn" data-filter="cat" data-val="markham"      onclick="setFilter('cat','markham',this)">🌿 Markham Park</button>
      <button class="filter-btn" data-filter="cat" data-val="quietwaters"  onclick="setFilter('cat','quietwaters',this)">💧 Quiet Waters</button>
    </div>
    <div class="filter-group">
      <span class="filter-label">Difficulty:</span>
      <button class="filter-btn active" data-filter="diff" data-val="all"    onclick="setFilter('diff','all',this)">All</button>
      <button class="filter-btn" data-filter="diff" data-val="Easy"          onclick="setFilter('diff','Easy',this)">Easy</button>
      <button class="filter-btn" data-filter="diff" data-val="Moderate"      onclick="setFilter('diff','Moderate',this)">Moderate</button>
      <button class="filter-btn" data-filter="diff" data-val="Hard"          onclick="setFilter('diff','Hard',this)">Hard</button>
      <button class="filter-btn" data-filter="diff" data-val="Expert"        onclick="setFilter('diff','Expert',this)">Expert</button>
    </div>
  </div>
  <div class="trail-count"><span id="trailCountNum">0</span> trails — click any card to open trail map</div>
  <div class="trails-grid" id="trailsGrid"></div>
</section>

<!-- GAMES -->
<section id="games">
  <div class="section-label">Ridge Arcade</div>
  <h2 class="section-title">Play the<br>Peak</h2>
  <div class="divider"></div>
  <p style="max-width:500px;color:rgba(240,236,224,0.65);font-size:0.95rem;line-height:1.8;">Four games — three classic arcade games and a full disease simulation.</p>
  <div class="games-layout">

    <!-- TETRIS -->
    <div class="game-panel">
      <div class="game-header">
        <div class="game-tag">Arcade · Classic · Puzzle</div>
        <div class="game-title">🟦 Ridge Tetris</div>
        <button class="fs-btn" onclick="toggleFS(this)">⛶ Fullscreen</button>
      </div>
      <div class="game-canvas-area" style="flex-direction:column;gap:0.8rem;padding:1.5rem;">
        <div style="display:flex;gap:1.5rem;align-items:flex-start;">
          <canvas id="tetrisCanvas" width="240" height="480" style="border:1px solid rgba(0,180,160,0.2);"></canvas>
          <div style="display:flex;flex-direction:column;gap:1rem;min-width:100px;">
            <div>
              <div style="font-family:'Barlow Condensed',sans-serif;font-size:0.65rem;letter-spacing:3px;text-transform:uppercase;color:rgba(240,236,224,0.35);margin-bottom:0.3rem;">SCORE</div>
              <div id="tetScore" style="font-family:'Bebas Neue',sans-serif;font-size:2rem;color:var(--teal);">0</div>
            </div>
            <div>
              <div style="font-family:'Barlow Condensed',sans-serif;font-size:0.65rem;letter-spacing:3px;text-transform:uppercase;color:rgba(240,236,224,0.35);margin-bottom:0.3rem;">LEVEL</div>
              <div id="tetLevel" style="font-family:'Bebas Neue',sans-serif;font-size:2rem;color:var(--coral);">1</div>
            </div>
            <div>
              <div style="font-family:'Barlow Condensed',sans-serif;font-size:0.65rem;letter-spacing:3px;text-transform:uppercase;color:rgba(240,236,224,0.35);margin-bottom:0.3rem;">LINES</div>
              <div id="tetLines" style="font-family:'Bebas Neue',sans-serif;font-size:2rem;color:var(--sand);">0</div>
            </div>
            <div>
              <div style="font-family:'Barlow Condensed',sans-serif;font-size:0.65rem;letter-spacing:3px;text-transform:uppercase;color:rgba(240,236,224,0.35);margin-bottom:0.3rem;">NEXT</div>
              <canvas id="tetNext" width="80" height="80" style="border:1px solid rgba(0,180,160,0.15);"></canvas>
            </div>
          </div>
        </div>
      </div>
      <div class="game-controls">
        <kbd>←</kbd><kbd>→</kbd> move &nbsp;·&nbsp; <kbd>↑</kbd> rotate &nbsp;·&nbsp; <kbd>↓</kbd> soft drop &nbsp;·&nbsp; <kbd>Space</kbd> hard drop &nbsp;·&nbsp; <kbd>P</kbd> pause
      </div>
    </div>

    <!-- PAC-MAN -->
    <div class="game-panel">
      <div class="game-header">
        <div class="game-tag">Arcade · Classic · Chase</div>
        <div class="game-title">👾 Ridge Pac</div>
        <button class="fs-btn" onclick="toggleFS(this)">⛶ Fullscreen</button>
      </div>
      <div class="game-canvas-area" style="flex-direction:column;">
        <canvas id="pacCanvas" width="448" height="496"></canvas>
        <div class="dpad">
          <div></div><button class="dpad-btn" onclick="PACMAN.dpad(0,-1)">▲</button><div></div>
          <button class="dpad-btn" onclick="PACMAN.dpad(-1,0)">◀</button><div class="dpad-center"></div><button class="dpad-btn" onclick="PACMAN.dpad(1,0)">▶</button>
          <div></div><button class="dpad-btn" onclick="PACMAN.dpad(0,1)">▼</button><div></div>
        </div>
      </div>
      <div class="game-controls">
        <kbd>↑</kbd><kbd>↓</kbd><kbd>←</kbd><kbd>→</kbd> move &nbsp;·&nbsp; <kbd>Space</kbd> start &nbsp;·&nbsp; Score: <span id="pacScore">0</span> &nbsp;·&nbsp; Lives: <span id="pacLives">3</span>
      </div>
    </div>

    <!-- SERPENT -->
    <div class="game-panel">
      <div class="game-header">
        <div class="game-tag">Arcade · Classic</div>
        <div class="game-title">🐍 Ridge Serpent</div>
        <button class="fs-btn" onclick="toggleFS(this)">⛶ Fullscreen</button>
      </div>
      <div class="game-canvas-area" style="flex-direction:column;">
        <canvas id="serpentCanvas" width="400" height="340"></canvas>
        <div class="dpad">
          <div></div><button class="dpad-btn" onclick="SERPENT.dpad(0,-1)">▲</button><div></div>
          <button class="dpad-btn" onclick="SERPENT.dpad(-1,0)">◀</button><div class="dpad-center"></div><button class="dpad-btn" onclick="SERPENT.dpad(1,0)">▶</button>
          <div></div><button class="dpad-btn" onclick="SERPENT.dpad(0,1)">▼</button><div></div>
        </div>
      </div>
      <div class="game-controls">
        <kbd>↑</kbd><kbd>↓</kbd><kbd>←</kbd><kbd>→</kbd> to move &nbsp;·&nbsp; <kbd>Space</kbd> to start/pause &nbsp;·&nbsp; Score: <span id="serpentScore">0</span> &nbsp;·&nbsp; High: <span id="serpentHigh">0</span>
      </div>
    </div>


    <!-- PATHOGEN -->
    <div class="game-panel">
      <div class="game-header">
        <div class="game-tag">Strategy · Simulation · Plague Inc. Style</div>
        <div class="game-title">☣ Pathogen</div>
        <button class="fs-btn" onclick="toggleFS(this)">⛶ Fullscreen</button>
      </div>
      
<div id="pathogen-game" style="width:100%;background:#060c10;font-family:'Courier New',monospace;">
<style>
  #pathogen-game {
    --bg:#060c10;--panel:#0a1520;--border:rgba(180,20,20,0.3);
    --red:#cc2222;--red2:#ff4444;--green:#22cc44;--orange:#e07820;
    --teal:#00b4a0;--cream:#f0ece0;--dim:rgba(240,236,224,0.45);
    --gold:#e8c97a;
  }

  #pathogen-game * {margin:0;padding:0;box-sizing:border-box;}
:root{
  --bg:#060c10;--panel:#0a1520;--border:rgba(180,20,20,0.3);
  --red:#cc2222;--red2:#ff4444;--green:#22cc44;--orange:#e07820;
  --teal:#00b4a0;--cream:#f0ece0;--dim:rgba(240,236,224,0.45);
  --gold:#e8c97a;
}
body{background:var(--bg);color:var(--cream);font-family:'Courier New',monospace;overflow:hidden;height:100vh;display:flex;flex-direction:column;}

/* ── HEADER ── */
  #pathogen-game #hdr {display:flex;align-items:center;justify-content:space-between;padding:0.5rem 1rem;background:rgba(0,0,0,0.6);border-bottom:1px solid var(--border);flex-shrink:0;}
  #pathogen-game #hdr h1 {font-size:1.3rem;letter-spacing:4px;color:var(--red2);text-shadow:0 0 18px rgba(200,0,0,0.5);}
  #pathogen-game .hdr-stats {display:flex;gap:1.5rem;}
  #pathogen-game .hstat {display:flex;flex-direction:column;align-items:center;}
  #pathogen-game .hstat-val {font-size:1rem;font-weight:bold;}
  #pathogen-game .hstat-lbl {font-size:0.55rem;letter-spacing:2px;color:var(--dim);text-transform:uppercase;}
  #pathogen-game .infected-val {color:var(--red2);}
  #pathogen-game .dead-val {color:#888;}
  #pathogen-game .healthy-val {color:var(--green);}
  #pathogen-game .dna-val {color:var(--gold);}
  #pathogen-game #day-display {font-size:0.7rem;letter-spacing:2px;color:var(--dim);}

/* ── MAIN LAYOUT ── */
  #pathogen-game #main {display:flex;flex:1;overflow:hidden;}

/* ── WORLD MAP ── */
  #pathogen-game #map-wrap {flex:1;position:relative;overflow:hidden;background:#040c10;}
  #pathogen-game #worldSVG {width:100%;height:100%;}
  #pathogen-game .country {stroke:#0a2030;stroke-width:0.5;cursor:pointer;transition:filter 0.2s;}
  #pathogen-game .country:hover {filter:brightness(1.4);}
  #pathogen-game .country.healthy {fill:#0d3040;}
  #pathogen-game .country.infected {fill:#6b0a0a;}
  #pathogen-game .country.severe {fill:#aa1010;}
  #pathogen-game .country.critical {fill:#dd2020;}
  #pathogen-game .country.cured {fill:#103020;}
  #pathogen-game .country.dead {fill:#1a1a1a;}
  #pathogen-game .city-dot {fill:rgba(255,255,100,0.6);stroke:none;cursor:pointer;}
  #pathogen-game .city-dot:hover {fill:rgba(255,255,0,1);}

/* ── BIOHAZARD PULSE (infection events) ── */
  #pathogen-game .infect-pulse {pointer-events:none;fill:none;stroke:rgba(220,40,40,0.7);stroke-width:1.5;animation:pulse-out 1.2s ease-out forwards;}
@keyframes pulse-out{from{r:4;opacity:1;}to{r:22;opacity:0;}}

/* ── RIGHT PANEL ── */
#rpanel{width:300px;background:var(--panel);border-left:1px solid var(--border);display:flex;flex-direction:column;overflow:hidden;}
.tab-bar{display:flex;border-bottom:1px solid var(--border);flex-shrink:0;}
.tab{flex:1;padding:0.5rem 0.3rem;text-align:center;font-size:0.62rem;letter-spacing:2px;text-transform:uppercase;cursor:pointer;color:var(--dim);border:none;background:transparent;transition:all 0.2s;}
.tab.active{color:var(--red2);border-bottom:2px solid var(--red2);background:rgba(200,0,0,0.06);}
.tab:hover:not(.active){color:var(--cream);background:rgba(255,255,255,0.03);}
.tab-content{flex:1;overflow-y:auto;padding:0.8rem;}
.tab-content::-webkit-scrollbar{width:4px;}
.tab-content::-webkit-scrollbar-track{background:transparent;}
.tab-content::-webkit-scrollbar-thumb{background:rgba(200,20,20,0.3);border-radius:2px;}

/* DISEASE SETUP */
#setup-screen{display:flex;flex-direction:column;gap:0.8rem;padding:1rem;}
#setup-screen h2{font-size:1rem;letter-spacing:3px;color:var(--red2);}
.setup-field{display:flex;flex-direction:column;gap:0.3rem;}
.setup-field label{font-size:0.62rem;letter-spacing:2px;text-transform:uppercase;color:var(--dim);}
.setup-field input,.setup-field select{background:rgba(255,255,255,0.05);border:1px solid rgba(255,255,255,0.1);color:var(--cream);padding:0.4rem 0.6rem;font-family:inherit;font-size:0.8rem;outline:none;}
.setup-field input:focus,.setup-field select:focus{border-color:var(--red2);}
.type-grid{display:grid;grid-template-columns:1fr 1fr;gap:0.5rem;}
.type-btn{background:rgba(255,255,255,0.04);border:1px solid rgba(255,255,255,0.1);color:var(--dim);padding:0.5rem;cursor:pointer;font-size:0.7rem;letter-spacing:1px;text-align:center;transition:all 0.2s;}
.type-btn:hover,.type-btn.sel{background:rgba(200,20,20,0.15);border-color:var(--red2);color:var(--cream);}
.diff-row{display:flex;gap:0.4rem;}
.diff-btn{flex:1;background:rgba(255,255,255,0.04);border:1px solid rgba(255,255,255,0.1);color:var(--dim);padding:0.4rem;cursor:pointer;font-size:0.65rem;letter-spacing:1px;text-align:center;transition:all 0.2s;}
.diff-btn:hover,.diff-btn.sel{border-color:var(--gold);color:var(--gold);background:rgba(232,201,122,0.1);}
.start-btn{background:rgba(200,0,0,0.2);border:1px solid var(--red);color:var(--red2);padding:0.8rem;cursor:pointer;font-size:0.85rem;letter-spacing:4px;text-transform:uppercase;width:100%;margin-top:0.5rem;transition:all 0.2s;}
.start-btn:hover{background:rgba(200,0,0,0.4);border-color:var(--red2);}

/* UPGRADES */
.upgrade-section{margin-bottom:1rem;}
.upgrade-section h3{font-size:0.62rem;letter-spacing:3px;text-transform:uppercase;color:var(--dim);margin-bottom:0.5rem;padding-bottom:0.3rem;border-bottom:1px solid rgba(255,255,255,0.06);}
.upgrade-node{display:flex;align-items:center;gap:0.5rem;padding:0.45rem 0.5rem;margin-bottom:0.3rem;border:1px solid rgba(255,255,255,0.07);cursor:pointer;transition:all 0.18s;position:relative;}
.upgrade-node:hover:not(.locked):not(.owned){background:rgba(200,0,0,0.1);border-color:rgba(200,0,0,0.3);}
.upgrade-node.owned{background:rgba(0,100,50,0.15);border-color:rgba(0,180,80,0.25);cursor:default;}
.upgrade-node.locked{opacity:0.4;cursor:not-allowed;}
.upgrade-node.affordable:not(.owned):not(.locked){border-color:rgba(232,201,122,0.4);animation:glow-pulse 2s infinite;}
@keyframes glow-pulse{0%,100%{box-shadow:0 0 4px rgba(232,201,122,0);}50%{box-shadow:0 0 8px rgba(232,201,122,0.3);}}
.upg-icon{font-size:1.1rem;flex-shrink:0;}
.upg-info{flex:1;min-width:0;}
.upg-name{font-size:0.72rem;letter-spacing:1px;color:var(--cream);}
.upg-desc{font-size:0.58rem;color:var(--dim);margin-top:0.1rem;line-height:1.3;}
.upg-cost{font-size:0.65rem;color:var(--gold);flex-shrink:0;font-weight:bold;}
.upg-cost.owned{color:var(--green);}

/* STATS TAB */
.stat-row{display:flex;justify-content:space-between;align-items:center;padding:0.35rem 0;border-bottom:1px solid rgba(255,255,255,0.04);font-size:0.72rem;}
.stat-row .lbl{color:var(--dim);}
.stat-row .val{font-weight:bold;}
.progress-bar{height:6px;background:rgba(255,255,255,0.07);border-radius:3px;overflow:hidden;margin:0.2rem 0;}
.progress-fill{height:100%;border-radius:3px;transition:width 0.5s;}
.section-title-sm{font-size:0.62rem;letter-spacing:3px;text-transform:uppercase;color:var(--dim);margin:0.8rem 0 0.4rem;padding-bottom:0.3rem;border-bottom:1px solid rgba(255,255,255,0.06);}

/* SYMPTOMS */
.symptom-tag{display:inline-block;padding:0.15rem 0.5rem;margin:0.15rem;font-size:0.6rem;letter-spacing:1px;border-radius:2px;}
.symptom-tag.mild{background:rgba(255,180,0,0.15);border:1px solid rgba(255,180,0,0.3);color:#ffb800;}
.symptom-tag.severe{background:rgba(255,80,0,0.15);border:1px solid rgba(255,80,0,0.3);color:#ff5000;}
.symptom-tag.lethal{background:rgba(200,0,0,0.2);border:1px solid rgba(200,0,0,0.4);color:var(--red2);}

/* NEWS TICKER */
#news-ticker{background:rgba(0,0,0,0.5);border-top:1px solid var(--border);padding:0.3rem 1rem;font-size:0.62rem;letter-spacing:1px;color:var(--dim);overflow:hidden;white-space:nowrap;flex-shrink:0;}
.ticker-inner{display:inline-block;animation:ticker-scroll 30s linear infinite;}
@keyframes ticker-scroll{from{transform:translateX(100vw);}to{transform:translateX(-100%);}}

/* NOTIFICATION POPUP */
#notif{position:fixed;top:60px;left:50%;transform:translateX(-50%);background:rgba(0,0,0,0.92);border:1px solid var(--border);padding:0.6rem 1.2rem;font-size:0.72rem;letter-spacing:1px;color:var(--red2);z-index:999;pointer-events:none;opacity:0;transition:opacity 0.3s;max-width:400px;text-align:center;}
#notif.show{opacity:1;}

/* DNA POINTS POPUP */
.dna-popup{position:absolute;pointer-events:none;font-size:0.75rem;color:var(--gold);font-weight:bold;animation:float-up 1.5s ease-out forwards;z-index:50;}
@keyframes float-up{from{transform:translateY(0);opacity:1;}to{transform:translateY(-40px);opacity:0;}}

/* GAME OVER / WIN SCREENS */
#overlay{position:fixed;inset:0;background:rgba(0,0,0,0.88);align-items:center;justify-content:center;z-index:200;display:none;}
#overlay-box{background:var(--panel);border:1px solid var(--border);padding:2.5rem;text-align:center;max-width:380px;}
#overlay-box h2{font-size:2rem;letter-spacing:4px;margin-bottom:1rem;}
#overlay-box p{font-size:0.8rem;color:var(--dim);line-height:1.8;margin-bottom:1.5rem;}
.overlay-btn{background:rgba(200,0,0,0.2);border:1px solid var(--red);color:var(--red2);padding:0.7rem 2rem;cursor:pointer;font-family:inherit;font-size:0.8rem;letter-spacing:3px;text-transform:uppercase;transition:all 0.2s;}
.overlay-btn:hover{background:rgba(200,0,0,0.4);}
.win-box h2{color:var(--gold);}
.win-box{border-color:rgba(232,201,122,0.4);}

/* SPEED CONTROLS */
#speed-bar{display:flex;gap:0.4rem;align-items:center;padding:0.4rem 0.6rem;background:rgba(0,0,0,0.4);border-top:1px solid var(--border);flex-shrink:0;}
.speed-btn{background:rgba(255,255,255,0.05);border:1px solid rgba(255,255,255,0.1);color:var(--dim);padding:0.2rem 0.6rem;cursor:pointer;font-size:0.65rem;letter-spacing:1px;transition:all 0.15s;}
.speed-btn.active{background:rgba(200,0,0,0.2);border-color:var(--red2);color:var(--red2);}
#speed-lbl{font-size:0.6rem;letter-spacing:2px;color:var(--dim);margin-right:0.3rem;}
#pause-btn{margin-left:auto;background:rgba(255,255,255,0.05);border:1px solid rgba(255,255,255,0.1);color:var(--cream);padding:0.2rem 0.8rem;cursor:pointer;font-size:0.65rem;letter-spacing:2px;}
#pause-btn:hover{border-color:var(--teal);color:var(--teal);}

  #pathogen-game { height:700px; display:flex; flex-direction:column; overflow:hidden; position:relative; }
</style>


<!-- HEADER -->
<div id="hdr">
  <h1>☣ PATHOGEN</h1>
  <div class="hdr-stats">
    <div class="hstat"><div class="hstat-val infected-val" id="h-infected">0</div><div class="hstat-lbl">Infected</div></div>
    <div class="hstat"><div class="hstat-val dead-val" id="h-dead">0</div><div class="hstat-lbl">Dead</div></div>
    <div class="hstat"><div class="hstat-val healthy-val" id="h-healthy">8,000,000,000</div><div class="hstat-lbl">Healthy</div></div>
    <div class="hstat"><div class="hstat-val dna-val" id="h-dna">0</div><div class="hstat-lbl">DNA ⚗</div></div>
  </div>
  <div id="day-display">DAY 0</div>
</div>

<!-- MAIN -->
<div id="main">

  <!-- WORLD MAP -->
  <div id="map-wrap">
    <svg id="worldSVG" viewBox="0 0 1000 500" xmlns="http://www.w3.org/2000/svg">
      <!-- Simplified world regions as polygons -->
      <!-- North America -->
      <polygon class="country healthy" id="c-northamerica" data-name="North America" data-pop="500000000"
        points="80,80 200,70 240,90 260,130 230,160 200,180 160,190 100,180 70,150 60,110"/>
      <!-- Central America -->
      <polygon class="country healthy" id="c-centralamerica" data-name="Central America" data-pop="180000000"
        points="160,190 200,180 210,210 190,230 160,220"/>
      <!-- South America -->
      <polygon class="country healthy" id="c-southamerica" data-name="South America" data-pop="440000000"
        points="155,230 210,215 240,230 250,280 240,350 210,390 180,400 150,370 130,320 130,270"/>
      <!-- Western Europe -->
      <polygon class="country healthy" id="c-westeurope" data-name="Western Europe" data-pop="390000000"
        points="380,90 430,80 450,100 440,130 410,140 380,130 370,110"/>
      <!-- Eastern Europe -->
      <polygon class="country healthy" id="c-easteurope" data-name="Eastern Europe" data-pop="290000000"
        points="450,80 520,75 540,95 530,125 500,135 450,130 440,110"/>
      <!-- Russia -->
      <polygon class="country healthy" id="c-russia" data-name="Russia" data-pop="145000000"
        points="520,50 700,40 760,60 780,90 740,110 680,115 600,110 540,100 520,75"/>
      <!-- Middle East -->
      <polygon class="country healthy" id="c-middleeast" data-name="Middle East" data-pop="410000000"
        points="450,140 540,130 560,150 550,185 510,195 460,185 440,165"/>
      <!-- Africa -->
      <polygon class="country healthy" id="c-africa" data-name="Africa" data-pop="1400000000"
        points="380,150 460,145 480,170 480,260 460,330 420,360 380,340 340,290 330,230 350,180"/>
      <!-- South Asia -->
      <polygon class="country healthy" id="c-southasia" data-name="South Asia" data-pop="1900000000"
        points="550,140 640,130 670,155 660,200 620,220 570,210 545,185"/>
      <!-- Southeast Asia -->
      <polygon class="country healthy" id="c-seasia" data-name="SE Asia" data-pop="680000000"
        points="660,155 730,145 760,170 750,210 710,225 670,210 655,185"/>
      <!-- East Asia -->
      <polygon class="country healthy" id="c-eastasia" data-name="East Asia" data-pop="1600000000"
        points="670,80 780,70 820,90 830,130 800,160 740,165 690,150 665,120"/>
      <!-- Oceania -->
      <polygon class="country healthy" id="c-oceania" data-name="Oceania" data-pop="43000000"
        points="760,290 840,280 870,310 850,350 800,355 760,330"/>
      <!-- Japan -->
      <ellipse class="country healthy" id="c-japan" data-name="Japan" data-pop="125000000" cx="850" cy="120" rx="22" ry="30"/>
      <!-- UK/Ireland -->
      <ellipse class="country healthy" id="c-uk" data-name="United Kingdom" data-pop="67000000" cx="360" cy="95" rx="14" ry="18"/>
      <!-- Greenland -->
      <ellipse class="country healthy" id="c-greenland" data-name="Greenland" data-pop="56000" cx="270" cy="55" rx="35" ry="25"/>
      <!-- Indonesia -->
      <polygon class="country healthy" id="c-indonesia" data-name="Indonesia" data-pop="275000000"
        points="700,230 780,220 810,240 800,265 750,270 700,255"/>
      <!-- Madagascar -->
      <ellipse class="country healthy" id="c-madagascar" data-name="Madagascar" data-pop="28000000" cx="500" cy="310" rx="12" ry="25"/>
    </svg>
    <!-- Infection animations layer -->
    <svg id="animSVG" style="position:absolute;inset:0;width:100%;height:100%;pointer-events:none;" viewBox="0 0 1000 500"></svg>
  </div>

  <!-- RIGHT PANEL -->
  <div id="rpanel">
    <!-- SETUP SCREEN (shown before game starts) -->
    <div id="setup-screen">
      <h2>☣ PATHOGEN</h2>
      <p style="font-size:0.68rem;color:var(--dim);line-height:1.6;">Evolve a deadly pathogen. Infect and kill all of humanity before a cure is developed.</p>

      <div class="setup-field">
        <label>Disease Name</label>
        <input type="text" id="dis-name" placeholder="e.g. RidgeVirus-X" maxlength="24" value="RidgeVirus-X">
      </div>

      <div class="setup-field">
        <label>Pathogen Type</label>
        <div class="type-grid">
          <div class="type-btn sel" data-type="bacteria">🦠 Bacteria<br><span style="font-size:0.55rem;color:var(--dim)">Balanced, adaptable</span></div>
          <div class="type-btn" data-type="virus">🔴 Virus<br><span style="font-size:0.55rem;color:var(--dim)">Fast mutating</span></div>
          <div class="type-btn" data-type="fungus">🍄 Fungus<br><span style="font-size:0.55rem;color:var(--dim)">Drug resistant</span></div>
          <div class="type-btn" data-type="parasite">🐛 Parasite<br><span style="font-size:0.55rem;color:var(--dim)">Hard to detect</span></div>
          <div class="type-btn" data-type="prion">🧠 Prion<br><span style="font-size:0.55rem;color:var(--dim)">Untreatable</span></div>
          <div class="type-btn" data-type="nano">🤖 Nano-virus<br><span style="font-size:0.55rem;color:var(--dim)">Tech-enhanced</span></div>
        </div>
      </div>

      <div class="setup-field">
        <label>Starting Country</label>
        <select id="start-country">
          <option value="c-northamerica">North America</option>
          <option value="c-southasia">South Asia (High density)</option>
          <option value="c-eastasia">East Asia</option>
          <option value="c-africa">Africa</option>
          <option value="c-westeurope">Western Europe</option>
          <option value="c-russia">Russia</option>
          <option value="c-southamerica">South America</option>
          <option value="c-oceania">Oceania (Island isolation)</option>
        </select>
      </div>

      <div class="setup-field">
        <label>Difficulty</label>
        <div class="diff-row">
          <div class="diff-btn sel" data-diff="casual">Casual</div>
          <div class="diff-btn" data-diff="normal">Normal</div>
          <div class="diff-btn" data-diff="brutal">Brutal</div>
          <div class="diff-btn" data-diff="mega">Mega Brutal</div>
        </div>
      </div>

      <button class="start-btn" id="start-game-btn">☣ BEGIN OUTBREAK</button>
    </div>

    <!-- GAME TABS (hidden until game starts) -->
    <div id="game-ui" style="display:none;flex-direction:column;flex:1;overflow:hidden;">
      <div class="tab-bar">
        <button class="tab active" data-tab="upgrades">Evolve</button>
        <button class="tab" data-tab="disease">Disease</button>
        <button class="tab" data-tab="world">World</button>
        <button class="tab" data-tab="cure">Cure</button>
      </div>

      <!-- EVOLVE TAB -->
      <div class="tab-content" id="tab-upgrades">
        <div class="upgrade-section">
          <h3>🌬 Transmission</h3>
          <div id="upg-transmission"></div>
        </div>
        <div class="upgrade-section">
          <h3>💀 Symptoms</h3>
          <div id="upg-symptoms"></div>
        </div>
        <div class="upgrade-section">
          <h3>🛡 Abilities</h3>
          <div id="upg-abilities"></div>
        </div>
      </div>

      <!-- DISEASE TAB -->
      <div class="tab-content" id="tab-disease" style="display:none;">
        <div class="section-title-sm">Stats</div>
        <div class="stat-row"><span class="lbl">Infectivity</span><span class="val" id="stat-inf" style="color:var(--orange)">0</span></div>
        <div class="progress-bar"><div class="progress-fill" id="bar-inf" style="background:var(--orange);width:0%"></div></div>
        <div class="stat-row"><span class="lbl">Lethality</span><span class="val" id="stat-let" style="color:var(--red2)">0</span></div>
        <div class="progress-bar"><div class="progress-fill" id="bar-let" style="background:var(--red2);width:0%"></div></div>
        <div class="stat-row"><span class="lbl">Severity</span><span class="val" id="stat-sev" style="color:#ff9900">0</span></div>
        <div class="progress-bar"><div class="progress-fill" id="bar-sev" style="background:#ff9900;width:0%"></div></div>
        <div class="stat-row"><span class="lbl">Drug Resistance</span><span class="val" id="stat-drug" style="color:var(--teal)">0</span></div>
        <div class="progress-bar"><div class="progress-fill" id="bar-drug" style="background:var(--teal);width:0%"></div></div>
        <div class="stat-row"><span class="lbl">Cure Resistance</span><span class="val" id="stat-cure-res" style="color:var(--gold)">0</span></div>
        <div class="progress-bar"><div class="progress-fill" id="bar-cure-res" style="background:var(--gold);width:0%"></div></div>

        <div class="section-title-sm">Active Symptoms</div>
        <div id="symptom-list">—</div>

        <div class="section-title-sm">Mutation Events</div>
        <div id="mutation-log" style="font-size:0.65rem;color:var(--dim);line-height:1.8;">No mutations yet.</div>
      </div>

      <!-- WORLD TAB -->
      <div class="tab-content" id="tab-world" style="display:none;">
        <div class="section-title-sm">Regions</div>
        <div id="country-list"></div>
      </div>

      <!-- CURE TAB -->
      <div class="tab-content" id="tab-cure" style="display:none;">
        <div class="stat-row"><span class="lbl">Cure Progress</span><span class="val" id="cure-pct" style="color:var(--teal)">0%</span></div>
        <div class="progress-bar" style="height:10px;margin-bottom:1rem;"><div class="progress-fill" id="cure-bar" style="background:var(--teal);width:0%"></div></div>
        <div class="stat-row"><span class="lbl">Research Labs Active</span><span class="val" id="labs-active">0</span></div>
        <div class="stat-row"><span class="lbl">Cure Speed</span><span class="val" id="cure-speed-disp">0%/day</span></div>
        <div class="stat-row"><span class="lbl">Countries Locked Down</span><span class="val" id="lockdowns">0</span></div>
        <div class="stat-row"><span class="lbl">Vaccines Deployed</span><span class="val" id="vaccines">0</span></div>
        <div class="section-title-sm">Government Actions</div>
        <div id="gov-log" style="font-size:0.65rem;color:var(--dim);line-height:1.9;">No actions yet.</div>
      </div>
    </div>
  </div>
</div>

<!-- SPEED BAR -->
<div id="speed-bar" style="display:none;">
  <span id="speed-lbl">SPEED:</span>
  <button class="speed-btn active" data-speed="1" onclick="setSpeed(1)">▶ 1×</button>
  <button class="speed-btn" data-speed="2" onclick="setSpeed(2)">▶▶ 2×</button>
  <button class="speed-btn" data-speed="3" onclick="setSpeed(3)">▶▶▶ 3×</button>
  <button class="speed-btn" id="pause-btn" onclick="togglePause()">⏸ PAUSE</button>
</div>

<!-- NEWS TICKER -->
<div id="news-ticker"><span class="ticker-inner" id="ticker-text">☣ PATHOGEN — Evolve your disease. Infect the world. Eradicate humanity.</span></div>

<!-- NOTIFICATION -->
<div id="notif"></div>

<!-- OVERLAY (win/lose) -->
<div id="overlay">
  <div id="overlay-box">
    <h2 id="overlay-title"></h2>
    <p id="overlay-msg"></p>
    <button class="overlay-btn" onclick="resetGame()">↺ PLAY AGAIN</button>
  </div>
</div>

<script>
// ═══════════════════════════════════════════
//  PATHOGEN — Full Plague Inc. Game Engine
// ═══════════════════════════════════════════

const WORLD_POP = 8_000_000_000;

// COUNTRIES data
const COUNTRIES = {
  'c-northamerica':  {name:'North America',  pop:500_000_000,  climate:'temperate', wealth:'rich',    cx:165, cy:135, neighbors:['c-centralamerica','c-westeurope','c-easteurope']},
  'c-centralamerica':{name:'Central America',pop:180_000_000,  climate:'tropical',  wealth:'medium',  cx:185, cy:210, neighbors:['c-northamerica','c-southamerica','c-africa']},
  'c-southamerica':  {name:'South America',  pop:440_000_000,  climate:'tropical',  wealth:'medium',  cx:185, cy:310, neighbors:['c-centralamerica']},
  'c-westeurope':    {name:'West Europe',    pop:390_000_000,  climate:'temperate', wealth:'rich',    cx:410, cy:110, neighbors:['c-easteurope','c-northamerica','c-africa','c-middleeast','c-uk']},
  'c-easteurope':    {name:'East Europe',    pop:290_000_000,  climate:'temperate', wealth:'medium',  cx:490, cy:105, neighbors:['c-westeurope','c-russia','c-middleeast']},
  'c-russia':        {name:'Russia',         pop:145_000_000,  climate:'cold',      wealth:'medium',  cx:650, cy:75,  neighbors:['c-easteurope','c-eastasia','c-southasia']},
  'c-middleeast':    {name:'Middle East',    pop:410_000_000,  climate:'arid',      wealth:'medium',  cx:500, cy:165, neighbors:['c-easteurope','c-africa','c-southasia','c-westeurope']},
  'c-africa':        {name:'Africa',         pop:1_400_000_000,climate:'tropical',  wealth:'poor',    cx:415, cy:255, neighbors:['c-westeurope','c-middleeast','c-centralamerica','c-madagascar']},
  'c-southasia':     {name:'South Asia',     pop:1_900_000_000,climate:'tropical',  wealth:'poor',    cx:610, cy:175, neighbors:['c-middleeast','c-eastasia','c-russia','c-seasia']},
  'c-seasia':        {name:'SE Asia',        pop:680_000_000,  climate:'tropical',  wealth:'medium',  cx:710, cy:185, neighbors:['c-southasia','c-eastasia','c-oceania','c-indonesia']},
  'c-eastasia':      {name:'East Asia',      pop:1_600_000_000,climate:'temperate', wealth:'rich',    cx:750, cy:120, neighbors:['c-russia','c-southasia','c-seasia','c-japan']},
  'c-oceania':       {name:'Oceania',        pop:43_000_000,   climate:'temperate', wealth:'rich',    cx:815, cy:320, neighbors:['c-seasia','c-indonesia']},
  'c-japan':         {name:'Japan',          pop:125_000_000,  climate:'temperate', wealth:'rich',    cx:850, cy:120, neighbors:['c-eastasia']},
  'c-uk':            {name:'United Kingdom', pop:67_000_000,   climate:'cold',      wealth:'rich',    cx:360, cy:95,  neighbors:['c-westeurope']},
  'c-greenland':     {name:'Greenland',      pop:56_000,       climate:'cold',      wealth:'rich',    cx:270, cy:55,  neighbors:['c-northamerica']},
  'c-indonesia':     {name:'Indonesia',      pop:275_000_000,  climate:'tropical',  wealth:'medium',  cx:755, cy:245, neighbors:['c-seasia','c-oceania']},
  'c-madagascar':    {name:'Madagascar',     pop:28_000_000,   climate:'tropical',  wealth:'poor',    cx:500, cy:310, neighbors:['c-africa']},
};

// UPGRADE TREES
const UPGRADES = {
  transmission: [
    {id:'air1',      name:'Airborne',          icon:'💨', cost:3,  desc:'Spreads through the air',           requires:[],       inf:8,  sev:1,  let:0, drug:0, cureRes:0},
    {id:'air2',      name:'Aerosol',            icon:'🌫', cost:5,  desc:'Enhanced airborne transmission',    requires:['air1'], inf:14, sev:2,  let:0, drug:0, cureRes:1},
    {id:'air3',      name:'Extreme Drought',    icon:'☁', cost:8,  desc:'Thrives in dry conditions',         requires:['air2'], inf:10, sev:2,  let:1, drug:1, cureRes:1},
    {id:'water1',    name:'Water-borne',         icon:'💧', cost:3,  desc:'Contaminates water supplies',       requires:[],       inf:8,  sev:1,  let:0, drug:0, cureRes:0},
    {id:'water2',    name:'Aquacyte',            icon:'🌊', cost:5,  desc:'Survives in water long-term',       requires:['water1'],inf:12, sev:1, let:0, drug:1, cureRes:0},
    {id:'insect1',   name:'Insect Transmission', icon:'🦟', cost:4,  desc:'Spread by insects',                requires:[],       inf:9,  sev:1,  let:0, drug:0, cureRes:0},
    {id:'insect2',   name:'Bird Transmission',   icon:'🦅', cost:6,  desc:'Spread by birds globally',         requires:['insect1'],inf:14,sev:2, let:0, drug:0, cureRes:1},
    {id:'contact1',  name:'Direct Contact',      icon:'🤝', cost:2,  desc:'Spreads by physical contact',      requires:[],       inf:6,  sev:1,  let:0, drug:0, cureRes:0},
    {id:'contact2',  name:'Saliva Transmission', icon:'😷', cost:3,  desc:'Spreads through saliva',           requires:['contact1'],inf:8, sev:1, let:0, drug:0, cureRes:0},
    {id:'blood1',    name:'Blood-borne',         icon:'🩸', cost:5,  desc:'Spreads via blood contact',        requires:[],       inf:7,  sev:3,  let:2, drug:2, cureRes:1},
  ],
  symptoms: [
    {id:'cough',     name:'Coughing',            icon:'🤧', cost:1,  desc:'Mild respiratory symptom',         requires:[],       inf:5,  sev:3,  let:0, drug:0, cureRes:0, severity:'mild'},
    {id:'fever',     name:'Fever',               icon:'🌡', cost:1,  desc:'Elevated body temperature',        requires:[],       inf:3,  sev:4,  let:1, drug:0, cureRes:0, severity:'mild'},
    {id:'rash',      name:'Skin Rash',           icon:'🔴', cost:2,  desc:'Visible rash increases visibility',requires:['cough'],inf:2,  sev:5,  let:1, drug:0, cureRes:1, severity:'mild'},
    {id:'pulm',      name:'Pulmonary Fibrosis',  icon:'🫁', cost:4,  desc:'Severe lung scarring',             requires:['cough'],inf:3,  sev:12, let:6, drug:2, cureRes:2, severity:'severe'},
    {id:'hemor',     name:'Hemorrhaging',        icon:'💉', cost:5,  desc:'Internal bleeding',               requires:['fever'],inf:2,  sev:10, let:10,drug:2, cureRes:3, severity:'severe'},
    {id:'neuro',     name:'Meningitis',          icon:'🧠', cost:4,  desc:'Brain inflammation',              requires:['fever'],inf:4,  sev:10, let:7, drug:2, cureRes:2, severity:'severe'},
    {id:'nausea',    name:'Nausea',              icon:'🤢', cost:2,  desc:'Widespread nausea',               requires:[],       inf:4,  sev:5,  let:0, drug:0, cureRes:0, severity:'mild'},
    {id:'vomit',     name:'Vomiting',            icon:'🤮', cost:3,  desc:'Projectile vomiting',             requires:['nausea'],inf:7,  sev:8,  let:2, drug:0, cureRes:1, severity:'severe'},
    {id:'diarrhea',  name:'Diarrhea',            icon:'💩', cost:2,  desc:'Rapid fluid spread',              requires:['nausea'],inf:8,  sev:4,  let:1, drug:0, cureRes:0, severity:'mild'},
    {id:'septic',    name:'Septicaemia',         icon:'☠', cost:6,  desc:'Blood poisoning. Highly lethal',  requires:['hemor'],inf:2,  sev:8,  let:18,drug:3, cureRes:4, severity:'lethal'},
    {id:'organ',     name:'Total Organ Failure', icon:'💀', cost:7,  desc:'All organs fail. Near-certain death',requires:['septic'],inf:1,sev:5, let:24,drug:4, cureRes:5, severity:'lethal'},
    {id:'coma',      name:'Coma',                icon:'😵', cost:5,  desc:'Victims fall into coma',          requires:['neuro'],inf:1,  sev:8,  let:12,drug:3, cureRes:3, severity:'lethal'},
    {id:'paralysis', name:'Paralysis',           icon:'🦽', cost:5,  desc:'Nerve damage causes paralysis',   requires:['neuro'],inf:2,  sev:10, let:8, drug:2, cureRes:4, severity:'severe'},
    {id:'insomnia',  name:'Insomnia',            icon:'😴', cost:3,  desc:'Disrupts sleep and cognition',    requires:['fever'],inf:5,  sev:6,  let:2, drug:1, cureRes:1, severity:'mild'},
  ],
  abilities: [
    {id:'drug1',     name:'Drug Resistance 1',   icon:'💊', cost:3,  desc:'Resistant to basic treatments',   requires:[],       inf:0,  sev:0,  let:0, drug:10,cureRes:4},
    {id:'drug2',     name:'Drug Resistance 2',   icon:'🧪', cost:5,  desc:'Resistant to all standard drugs', requires:['drug1'],inf:0,  sev:0,  let:0, drug:18,cureRes:8},
    {id:'drug3',     name:'Total Drug Immunity',  icon:'🛡', cost:8,  desc:'Immune to all known drugs',       requires:['drug2'],inf:0,  sev:0,  let:0, drug:30,cureRes:15},
    {id:'cold1',     name:'Cold Resistance',      icon:'🧊', cost:3,  desc:'Survives in cold climates',       requires:[],       inf:6,  sev:0,  let:0, drug:0, cureRes:1},
    {id:'heat1',     name:'Heat Resistance',      icon:'🔥', cost:3,  desc:'Survives in hot climates',        requires:[],       inf:6,  sev:0,  let:0, drug:0, cureRes:1},
    {id:'env1',      name:'Environmental Hardening',icon:'🌍',cost:4, desc:'Survives outside the host',       requires:['cold1','heat1'],inf:8,sev:0,let:0,drug:2,cureRes:2},
    {id:'stealth',   name:'Genetic Hardening',    icon:'🧬', cost:4,  desc:'Slows cure development',          requires:[],       inf:0,  sev:0,  let:0, drug:5, cureRes:20},
    {id:'stealth2',  name:'Gene Scramble',        icon:'🔬', cost:6,  desc:'Greatly slows cure',              requires:['stealth'],inf:0,sev:0, let:0, drug:8, cureRes:35},
    {id:'mutation',  name:'Genetic Re-coding',    icon:'🦠', cost:5,  desc:'Random beneficial mutations',     requires:[],       inf:5,  sev:3,  let:3, drug:5, cureRes:5},
    {id:'zoonotic',  name:'Zoonotic Leap',        icon:'🐾', cost:4,  desc:'Jumps between animal species',    requires:[],       inf:12, sev:2,  let:1, drug:0, cureRes:2},
    {id:'biofilm',   name:'Biofilm Growth',       icon:'🟢', cost:4,  desc:'Protects against immune response',requires:[],       inf:3,  sev:2,  let:3, drug:8, cureRes:6},
    {id:'dormant',   name:'Dormancy',             icon:'😴', cost:5,  desc:'Lies dormant to avoid detection', requires:[],       inf:4,  sev:0,  let:0, drug:5, cureRes:8},
  ]
};

// ── GAME STATE ──
let G = null; // main game state

function initState(diseaseName, pathType, startCountry, difficulty){
  const diffMult = {casual:0.4, normal:1.0, brutal:1.8, 'mega':3.0}[difficulty] || 1.0;
  const typeBonus = {
    bacteria:  {inf:1.0, let:1.0, drug:1.0, cureSpeed:1.0},
    virus:     {inf:1.3, let:1.1, drug:0.8, cureSpeed:1.2},
    fungus:    {inf:0.9, let:1.0, drug:1.4, cureSpeed:0.8},
    parasite:  {inf:1.1, let:1.0, drug:1.1, cureSpeed:0.7},
    prion:     {inf:0.8, let:1.3, drug:1.5, cureSpeed:0.6},
    nano:      {inf:1.2, let:1.2, drug:1.3, cureSpeed:1.1},
  }[pathType] || {inf:1.0,let:1.0,drug:1.0,cureSpeed:1.0};

  // Init country state
  const regions = {};
  for(const [id, data] of Object.entries(COUNTRIES)){
    regions[id] = {
      ...data,
      id,
      infected: 0,
      dead: 0,
      cured: 0,
      healthy: data.pop,
      active: false,
      lockdown: false,
      airport: true,
      port: ['c-southamerica','c-africa','c-southasia','c-seasia','c-indonesia','c-oceania','c-uk'].includes(id),
    };
  }

  // Seed the starting country
  const seed = Math.floor(regions[startCountry].pop * 0.00001);
  regions[startCountry].infected = seed;
  regions[startCountry].healthy  -= seed;
  regions[startCountry].active   = true;

  G = {
    name: diseaseName,
    type: pathType,
    difficulty: diffMult,
    typeBonus,
    day: 0,
    dna: 0,
    running: false,
    paused: false,
    speed: 1,
    regions,
    owned: new Set(),
    // base stats
    infectivity: 2 * typeBonus.inf,
    lethality:   0.1,
    severity:    2,
    drugResist:  0,
    cureResist:  0,
    // cure
    cureProgress: 0,
    cureActive:   false,
    cureSpeed:    0,
    govActions:   [],
    govLog:       [],
    newsQueue:    [],
    mutationLog:  [],
    symptoms:     [],
    vaccineDeployed: false,
    totalInfected: seed,
    totalDead: 0,
    // tick counter
    tick: 0,
    ticksPerDay: 60, // at speed 1
  };
}

// ── SETUP UI ──
let selectedType = 'bacteria';
let selectedDiff = 'casual';

document.querySelectorAll('.type-btn').forEach(btn=>{
  btn.addEventListener('click',()=>{
    document.querySelectorAll('.type-btn').forEach(b=>b.classList.remove('sel'));
    btn.classList.add('sel');
    selectedType = btn.dataset.type;
  });
});
document.querySelectorAll('.diff-btn').forEach(btn=>{
  btn.addEventListener('click',()=>{
    document.querySelectorAll('.diff-btn').forEach(b=>b.classList.remove('sel'));
    btn.classList.add('sel');
    selectedDiff = btn.dataset.diff;
  });
});

document.getElementById('start-game-btn').addEventListener('click',()=>{
  const name = document.getElementById('dis-name').value.trim() || 'Unknown Pathogen';
  const country = document.getElementById('start-country').value;
  startGame(name, selectedType, country, selectedDiff);
});

// ── TABS ──
document.querySelectorAll('.tab').forEach(tab=>{
  tab.addEventListener('click',()=>{
    document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
    document.querySelectorAll('.tab-content').forEach(c=>c.style.display='none');
    tab.classList.add('active');
    document.getElementById('tab-'+tab.dataset.tab).style.display='block';
  });
});

// ── UPGRADE RENDERING ──
function renderUpgrades(){
  ['transmission','symptoms','abilities'].forEach(cat=>{
    const container = document.getElementById('upg-'+cat);
    container.innerHTML = '';
    UPGRADES[cat].forEach(upg=>{
      const owned    = G.owned.has(upg.id);
      const requires = upg.requires.every(r=>G.owned.has(r));
      const canAfford= G.dna >= upg.cost;
      const affordable = !owned && requires && canAfford;
      const locked   = !requires && !owned;

      const div = document.createElement('div');
      div.className = 'upgrade-node' + (owned?' owned':(locked?' locked':(affordable?' affordable':'')));
      div.innerHTML = `
        <span class="upg-icon">${upg.icon}</span>
        <div class="upg-info">
          <div class="upg-name">${upg.name}</div>
          <div class="upg-desc">${upg.desc}</div>
        </div>
        <span class="upg-cost ${owned?'owned':''}">${owned?'✓':('⚗'+upg.cost)}</span>
      `;
      if(!owned && !locked){
        div.addEventListener('click',()=>buyUpgrade(upg, cat));
      }
      container.appendChild(div);
    });
  });
}

function buyUpgrade(upg, cat){
  if(G.dna < upg.cost){ notify('⚗ Not enough DNA points! Need '+upg.cost); return; }
  if(!upg.requires.every(r=>G.owned.has(r))){ notify('⚠ Prerequisites not met'); return; }
  if(G.owned.has(upg.id)) return;

  G.dna -= upg.cost;
  G.owned.add(upg.id);
  G.infectivity += upg.inf  * G.typeBonus.inf;
  G.lethality   += upg.let  * 0.05;
  G.severity    += upg.sev;
  G.drugResist  += upg.drug;
  G.cureResist  += upg.cureRes;

  if(upg.severity) G.symptoms.push(upg);

  dnaPopup(-upg.cost);
  notify(`🧬 Evolved: ${upg.icon} ${upg.name}`);
  G.mutationLog.unshift(`Day ${G.day}: Evolved ${upg.name}`);
  addNews(`Scientists detect unusual mutation: ${upg.name} variant spreading.`);
  renderUpgrades();
  updateDiseaseTab();
}

// ── GAME LOOP ──
let gameInterval = null;

function startGame(name, type, country, diff){
  initState(name, type, country, diff);
  document.getElementById('setup-screen').style.display = 'none';
  document.getElementById('game-ui').style.display = 'flex';
  document.getElementById('speed-bar').style.display = 'flex';
  renderUpgrades();
  updateCountryList();
  G.running = true;
  runLoop();
  notify(`☣ ${name} has been detected in ${COUNTRIES[country].name}!`);
  addNews(`Breaking: Unusual illness reported. Health authorities monitoring.`);
}

function runLoop(){
  if(gameInterval) clearInterval(gameInterval);
  const ms = Math.max(16, Math.floor(1000 / (G.speed * 20)));
  gameInterval = setInterval(gameTick, ms);
}

function setSpeed(s){
  G.speed = s;
  document.querySelectorAll('.speed-btn[data-speed]').forEach(b=>{
    b.classList.toggle('active', parseInt(b.dataset.speed)===s);
  });
  runLoop();
}

function togglePause(){
  G.paused = !G.paused;
  document.getElementById('pause-btn').textContent = G.paused ? '▶ RESUME' : '⏸ PAUSE';
}

function gameTick(){
  if(!G || !G.running || G.paused) return;

  G.tick++;
  if(G.tick % G.ticksPerDay !== 0) return;

  G.day++;
  document.getElementById('day-display').textContent = `DAY ${G.day}`;

  spreadDisease();
  killPeople();
  giveDNA();
  progressCure();
  randomEvents();
  checkWinLose();
  updateHUD();
  updateCountryList();
  if(G.day % 5 === 0) updateDiseaseTab();
}

function spreadDisease(){
  const regions = Object.values(G.regions);
  const totalInfected = regions.reduce((s,r)=>s+r.infected,0);
  const worldInfPct = totalInfected / WORLD_POP;

  regions.forEach(r=>{
    if(!r.active || r.healthy <= 0) return;

    // Base spread rate
    let spread = r.infected * (G.infectivity / 100) * 0.12;

    // Climate modifiers
    if(r.climate === 'tropical' && G.owned.has('heat1')) spread *= 1.3;
    if(r.climate === 'cold'     && G.owned.has('cold1')) spread *= 1.3;
    if(r.climate === 'arid'     && G.owned.has('heat1')) spread *= 1.2;

    // Lockdown reduces spread
    if(r.lockdown) spread *= 0.2;

    spread = Math.floor(Math.min(spread, r.healthy));
    if(spread > 0){
      r.infected += spread;
      r.healthy  -= spread;
      G.totalInfected += spread;
    }
  });

  // Cross-border spread
  if(G.day % 3 === 0){
    regions.forEach(r=>{
      if(!r.active || r.infected < 100) return;
      r.neighbors.forEach(nid=>{
        const n = G.regions[nid];
        if(!n || n.healthy <= 0) return;
        if(n.active) return; // already infected

        let chance = (r.infected / r.pop) * 0.08 * G.infectivity;
        if(n.lockdown) chance *= 0.05;
        if(!r.airport && !r.port) chance *= 0.3;

        if(Math.random() < chance){
          const seed = Math.max(1, Math.floor(n.pop * 0.00005));
          n.infected += seed;
          n.healthy  -= seed;
          n.active    = true;
          G.totalInfected += seed;
          notify(`✈ ${G.name} has reached ${n.name}!`);
          addNews(`Health alert: ${G.name} cases confirmed in ${n.name}.`);
          spawnInfectionPulse(n.cx, n.cy);
          updateMapColors();
        }
      });
    });
  }

  updateMapColors();
}

function killPeople(){
  if(G.lethality <= 0) return;
  Object.values(G.regions).forEach(r=>{
    if(!r.active || r.infected <= 0) return;
    let deaths = Math.floor(r.infected * G.lethality * 0.008);
    deaths = Math.min(deaths, r.infected);
    if(deaths > 0){
      r.infected -= deaths;
      r.dead     += deaths;
      G.totalDead += deaths;
    }
  });
}

function giveDNA(){
  // DNA from infections and deaths
  const regions = Object.values(G.regions);
  const totalInf = regions.reduce((s,r)=>s+r.infected,0);
  const infPop = totalInf / WORLD_POP;

  let dnaGain = 0;
  // base trickle
  dnaGain += Math.floor(infPop * 4 + 0.5);
  // bonus from deaths
  dnaGain += Math.floor(G.totalDead / 5_000_000);
  // random mutation events
  if(Math.random() < 0.08 + infPop * 0.1) dnaGain += 1;

  if(dnaGain > 0){
    G.dna += dnaGain;
    updateHUD();
    renderUpgrades(); // re-check affordability
  }
}

function progressCure(){
  const regions = Object.values(G.regions);
  const totalInf = regions.reduce((s,r)=>s+r.infected,0);
  const infPop   = totalInf / WORLD_POP;

  // Cure starts when ~10% world infected or severity is high
  if(!G.cureActive && (infPop > 0.1 || G.severity > 30)){
    G.cureActive = true;
    notify('🔬 World Health Organization has begun developing a cure!');
    addNews(`WHO declares global health emergency. Cure research initiated.`);
  }
  if(!G.cureActive) return;

  // Cure speed based on infected nations' wealth
  let labPower = 0;
  let labCount = 0;
  regions.forEach(r=>{
    if(r.active){
      labCount++;
      const w = {rich:3, medium:1.5, poor:0.7}[r.wealth] || 1;
      labPower += w * (!r.lockdown ? 1 : 1.5);
    }
  });
  document.getElementById('labs-active').textContent = labCount;

  // Base cure increment
  let cureInc = labPower * 0.003 * G.difficulty * G.typeBonus.cureSpeed;
  // Resistance slows cure
  cureInc *= Math.max(0.05, 1 - G.cureResist / 200);
  G.cureSpeed = cureInc;
  document.getElementById('cure-speed-disp').textContent = (cureInc*100).toFixed(3)+'%/day';

  G.cureProgress = Math.min(100, G.cureProgress + cureInc);

  // Government responses at cure thresholds
  checkGovResponse();

  if(G.cureProgress >= 100 && !G.vaccineDeployed){
    G.vaccineDeployed = true;
    notify('💉 A CURE HAS BEEN DEVELOPED! Vaccination campaigns beginning...');
    addNews(`VACCINE BREAKTHROUGH: Mass vaccination begins worldwide.`);
    startVaccination();
  }
}

function startVaccination(){
  // Cured people start recovering
  const vaccTimer = setInterval(()=>{
    if(!G || !G.running){ clearInterval(vaccTimer); return; }
    let allCured = true;
    Object.values(G.regions).forEach(r=>{
      if(r.infected > 0){
        allCured = false;
        const vacc = Math.floor(r.infected * 0.05 * (1 - G.cureResist/300));
        const cured = Math.max(0,vacc);
        r.infected -= cured;
        r.cured    += cured;
        if(r.infected < 0) r.infected = 0;
      }
    });
    updateMapColors();
    updateHUD();
    if(allCured) clearInterval(vaccTimer);
  }, 400);
}

function checkGovResponse(){
  const p = G.cureProgress;
  const govLog = document.getElementById('gov-log');

  const events = [
    {at:5,  msg:'🏥 Hospitals on alert. Triage protocols activated.'},
    {at:10, msg:'✈ International travel warnings issued.'},
    {at:20, msg:'🔒 Quarantine zones established in affected regions.'},
    {at:30, msg:'📺 Public health campaigns launched. Hand washing mandated.'},
    {at:40, msg:'🏫 Schools and universities closed in outbreak zones.'},
    {at:50, msg:'🔒 National lockdowns implemented in high-risk countries.'},
    {at:60, msg:'💊 Emergency drug trials fast-tracked globally.'},
    {at:70, msg:'🛬 All international travel suspended.'},
    {at:80, msg:'🧬 Gene sequencing identifies cure pathway.'},
    {at:90, msg:'💉 Vaccine prototype enters human trials.'},
    {at:95, msg:'🌍 Mass vaccine production begins.'},
  ];

  events.forEach(ev=>{
    if(p >= ev.at && !G.govActions.includes(ev.at)){
      G.govActions.push(ev.at);
      G.govLog.unshift(`Day ${G.day}: ${ev.msg}`);
      notify(ev.msg);
      addNews(ev.msg.replace(/^./,''));
      // Apply lockdowns at 50%
      if(ev.at === 50){
        Object.values(G.regions).forEach(r=>{ if(r.active && r.wealth==='rich') r.lockdown=true; });
        document.getElementById('lockdowns').textContent = Object.values(G.regions).filter(r=>r.lockdown).length;
      }
    }
  });

  if(G.vaccineDeployed) document.getElementById('vaccines').textContent = 'Active';
  govLog.innerHTML = G.govLog.slice(0,15).join('<br>') || 'No actions yet.';
}

function randomEvents(){
  if(Math.random() < 0.02){
    const msgs = [
      '🐀 Rodent population boom increases spread vector.',
      '🌍 International conference creates new transmission hub.',
      '💧 Water treatment facility contaminated.',
      '🛩 Infected flight crew causes international spread.',
      '🎪 Mass gathering event creates super-spreader cluster.',
      '📦 Contaminated shipping containers detected.',
    ];
    const msg = msgs[Math.floor(Math.random()*msgs.length)];
    addNews(msg);
    G.infectivity = Math.min(100, G.infectivity + 1);
  }
}

function checkWinLose(){
  const regions = Object.values(G.regions);
  const totalInf  = regions.reduce((s,r)=>s+r.infected,0);
  const totalDead = regions.reduce((s,r)=>s+r.dead,0);
  const totalCured= regions.reduce((s,r)=>s+r.cured,0);
  const totalAlive= WORLD_POP - totalDead;

  // WIN: Everyone dead
  if(totalDead + totalInf >= WORLD_POP * 0.999 && totalInf < 100){
    endGame(true, totalDead, totalInf);
    return;
  }

  // LOSE: Cure complete and no more infected
  if(G.vaccineDeployed && totalInf < 1000 && totalCured > 100000){
    endGame(false, totalDead, totalInf);
    return;
  }
}

function endGame(won, dead, infected){
  G.running = false;
  clearInterval(gameInterval);
  const overlay = document.getElementById('overlay');
  const box     = document.getElementById('overlay-box');
  const title   = document.getElementById('overlay-title');
  const msg     = document.getElementById('overlay-msg');

  overlay.style.display = 'flex'; overlay.style.alignItems = 'center'; overlay.style.justifyContent = 'center';
  if(won){
    box.className = 'overlay-box win-box';
    title.textContent = '☠ HUMANITY EXTINCT';
    title.style.color = '#cc2222';
    msg.innerHTML = `<strong>${G.name}</strong> has successfully eradicated all human life.<br><br>
      ${fmtNum(dead)} killed over ${G.day} days.<br>
      Pathogen type: ${G.type}<br>
      Upgrades evolved: ${G.owned.size}<br><br>
      <em>The Earth is silent.</em>`;
  } else {
    box.className = 'overlay-box';
    title.textContent = '💉 CURE FOUND';
    title.style.color = '#00b4a0';
    msg.innerHTML = `A vaccine was developed before <strong>${G.name}</strong> could finish its work.<br><br>
      ${fmtNum(dead)} casualties over ${G.day} days.<br>
      ${fmtNum(infected)} infected at peak.<br>
      Humanity survives — for now.<br><br>
      <em>Try a higher difficulty or evolve faster.</em>`;
  }
}

function resetGame(){
  if(gameInterval) clearInterval(gameInterval);
  G = null;
  document.getElementById('overlay').style.display = 'none';
  document.getElementById('setup-screen').style.display = 'flex';
  document.getElementById('game-ui').style.display = 'none';
  document.getElementById('speed-bar').style.display = 'none';
  updateHUD();
}

// ── HUD UPDATES ──
function updateHUD(){
  const regions = Object.values(G ? G.regions : {});
  const inf  = regions.reduce((s,r)=>s+r.infected,0);
  const dead = regions.reduce((s,r)=>s+r.dead,0);
  const hlth = Math.max(0, WORLD_POP - inf - dead);
  document.getElementById('h-infected').textContent = fmtNum(inf);
  document.getElementById('h-dead').textContent     = fmtNum(dead);
  document.getElementById('h-healthy').textContent  = fmtNum(hlth);
  document.getElementById('h-dna').textContent      = G ? G.dna : 0;
  document.getElementById('cure-pct').textContent   = G ? G.cureProgress.toFixed(1)+'%' : '0%';
  document.getElementById('cure-bar').style.width   = G ? G.cureProgress+'%' : '0%';
}

function updateDiseaseTab(){
  if(!G) return;
  const inf = Math.min(100, G.infectivity);
  const let_ = Math.min(100, G.lethality * 50);
  const sev = Math.min(100, G.severity * 1.5);
  const dr = Math.min(100, G.drugResist);
  const cr = Math.min(100, G.cureResist);

  document.getElementById('stat-inf').textContent = Math.round(G.infectivity);
  document.getElementById('bar-inf').style.width = inf+'%';
  document.getElementById('stat-let').textContent = Math.round(G.lethality*100)/100;
  document.getElementById('bar-let').style.width = let_+'%';
  document.getElementById('stat-sev').textContent = Math.round(G.severity);
  document.getElementById('bar-sev').style.width = sev+'%';
  document.getElementById('stat-drug').textContent = Math.round(G.drugResist);
  document.getElementById('bar-drug').style.width = dr+'%';
  document.getElementById('stat-cure-res').textContent = Math.round(G.cureResist);
  document.getElementById('bar-cure-res').style.width = cr+'%';

  // Symptoms
  const symDiv = document.getElementById('symptom-list');
  if(G.symptoms.length === 0){ symDiv.innerHTML = '<span style="color:var(--dim);font-size:0.7rem">No symptoms evolved</span>'; }
  else { symDiv.innerHTML = G.symptoms.map(s=>`<span class="symptom-tag ${s.severity}">${s.icon} ${s.name}</span>`).join(''); }

  // Mutation log
  document.getElementById('mutation-log').innerHTML =
    G.mutationLog.slice(0,8).join('<br>') || 'No mutations yet.';
}

function updateCountryList(){
  if(!G) return;
  const list = document.getElementById('country-list');
  const items = Object.values(G.regions)
    .filter(r=>r.active || r.dead > 0)
    .sort((a,b)=>(b.infected+b.dead)-(a.infected+a.dead));

  list.innerHTML = items.map(r=>{
    const infPct = ((r.infected/r.pop)*100).toFixed(1);
    const deadPct= ((r.dead/r.pop)*100).toFixed(1);
    const status = r.lockdown ? '🔒' : r.active ? '☣' : '✓';
    return `<div class="stat-row" style="flex-direction:column;align-items:flex-start;gap:0.2rem;padding:0.4rem 0;">
      <div style="display:flex;justify-content:space-between;width:100%">
        <span style="font-size:0.7rem;color:var(--cream)">${status} ${r.name}</span>
        <span style="font-size:0.65rem;color:var(--dim)">${r.lockdown?'LOCKDOWN':''}</span>
      </div>
      <div style="display:flex;gap:1rem;font-size:0.62rem;">
        <span style="color:var(--red2)">☣ ${fmtNum(r.infected)} (${infPct}%)</span>
        <span style="color:#666">💀 ${fmtNum(r.dead)} (${deadPct}%)</span>
      </div>
      <div class="progress-bar" style="width:100%">
        <div class="progress-fill" style="background:var(--red2);width:${Math.min(100,infPct)}%"></div>
      </div>
    </div>`;
  }).join('') || '<span style="font-size:0.7rem;color:var(--dim)">No regions infected yet.</span>';
}

// ── MAP COLORS ──
function updateMapColors(){
  if(!G) return;
  Object.values(G.regions).forEach(r=>{
    const el = document.getElementById(r.id);
    if(!el) return;
    if(!r.active){ el.className='country healthy'; return; }
    const infPct = r.infected / r.pop;
    const deadPct = r.dead / r.pop;
    if(deadPct > 0.5)      el.className = 'country dead';
    else if(infPct > 0.6)  el.className = 'country critical';
    else if(infPct > 0.3)  el.className = 'country severe';
    else                   el.className = 'country infected';
  });
}

function spawnInfectionPulse(cx, cy){
  const svg = document.getElementById('animSVG');
  const circle = document.createElementNS('http://www.w3.org/2000/svg','circle');
  circle.setAttribute('cx', cx);
  circle.setAttribute('cy', cy);
  circle.setAttribute('r', 4);
  circle.classList.add('infect-pulse');
  svg.appendChild(circle);
  setTimeout(()=>circle.remove(), 1300);
}

// ── NEWS / NOTIFY ──
let notifTimer = null;
function notify(msg){
  const el = document.getElementById('notif');
  el.textContent = msg;
  el.classList.add('show');
  clearTimeout(notifTimer);
  notifTimer = setTimeout(()=>el.classList.remove('show'), 3200);
}

function addNews(msg){
  if(!G) return;
  G.newsQueue.push(msg);
  if(G.newsQueue.length > 5) G.newsQueue.shift();
  document.getElementById('ticker-text').textContent =
    G.newsQueue.join('  •  ');
}

function dnaPopup(delta){
  const wrap = document.getElementById('map-wrap');
  const div  = document.createElement('div');
  div.className = 'dna-popup';
  div.textContent = (delta>0?'+':'')+delta+' ⚗';
  div.style.left = (Math.random()*60+20)+'%';
  div.style.top  = (Math.random()*60+20)+'%';
  div.style.color = delta < 0 ? '#ff4444' : '#e8c97a';
  wrap.appendChild(div);
  setTimeout(()=>div.remove(), 1600);
}

// ── UTILS ──
function fmtNum(n){
  if(n >= 1e9) return (n/1e9).toFixed(2)+'B';
  if(n >= 1e6) return (n/1e6).toFixed(2)+'M';
  if(n >= 1e3) return (n/1e3).toFixed(1)+'K';
  return Math.round(n).toString();
}

// Initial HUD
updateHUD();
</script>

<script>
(function(){

// ═══════════════════════════════════════════
//  PATHOGEN — Full Plague Inc. Game Engine
// ═══════════════════════════════════════════

const WORLD_POP = 8_000_000_000;

// COUNTRIES data
const COUNTRIES = {
  'c-northamerica':  {name:'North America',  pop:500_000_000,  climate:'temperate', wealth:'rich',    cx:165, cy:135, neighbors:['c-centralamerica','c-westeurope','c-easteurope']},
  'c-centralamerica':{name:'Central America',pop:180_000_000,  climate:'tropical',  wealth:'medium',  cx:185, cy:210, neighbors:['c-northamerica','c-southamerica','c-africa']},
  'c-southamerica':  {name:'South America',  pop:440_000_000,  climate:'tropical',  wealth:'medium',  cx:185, cy:310, neighbors:['c-centralamerica']},
  'c-westeurope':    {name:'West Europe',    pop:390_000_000,  climate:'temperate', wealth:'rich',    cx:410, cy:110, neighbors:['c-easteurope','c-northamerica','c-africa','c-middleeast','c-uk']},
  'c-easteurope':    {name:'East Europe',    pop:290_000_000,  climate:'temperate', wealth:'medium',  cx:490, cy:105, neighbors:['c-westeurope','c-russia','c-middleeast']},
  'c-russia':        {name:'Russia',         pop:145_000_000,  climate:'cold',      wealth:'medium',  cx:650, cy:75,  neighbors:['c-easteurope','c-eastasia','c-southasia']},
  'c-middleeast':    {name:'Middle East',    pop:410_000_000,  climate:'arid',      wealth:'medium',  cx:500, cy:165, neighbors:['c-easteurope','c-africa','c-southasia','c-westeurope']},
  'c-africa':        {name:'Africa',         pop:1_400_000_000,climate:'tropical',  wealth:'poor',    cx:415, cy:255, neighbors:['c-westeurope','c-middleeast','c-centralamerica','c-madagascar']},
  'c-southasia':     {name:'South Asia',     pop:1_900_000_000,climate:'tropical',  wealth:'poor',    cx:610, cy:175, neighbors:['c-middleeast','c-eastasia','c-russia','c-seasia']},
  'c-seasia':        {name:'SE Asia',        pop:680_000_000,  climate:'tropical',  wealth:'medium',  cx:710, cy:185, neighbors:['c-southasia','c-eastasia','c-oceania','c-indonesia']},
  'c-eastasia':      {name:'East Asia',      pop:1_600_000_000,climate:'temperate', wealth:'rich',    cx:750, cy:120, neighbors:['c-russia','c-southasia','c-seasia','c-japan']},
  'c-oceania':       {name:'Oceania',        pop:43_000_000,   climate:'temperate', wealth:'rich',    cx:815, cy:320, neighbors:['c-seasia','c-indonesia']},
  'c-japan':         {name:'Japan',          pop:125_000_000,  climate:'temperate', wealth:'rich',    cx:850, cy:120, neighbors:['c-eastasia']},
  'c-uk':            {name:'United Kingdom', pop:67_000_000,   climate:'cold',      wealth:'rich',    cx:360, cy:95,  neighbors:['c-westeurope']},
  'c-greenland':     {name:'Greenland',      pop:56_000,       climate:'cold',      wealth:'rich',    cx:270, cy:55,  neighbors:['c-northamerica']},
  'c-indonesia':     {name:'Indonesia',      pop:275_000_000,  climate:'tropical',  wealth:'medium',  cx:755, cy:245, neighbors:['c-seasia','c-oceania']},
  'c-madagascar':    {name:'Madagascar',     pop:28_000_000,   climate:'tropical',  wealth:'poor',    cx:500, cy:310, neighbors:['c-africa']},
};

// UPGRADE TREES
const UPGRADES = {
  transmission: [
    {id:'air1',      name:'Airborne',          icon:'💨', cost:3,  desc:'Spreads through the air',           requires:[],       inf:8,  sev:1,  let:0, drug:0, cureRes:0},
    {id:'air2',      name:'Aerosol',            icon:'🌫', cost:5,  desc:'Enhanced airborne transmission',    requires:['air1'], inf:14, sev:2,  let:0, drug:0, cureRes:1},
    {id:'air3',      name:'Extreme Drought',    icon:'☁', cost:8,  desc:'Thrives in dry conditions',         requires:['air2'], inf:10, sev:2,  let:1, drug:1, cureRes:1},
    {id:'water1',    name:'Water-borne',         icon:'💧', cost:3,  desc:'Contaminates water supplies',       requires:[],       inf:8,  sev:1,  let:0, drug:0, cureRes:0},
    {id:'water2',    name:'Aquacyte',            icon:'🌊', cost:5,  desc:'Survives in water long-term',       requires:['water1'],inf:12, sev:1, let:0, drug:1, cureRes:0},
    {id:'insect1',   name:'Insect Transmission', icon:'🦟', cost:4,  desc:'Spread by insects',                requires:[],       inf:9,  sev:1,  let:0, drug:0, cureRes:0},
    {id:'insect2',   name:'Bird Transmission',   icon:'🦅', cost:6,  desc:'Spread by birds globally',         requires:['insect1'],inf:14,sev:2, let:0, drug:0, cureRes:1},
    {id:'contact1',  name:'Direct Contact',      icon:'🤝', cost:2,  desc:'Spreads by physical contact',      requires:[],       inf:6,  sev:1,  let:0, drug:0, cureRes:0},
    {id:'contact2',  name:'Saliva Transmission', icon:'😷', cost:3,  desc:'Spreads through saliva',           requires:['contact1'],inf:8, sev:1, let:0, drug:0, cureRes:0},
    {id:'blood1',    name:'Blood-borne',         icon:'🩸', cost:5,  desc:'Spreads via blood contact',        requires:[],       inf:7,  sev:3,  let:2, drug:2, cureRes:1},
  ],
  symptoms: [
    {id:'cough',     name:'Coughing',            icon:'🤧', cost:1,  desc:'Mild respiratory symptom',         requires:[],       inf:5,  sev:3,  let:0, drug:0, cureRes:0, severity:'mild'},
    {id:'fever',     name:'Fever',               icon:'🌡', cost:1,  desc:'Elevated body temperature',        requires:[],       inf:3,  sev:4,  let:1, drug:0, cureRes:0, severity:'mild'},
    {id:'rash',      name:'Skin Rash',           icon:'🔴', cost:2,  desc:'Visible rash increases visibility',requires:['cough'],inf:2,  sev:5,  let:1, drug:0, cureRes:1, severity:'mild'},
    {id:'pulm',      name:'Pulmonary Fibrosis',  icon:'🫁', cost:4,  desc:'Severe lung scarring',             requires:['cough'],inf:3,  sev:12, let:6, drug:2, cureRes:2, severity:'severe'},
    {id:'hemor',     name:'Hemorrhaging',        icon:'💉', cost:5,  desc:'Internal bleeding',               requires:['fever'],inf:2,  sev:10, let:10,drug:2, cureRes:3, severity:'severe'},
    {id:'neuro',     name:'Meningitis',          icon:'🧠', cost:4,  desc:'Brain inflammation',              requires:['fever'],inf:4,  sev:10, let:7, drug:2, cureRes:2, severity:'severe'},
    {id:'nausea',    name:'Nausea',              icon:'🤢', cost:2,  desc:'Widespread nausea',               requires:[],       inf:4,  sev:5,  let:0, drug:0, cureRes:0, severity:'mild'},
    {id:'vomit',     name:'Vomiting',            icon:'🤮', cost:3,  desc:'Projectile vomiting',             requires:['nausea'],inf:7,  sev:8,  let:2, drug:0, cureRes:1, severity:'severe'},
    {id:'diarrhea',  name:'Diarrhea',            icon:'💩', cost:2,  desc:'Rapid fluid spread',              requires:['nausea'],inf:8,  sev:4,  let:1, drug:0, cureRes:0, severity:'mild'},
    {id:'septic',    name:'Septicaemia',         icon:'☠', cost:6,  desc:'Blood poisoning. Highly lethal',  requires:['hemor'],inf:2,  sev:8,  let:18,drug:3, cureRes:4, severity:'lethal'},
    {id:'organ',     name:'Total Organ Failure', icon:'💀', cost:7,  desc:'All organs fail. Near-certain death',requires:['septic'],inf:1,sev:5, let:24,drug:4, cureRes:5, severity:'lethal'},
    {id:'coma',      name:'Coma',                icon:'😵', cost:5,  desc:'Victims fall into coma',          requires:['neuro'],inf:1,  sev:8,  let:12,drug:3, cureRes:3, severity:'lethal'},
    {id:'paralysis', name:'Paralysis',           icon:'🦽', cost:5,  desc:'Nerve damage causes paralysis',   requires:['neuro'],inf:2,  sev:10, let:8, drug:2, cureRes:4, severity:'severe'},
    {id:'insomnia',  name:'Insomnia',            icon:'😴', cost:3,  desc:'Disrupts sleep and cognition',    requires:['fever'],inf:5,  sev:6,  let:2, drug:1, cureRes:1, severity:'mild'},
  ],
  abilities: [
    {id:'drug1',     name:'Drug Resistance 1',   icon:'💊', cost:3,  desc:'Resistant to basic treatments',   requires:[],       inf:0,  sev:0,  let:0, drug:10,cureRes:4},
    {id:'drug2',     name:'Drug Resistance 2',   icon:'🧪', cost:5,  desc:'Resistant to all standard drugs', requires:['drug1'],inf:0,  sev:0,  let:0, drug:18,cureRes:8},
    {id:'drug3',     name:'Total Drug Immunity',  icon:'🛡', cost:8,  desc:'Immune to all known drugs',       requires:['drug2'],inf:0,  sev:0,  let:0, drug:30,cureRes:15},
    {id:'cold1',     name:'Cold Resistance',      icon:'🧊', cost:3,  desc:'Survives in cold climates',       requires:[],       inf:6,  sev:0,  let:0, drug:0, cureRes:1},
    {id:'heat1',     name:'Heat Resistance',      icon:'🔥', cost:3,  desc:'Survives in hot climates',        requires:[],       inf:6,  sev:0,  let:0, drug:0, cureRes:1},
    {id:'env1',      name:'Environmental Hardening',icon:'🌍',cost:4, desc:'Survives outside the host',       requires:['cold1','heat1'],inf:8,sev:0,let:0,drug:2,cureRes:2},
    {id:'stealth',   name:'Genetic Hardening',    icon:'🧬', cost:4,  desc:'Slows cure development',          requires:[],       inf:0,  sev:0,  let:0, drug:5, cureRes:20},
    {id:'stealth2',  name:'Gene Scramble',        icon:'🔬', cost:6,  desc:'Greatly slows cure',              requires:['stealth'],inf:0,sev:0, let:0, drug:8, cureRes:35},
    {id:'mutation',  name:'Genetic Re-coding',    icon:'🦠', cost:5,  desc:'Random beneficial mutations',     requires:[],       inf:5,  sev:3,  let:3, drug:5, cureRes:5},
    {id:'zoonotic',  name:'Zoonotic Leap',        icon:'🐾', cost:4,  desc:'Jumps between animal species',    requires:[],       inf:12, sev:2,  let:1, drug:0, cureRes:2},
    {id:'biofilm',   name:'Biofilm Growth',       icon:'🟢', cost:4,  desc:'Protects against immune response',requires:[],       inf:3,  sev:2,  let:3, drug:8, cureRes:6},
    {id:'dormant',   name:'Dormancy',             icon:'😴', cost:5,  desc:'Lies dormant to avoid detection', requires:[],       inf:4,  sev:0,  let:0, drug:5, cureRes:8},
  ]
};

// ── GAME STATE ──
let G = null; // main game state

function initState(diseaseName, pathType, startCountry, difficulty){
  const diffMult = {casual:0.4, normal:1.0, brutal:1.8, 'mega':3.0}[difficulty] || 1.0;
  const typeBonus = {
    bacteria:  {inf:1.0, let:1.0, drug:1.0, cureSpeed:1.0},
    virus:     {inf:1.3, let:1.1, drug:0.8, cureSpeed:1.2},
    fungus:    {inf:0.9, let:1.0, drug:1.4, cureSpeed:0.8},
    parasite:  {inf:1.1, let:1.0, drug:1.1, cureSpeed:0.7},
    prion:     {inf:0.8, let:1.3, drug:1.5, cureSpeed:0.6},
    nano:      {inf:1.2, let:1.2, drug:1.3, cureSpeed:1.1},
  }[pathType] || {inf:1.0,let:1.0,drug:1.0,cureSpeed:1.0};

  // Init country state
  const regions = {};
  for(const [id, data] of Object.entries(COUNTRIES)){
    regions[id] = {
      ...data,
      id,
      infected: 0,
      dead: 0,
      cured: 0,
      healthy: data.pop,
      active: false,
      lockdown: false,
      airport: true,
      port: ['c-southamerica','c-africa','c-southasia','c-seasia','c-indonesia','c-oceania','c-uk'].includes(id),
    };
  }

  // Seed the starting country
  const seed = Math.floor(regions[startCountry].pop * 0.00001);
  regions[startCountry].infected = seed;
  regions[startCountry].healthy  -= seed;
  regions[startCountry].active   = true;

  G = {
    name: diseaseName,
    type: pathType,
    difficulty: diffMult,
    typeBonus,
    day: 0,
    dna: 0,
    running: false,
    paused: false,
    speed: 1,
    regions,
    owned: new Set(),
    // base stats
    infectivity: 2 * typeBonus.inf,
    lethality:   0.1,
    severity:    2,
    drugResist:  0,
    cureResist:  0,
    // cure
    cureProgress: 0,
    cureActive:   false,
    cureSpeed:    0,
    govActions:   [],
    govLog:       [],
    newsQueue:    [],
    mutationLog:  [],
    symptoms:     [],
    vaccineDeployed: false,
    totalInfected: seed,
    totalDead: 0,
    // tick counter
    tick: 0,
    ticksPerDay: 60, // at speed 1
  };
}

// ── SETUP UI ──
let selectedType = 'bacteria';
let selectedDiff = 'casual';

document.querySelectorAll('.type-btn').forEach(btn=>{
  btn.addEventListener('click',()=>{
    document.querySelectorAll('.type-btn').forEach(b=>b.classList.remove('sel'));
    btn.classList.add('sel');
    selectedType = btn.dataset.type;
  });
});
document.querySelectorAll('.diff-btn').forEach(btn=>{
  btn.addEventListener('click',()=>{
    document.querySelectorAll('.diff-btn').forEach(b=>b.classList.remove('sel'));
    btn.classList.add('sel');
    selectedDiff = btn.dataset.diff;
  });
});

document.getElementById('start-game-btn').addEventListener('click',()=>{
  const name = document.getElementById('dis-name').value.trim() || 'Unknown Pathogen';
  const country = document.getElementById('start-country').value;
  startGame(name, selectedType, country, selectedDiff);
});

// ── TABS ──
document.querySelectorAll('.tab').forEach(tab=>{
  tab.addEventListener('click',()=>{
    document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
    document.querySelectorAll('.tab-content').forEach(c=>c.style.display='none');
    tab.classList.add('active');
    document.getElementById('tab-'+tab.dataset.tab).style.display='block';
  });
});

// ── UPGRADE RENDERING ──
function renderUpgrades(){
  ['transmission','symptoms','abilities'].forEach(cat=>{
    const container = document.getElementById('upg-'+cat);
    container.innerHTML = '';
    UPGRADES[cat].forEach(upg=>{
      const owned    = G.owned.has(upg.id);
      const requires = upg.requires.every(r=>G.owned.has(r));
      const canAfford= G.dna >= upg.cost;
      const affordable = !owned && requires && canAfford;
      const locked   = !requires && !owned;

      const div = document.createElement('div');
      div.className = 'upgrade-node' + (owned?' owned':(locked?' locked':(affordable?' affordable':'')));
      div.innerHTML = `
        <span class="upg-icon">${upg.icon}</span>
        <div class="upg-info">
          <div class="upg-name">${upg.name}</div>
          <div class="upg-desc">${upg.desc}</div>
        </div>
        <span class="upg-cost ${owned?'owned':''}">${owned?'✓':('⚗'+upg.cost)}</span>
      `;
      if(!owned && !locked){
        div.addEventListener('click',()=>buyUpgrade(upg, cat));
      }
      container.appendChild(div);
    });
  });
}

function buyUpgrade(upg, cat){
  if(G.dna < upg.cost){ notify('⚗ Not enough DNA points! Need '+upg.cost); return; }
  if(!upg.requires.every(r=>G.owned.has(r))){ notify('⚠ Prerequisites not met'); return; }
  if(G.owned.has(upg.id)) return;

  G.dna -= upg.cost;
  G.owned.add(upg.id);
  G.infectivity += upg.inf  * G.typeBonus.inf;
  G.lethality   += upg.let  * 0.05;
  G.severity    += upg.sev;
  G.drugResist  += upg.drug;
  G.cureResist  += upg.cureRes;

  if(upg.severity) G.symptoms.push(upg);

  dnaPopup(-upg.cost);
  notify(`🧬 Evolved: ${upg.icon} ${upg.name}`);
  G.mutationLog.unshift(`Day ${G.day}: Evolved ${upg.name}`);
  addNews(`Scientists detect unusual mutation: ${upg.name} variant spreading.`);
  renderUpgrades();
  updateDiseaseTab();
}

// ── GAME LOOP ──
let gameInterval = null;

function startGame(name, type, country, diff){
  initState(name, type, country, diff);
  document.getElementById('setup-screen').style.display = 'none';
  document.getElementById('game-ui').style.display = 'flex';
  document.getElementById('speed-bar').style.display = 'flex';
  renderUpgrades();
  updateCountryList();
  G.running = true;
  runLoop();
  notify(`☣ ${name} has been detected in ${COUNTRIES[country].name}!`);
  addNews(`Breaking: Unusual illness reported. Health authorities monitoring.`);
}

function runLoop(){
  if(gameInterval) clearInterval(gameInterval);
  const ms = Math.max(16, Math.floor(1000 / (G.speed * 20)));
  gameInterval = setInterval(gameTick, ms);
}

function setSpeed(s){
  G.speed = s;
  document.querySelectorAll('.speed-btn[data-speed]').forEach(b=>{
    b.classList.toggle('active', parseInt(b.dataset.speed)===s);
  });
  runLoop();
}

function togglePause(){
  G.paused = !G.paused;
  document.getElementById('pause-btn').textContent = G.paused ? '▶ RESUME' : '⏸ PAUSE';
}

function gameTick(){
  if(!G || !G.running || G.paused) return;

  G.tick++;
  if(G.tick % G.ticksPerDay !== 0) return;

  G.day++;
  document.getElementById('day-display').textContent = `DAY ${G.day}`;

  spreadDisease();
  killPeople();
  giveDNA();
  progressCure();
  randomEvents();
  checkWinLose();
  updateHUD();
  updateCountryList();
  if(G.day % 5 === 0) updateDiseaseTab();
}

function spreadDisease(){
  const regions = Object.values(G.regions);
  const totalInfected = regions.reduce((s,r)=>s+r.infected,0);
  const worldInfPct = totalInfected / WORLD_POP;

  regions.forEach(r=>{
    if(!r.active || r.healthy <= 0) return;

    // Base spread rate
    let spread = r.infected * (G.infectivity / 100) * 0.12;

    // Climate modifiers
    if(r.climate === 'tropical' && G.owned.has('heat1')) spread *= 1.3;
    if(r.climate === 'cold'     && G.owned.has('cold1')) spread *= 1.3;
    if(r.climate === 'arid'     && G.owned.has('heat1')) spread *= 1.2;

    // Lockdown reduces spread
    if(r.lockdown) spread *= 0.2;

    spread = Math.floor(Math.min(spread, r.healthy));
    if(spread > 0){
      r.infected += spread;
      r.healthy  -= spread;
      G.totalInfected += spread;
    }
  });

  // Cross-border spread
  if(G.day % 3 === 0){
    regions.forEach(r=>{
      if(!r.active || r.infected < 100) return;
      r.neighbors.forEach(nid=>{
        const n = G.regions[nid];
        if(!n || n.healthy <= 0) return;
        if(n.active) return; // already infected

        let chance = (r.infected / r.pop) * 0.08 * G.infectivity;
        if(n.lockdown) chance *= 0.05;
        if(!r.airport && !r.port) chance *= 0.3;

        if(Math.random() < chance){
          const seed = Math.max(1, Math.floor(n.pop * 0.00005));
          n.infected += seed;
          n.healthy  -= seed;
          n.active    = true;
          G.totalInfected += seed;
          notify(`✈ ${G.name} has reached ${n.name}!`);
          addNews(`Health alert: ${G.name} cases confirmed in ${n.name}.`);
          spawnInfectionPulse(n.cx, n.cy);
          updateMapColors();
        }
      });
    });
  }

  updateMapColors();
}

function killPeople(){
  if(G.lethality <= 0) return;
  Object.values(G.regions).forEach(r=>{
    if(!r.active || r.infected <= 0) return;
    let deaths = Math.floor(r.infected * G.lethality * 0.008);
    deaths = Math.min(deaths, r.infected);
    if(deaths > 0){
      r.infected -= deaths;
      r.dead     += deaths;
      G.totalDead += deaths;
    }
  });
}

function giveDNA(){
  // DNA from infections and deaths
  const regions = Object.values(G.regions);
  const totalInf = regions.reduce((s,r)=>s+r.infected,0);
  const infPop = totalInf / WORLD_POP;

  let dnaGain = 0;
  // base trickle
  dnaGain += Math.floor(infPop * 4 + 0.5);
  // bonus from deaths
  dnaGain += Math.floor(G.totalDead / 5_000_000);
  // random mutation events
  if(Math.random() < 0.08 + infPop * 0.1) dnaGain += 1;

  if(dnaGain > 0){
    G.dna += dnaGain;
    updateHUD();
    renderUpgrades(); // re-check affordability
  }
}

function progressCure(){
  const regions = Object.values(G.regions);
  const totalInf = regions.reduce((s,r)=>s+r.infected,0);
  const infPop   = totalInf / WORLD_POP;

  // Cure starts when ~10% world infected or severity is high
  if(!G.cureActive && (infPop > 0.1 || G.severity > 30)){
    G.cureActive = true;
    notify('🔬 World Health Organization has begun developing a cure!');
    addNews(`WHO declares global health emergency. Cure research initiated.`);
  }
  if(!G.cureActive) return;

  // Cure speed based on infected nations' wealth
  let labPower = 0;
  let labCount = 0;
  regions.forEach(r=>{
    if(r.active){
      labCount++;
      const w = {rich:3, medium:1.5, poor:0.7}[r.wealth] || 1;
      labPower += w * (!r.lockdown ? 1 : 1.5);
    }
  });
  document.getElementById('labs-active').textContent = labCount;

  // Base cure increment
  let cureInc = labPower * 0.003 * G.difficulty * G.typeBonus.cureSpeed;
  // Resistance slows cure
  cureInc *= Math.max(0.05, 1 - G.cureResist / 200);
  G.cureSpeed = cureInc;
  document.getElementById('cure-speed-disp').textContent = (cureInc*100).toFixed(3)+'%/day';

  G.cureProgress = Math.min(100, G.cureProgress + cureInc);

  // Government responses at cure thresholds
  checkGovResponse();

  if(G.cureProgress >= 100 && !G.vaccineDeployed){
    G.vaccineDeployed = true;
    notify('💉 A CURE HAS BEEN DEVELOPED! Vaccination campaigns beginning...');
    addNews(`VACCINE BREAKTHROUGH: Mass vaccination begins worldwide.`);
    startVaccination();
  }
}

function startVaccination(){
  // Cured people start recovering
  const vaccTimer = setInterval(()=>{
    if(!G || !G.running){ clearInterval(vaccTimer); return; }
    let allCured = true;
    Object.values(G.regions).forEach(r=>{
      if(r.infected > 0){
        allCured = false;
        const vacc = Math.floor(r.infected * 0.05 * (1 - G.cureResist/300));
        const cured = Math.max(0,vacc);
        r.infected -= cured;
        r.cured    += cured;
        if(r.infected < 0) r.infected = 0;
      }
    });
    updateMapColors();
    updateHUD();
    if(allCured) clearInterval(vaccTimer);
  }, 400);
}

function checkGovResponse(){
  const p = G.cureProgress;
  const govLog = document.getElementById('gov-log');

  const events = [
    {at:5,  msg:'🏥 Hospitals on alert. Triage protocols activated.'},
    {at:10, msg:'✈ International travel warnings issued.'},
    {at:20, msg:'🔒 Quarantine zones established in affected regions.'},
    {at:30, msg:'📺 Public health campaigns launched. Hand washing mandated.'},
    {at:40, msg:'🏫 Schools and universities closed in outbreak zones.'},
    {at:50, msg:'🔒 National lockdowns implemented in high-risk countries.'},
    {at:60, msg:'💊 Emergency drug trials fast-tracked globally.'},
    {at:70, msg:'🛬 All international travel suspended.'},
    {at:80, msg:'🧬 Gene sequencing identifies cure pathway.'},
    {at:90, msg:'💉 Vaccine prototype enters human trials.'},
    {at:95, msg:'🌍 Mass vaccine production begins.'},
  ];

  events.forEach(ev=>{
    if(p >= ev.at && !G.govActions.includes(ev.at)){
      G.govActions.push(ev.at);
      G.govLog.unshift(`Day ${G.day}: ${ev.msg}`);
      notify(ev.msg);
      addNews(ev.msg.replace(/^./,''));
      // Apply lockdowns at 50%
      if(ev.at === 50){
        Object.values(G.regions).forEach(r=>{ if(r.active && r.wealth==='rich') r.lockdown=true; });
        document.getElementById('lockdowns').textContent = Object.values(G.regions).filter(r=>r.lockdown).length;
      }
    }
  });

  if(G.vaccineDeployed) document.getElementById('vaccines').textContent = 'Active';
  govLog.innerHTML = G.govLog.slice(0,15).join('<br>') || 'No actions yet.';
}

function randomEvents(){
  if(Math.random() < 0.02){
    const msgs = [
      '🐀 Rodent population boom increases spread vector.',
      '🌍 International conference creates new transmission hub.',
      '💧 Water treatment facility contaminated.',
      '🛩 Infected flight crew causes international spread.',
      '🎪 Mass gathering event creates super-spreader cluster.',
      '📦 Contaminated shipping containers detected.',
    ];
    const msg = msgs[Math.floor(Math.random()*msgs.length)];
    addNews(msg);
    G.infectivity = Math.min(100, G.infectivity + 1);
  }
}

function checkWinLose(){
  const regions = Object.values(G.regions);
  const totalInf  = regions.reduce((s,r)=>s+r.infected,0);
  const totalDead = regions.reduce((s,r)=>s+r.dead,0);
  const totalCured= regions.reduce((s,r)=>s+r.cured,0);
  const totalAlive= WORLD_POP - totalDead;

  // WIN: Everyone dead
  if(totalDead + totalInf >= WORLD_POP * 0.999 && totalInf < 100){
    endGame(true, totalDead, totalInf);
    return;
  }

  // LOSE: Cure complete and no more infected
  if(G.vaccineDeployed && totalInf < 1000 && totalCured > 100000){
    endGame(false, totalDead, totalInf);
    return;
  }
}

function endGame(won, dead, infected){
  G.running = false;
  clearInterval(gameInterval);
  const overlay = document.getElementById('overlay');
  const box     = document.getElementById('overlay-box');
  const title   = document.getElementById('overlay-title');
  const msg     = document.getElementById('overlay-msg');

  overlay.style.display = 'flex'; overlay.style.alignItems = 'center'; overlay.style.justifyContent = 'center';
  if(won){
    box.className = 'overlay-box win-box';
    title.textContent = '☠ HUMANITY EXTINCT';
    title.style.color = '#cc2222';
    msg.innerHTML = `<strong>${G.name}</strong> has successfully eradicated all human life.<br><br>
      ${fmtNum(dead)} killed over ${G.day} days.<br>
      Pathogen type: ${G.type}<br>
      Upgrades evolved: ${G.owned.size}<br><br>
      <em>The Earth is silent.</em>`;
  } else {
    box.className = 'overlay-box';
    title.textContent = '💉 CURE FOUND';
    title.style.color = '#00b4a0';
    msg.innerHTML = `A vaccine was developed before <strong>${G.name}</strong> could finish its work.<br><br>
      ${fmtNum(dead)} casualties over ${G.day} days.<br>
      ${fmtNum(infected)} infected at peak.<br>
      Humanity survives — for now.<br><br>
      <em>Try a higher difficulty or evolve faster.</em>`;
  }
}

function resetGame(){
  if(gameInterval) clearInterval(gameInterval);
  G = null;
  document.getElementById('overlay').style.display = 'none';
  document.getElementById('setup-screen').style.display = 'flex';
  document.getElementById('game-ui').style.display = 'none';
  document.getElementById('speed-bar').style.display = 'none';
  updateHUD();
}

// ── HUD UPDATES ──
function updateHUD(){
  const regions = Object.values(G ? G.regions : {});
  const inf  = regions.reduce((s,r)=>s+r.infected,0);
  const dead = regions.reduce((s,r)=>s+r.dead,0);
  const hlth = Math.max(0, WORLD_POP - inf - dead);
  document.getElementById('h-infected').textContent = fmtNum(inf);
  document.getElementById('h-dead').textContent     = fmtNum(dead);
  document.getElementById('h-healthy').textContent  = fmtNum(hlth);
  document.getElementById('h-dna').textContent      = G ? G.dna : 0;
  document.getElementById('cure-pct').textContent   = G ? G.cureProgress.toFixed(1)+'%' : '0%';
  document.getElementById('cure-bar').style.width   = G ? G.cureProgress+'%' : '0%';
}

function updateDiseaseTab(){
  if(!G) return;
  const inf = Math.min(100, G.infectivity);
  const let_ = Math.min(100, G.lethality * 50);
  const sev = Math.min(100, G.severity * 1.5);
  const dr = Math.min(100, G.drugResist);
  const cr = Math.min(100, G.cureResist);

  document.getElementById('stat-inf').textContent = Math.round(G.infectivity);
  document.getElementById('bar-inf').style.width = inf+'%';
  document.getElementById('stat-let').textContent = Math.round(G.lethality*100)/100;
  document.getElementById('bar-let').style.width = let_+'%';
  document.getElementById('stat-sev').textContent = Math.round(G.severity);
  document.getElementById('bar-sev').style.width = sev+'%';
  document.getElementById('stat-drug').textContent = Math.round(G.drugResist);
  document.getElementById('bar-drug').style.width = dr+'%';
  document.getElementById('stat-cure-res').textContent = Math.round(G.cureResist);
  document.getElementById('bar-cure-res').style.width = cr+'%';

  // Symptoms
  const symDiv = document.getElementById('symptom-list');
  if(G.symptoms.length === 0){ symDiv.innerHTML = '<span style="color:var(--dim);font-size:0.7rem">No symptoms evolved</span>'; }
  else { symDiv.innerHTML = G.symptoms.map(s=>`<span class="symptom-tag ${s.severity}">${s.icon} ${s.name}</span>`).join(''); }

  // Mutation log
  document.getElementById('mutation-log').innerHTML =
    G.mutationLog.slice(0,8).join('<br>') || 'No mutations yet.';
}

function updateCountryList(){
  if(!G) return;
  const list = document.getElementById('country-list');
  const items = Object.values(G.regions)
    .filter(r=>r.active || r.dead > 0)
    .sort((a,b)=>(b.infected+b.dead)-(a.infected+a.dead));

  list.innerHTML = items.map(r=>{
    const infPct = ((r.infected/r.pop)*100).toFixed(1);
    const deadPct= ((r.dead/r.pop)*100).toFixed(1);
    const status = r.lockdown ? '🔒' : r.active ? '☣' : '✓';
    return `<div class="stat-row" style="flex-direction:column;align-items:flex-start;gap:0.2rem;padding:0.4rem 0;">
      <div style="display:flex;justify-content:space-between;width:100%">
        <span style="font-size:0.7rem;color:var(--cream)">${status} ${r.name}</span>
        <span style="font-size:0.65rem;color:var(--dim)">${r.lockdown?'LOCKDOWN':''}</span>
      </div>
      <div style="display:flex;gap:1rem;font-size:0.62rem;">
        <span style="color:var(--red2)">☣ ${fmtNum(r.infected)} (${infPct}%)</span>
        <span style="color:#666">💀 ${fmtNum(r.dead)} (${deadPct}%)</span>
      </div>
      <div class="progress-bar" style="width:100%">
        <div class="progress-fill" style="background:var(--red2);width:${Math.min(100,infPct)}%"></div>
      </div>
    </div>`;
  }).join('') || '<span style="font-size:0.7rem;color:var(--dim)">No regions infected yet.</span>';
}

// ── MAP COLORS ──
function updateMapColors(){
  if(!G) return;
  Object.values(G.regions).forEach(r=>{
    const el = document.getElementById(r.id);
    if(!el) return;
    if(!r.active){ el.className='country healthy'; return; }
    const infPct = r.infected / r.pop;
    const deadPct = r.dead / r.pop;
    if(deadPct > 0.5)      el.className = 'country dead';
    else if(infPct > 0.6)  el.className = 'country critical';
    else if(infPct > 0.3)  el.className = 'country severe';
    else                   el.className = 'country infected';
  });
}

function spawnInfectionPulse(cx, cy){
  const svg = document.getElementById('animSVG');
  const circle = document.createElementNS('http://www.w3.org/2000/svg','circle');
  circle.setAttribute('cx', cx);
  circle.setAttribute('cy', cy);
  circle.setAttribute('r', 4);
  circle.classList.add('infect-pulse');
  svg.appendChild(circle);
  setTimeout(()=>circle.remove(), 1300);
}

// ── NEWS / NOTIFY ──
let notifTimer = null;
function notify(msg){
  const el = document.getElementById('notif');
  el.textContent = msg;
  el.classList.add('show');
  clearTimeout(notifTimer);
  notifTimer = setTimeout(()=>el.classList.remove('show'), 3200);
}

function addNews(msg){
  if(!G) return;
  G.newsQueue.push(msg);
  if(G.newsQueue.length > 5) G.newsQueue.shift();
  document.getElementById('ticker-text').textContent =
    G.newsQueue.join('  •  ');
}

function dnaPopup(delta){
  const wrap = document.getElementById('map-wrap');
  const div  = document.createElement('div');
  div.className = 'dna-popup';
  div.textContent = (delta>0?'+':'')+delta+' ⚗';
  div.style.left = (Math.random()*60+20)+'%';
  div.style.top  = (Math.random()*60+20)+'%';
  div.style.color = delta < 0 ? '#ff4444' : '#e8c97a';
  wrap.appendChild(div);
  setTimeout(()=>div.remove(), 1600);
}

// ── UTILS ──
function fmtNum(n){
  if(n >= 1e9) return (n/1e9).toFixed(2)+'B';
  if(n >= 1e6) return (n/1e6).toFixed(2)+'M';
  if(n >= 1e3) return (n/1e3).toFixed(1)+'K';
  return Math.round(n).toString();
}

// Initial HUD
updateHUD();

})();
</script>
</div>
      <div class="game-controls">
        Evolve your disease · Infect &amp; kill all 8 billion humans · Survive the cure · 6 pathogen types · Full upgrade tree
      </div>
    </div>


    <!-- CENTIPEDE -->
    <div class="game-panel">
      <div class="game-header">
        <div class="game-tag">Arcade · Classic · Shooter</div>
        <div class="game-title">🐛 Ridge Centipede</div>
        <button class="fs-btn" onclick="toggleFS(this)">⛶ Fullscreen</button>
      </div>
      <div class="game-canvas-area" style="flex-direction:column;">
        <canvas id="centCanvas" width="420" height="520"></canvas>
        <div style="display:flex;gap:0.8rem;margin-top:0.6rem;align-items:center;">
          <button class="dpad-btn" style="width:56px;height:44px;font-size:1.2rem;" onmousedown="CENTIPEDE.setDir(-1)" onmouseup="CENTIPEDE.setDir(0)" ontouchstart="CENTIPEDE.setDir(-1)" ontouchend="CENTIPEDE.setDir(0)">◀</button>
          <button class="dpad-btn" style="width:80px;height:44px;font-size:0.7rem;letter-spacing:1px;" onclick="CENTIPEDE.fire()">🔥 FIRE</button>
          <button class="dpad-btn" style="width:56px;height:44px;font-size:1.2rem;" onmousedown="CENTIPEDE.setDir(1)" onmouseup="CENTIPEDE.setDir(0)" ontouchstart="CENTIPEDE.setDir(1)" ontouchend="CENTIPEDE.setDir(0)">▶</button>
        </div>
      </div>
      <div class="game-controls">
        <kbd>←</kbd><kbd>→</kbd> move &nbsp;·&nbsp; <kbd>Space</kbd> shoot &nbsp;·&nbsp; Click canvas to start &nbsp;·&nbsp; Score: <span id="centScore">0</span> &nbsp;·&nbsp; Lives: <span id="centLives">3</span>
      </div>
    </div>

  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="section-label">Get In Touch</div>
  <h2 class="section-title">Contact</h2>
  <div class="divider"></div>
  <p style="max-width:500px;color:rgba(240,236,224,0.65);font-size:0.95rem;line-height:1.8;position:relative;z-index:1;">Reach out for trail tips, collab ideas, or just to talk MTB. Also check out the YouTube channel for riding content.</p>
  <div class="contact-grid">
    <a class="contact-card c-email" href="mailto:bobbydesmarais202@gmail.com">
      <span class="contact-icon">✉️</span>
      <div class="contact-label">Email</div>
      <div class="contact-value">bobbydesmarais202@gmail.com</div>
      <div class="contact-sub">Click to send an email</div>
    </a>
    <a class="contact-card c-phone" href="tel:+19548726880">
      <span class="contact-icon">📱</span>
      <div class="contact-label">Phone</div>
      <div class="contact-value">(954) 872-6880</div>
      <div class="contact-sub">Call or text anytime</div>
    </a>
    <a class="contact-card c-youtube" href="https://www.youtube.com/@BobbytheCarCleaner" target="_blank" rel="noopener">
      <span class="contact-icon">▶️</span>
      <div class="contact-label">YouTube</div>
      <div class="contact-value">Bobby the Car Cleaner</div>
      <div class="contact-sub">Watch on YouTube →</div>
    </a>
  </div>
</section>


<footer>
  <div class="footer-logo">RidgeRush<span class="dash">-</span><span class="mtb">MTB</span></div>
  <div class="footer-links">
    <a href="#practice">Skills Areas</a>
    <a href="#trails">Trails</a>
    <a href="#games">Arcade</a>
    <a href="#contact">Contact</a>
  </div>
  <p class="footer-copy">© 2026 RidgeRush-MTB — Ride at your own risk. Helmets required. Broward County MTB pass required at Markham Park &amp; Quiet Waters.</p>
</footer>

<!-- MAP MODAL -->
<div class="modal-overlay" id="mapModal" onclick="outsideClose(event)">
  <div class="modal-box">
    <div class="modal-header">
      <div>
        <div class="modal-title" id="mTitle"></div>
        <div class="modal-sub" id="mSub"></div>
        <div class="modal-badges" id="mBadges"></div>
      </div>
      <button class="modal-close" onclick="closeModal()">✕ CLOSE</button>
    </div>
    <div class="modal-body">
      <div class="modal-stats" id="mStats"></div>
      <div class="modal-desc" id="mDesc"></div>
      <div class="modal-map">
        <iframe id="mMapFrame" src="" allowfullscreen loading="lazy"></iframe>
      </div>
    </div>
  </div>
</div>

<script>
/* ═══════════ TRAIL DATA ═══════════ */
const TRAILS = [
  // MARKHAM PARK
  {name:"Pump Track",           park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Easy",     dist:"0.1 mi",  feat:"Pump Track, Skills",            desc:"A continuous loop of rollers and banked turns right at the trailhead, across from the Warm Up Loop start. Builds momentum and bike handling at any skill level.",                            q:"Markham+Park+MTB+Trails+Sunrise+Florida"},
  {name:"Warm Up Loop",         park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Easy",     dist:"0.5 mi",  feat:"Berms, Flow",                   desc:"The perfect intro to Markham's MTB system. Intermediate terrain with an advanced split-off near the start. Begins directly across from the pump track.",                                    q:"Markham+Park+MTB+Trails+Sunrise+Florida"},
  {name:"Boomerang",            park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Easy",     dist:"0.3 mi",  feat:"Flow, Beginner",                desc:"One of the best-rated beginner trails at Markham (4/5). A great easy loop that feeds into the Outback Return section of the park.",                                                      q:"Markham+Park+MTB+Trails+Sunrise+Florida"},
  {name:"Fishing Hole Loop",    park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Easy",     dist:"0.5 mi",  feat:"Lakeside, Scenic",              desc:"Scenic lakeside loop with wildlife sightings and a relaxed ride through open meadows near the water. Gopher tortoises and birds are frequent companions.",                                  q:"Markham+Park+MTB+Trails+Sunrise+Florida"},
  {name:"Adaptive Loop",        park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Easy",     dist:"3.1 mi",  feat:"Accessible, Wide",              desc:"The outer loop built for adaptive mountain bikes with hand cranks. Wide, gradual, and welcoming to beginners. One of the few dedicated adaptive MTB loops in Florida.",                     q:"Markham+Park+MTB+Adaptive+Loop+Sunrise+Florida"},
  {name:"Middle Earth",          park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Easy",     dist:"0.3 mi",  feat:"Connector, Flow",               desc:"A green-rated connector trail weaving through the trees at Markham Park, linking sections of the trail network for riders building their first full laps. Easy flow with a woodsy feel — true to its name.",                                                                                                                             q:"Markham+Park+MTB+Trails+Sunrise+Florida"},
  {name:"RTE 66",               park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Moderate", dist:"0.3 mi",  feat:"Flow, Berms, Boardwalk",        desc:"Fast, flowing trail with a new boardwalk on the advanced variant. Commonly linked with Black Snake and Armadillo for a well-rounded loop.",                                                q:"Markham+Park+MTB+Trails+Sunrise+Florida"},
  {name:"Deep Dark Forest",     park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Moderate", dist:"0.4 mi",  feat:"Roots, Singletrack",            desc:"Winding singletrack through dense forest with plenty of roots. Connects to Rock Garden and can serve as a smoother bypass. Most popular trail in the park.",                              q:"Markham+Park+MTB+Deep+Dark+Forest+Sunrise+Florida"},
  {name:"Armadillo",            park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Moderate", dist:"0.5 mi",  feat:"Berms, Climbs",                 desc:"Short climbs followed by fast, flowing berms. The trail with the most elevation gain at Markham at 33 ft. Often linked with Black Snake and RTE 66.",                                   q:"Markham+Park+MTB+Armadillo+Sunrise+Florida"},
  {name:"Traverse Trail",       park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Moderate", dist:"0.5 mi",  feat:"Connector, Flow",               desc:"Third-highest rated trail at Markham. Connects key sections of the trail system after heading left by the lake.",                                                                           q:"Markham+Park+MTB+Trails+Sunrise+Florida"},
  {name:"Las Olas",             park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Moderate", dist:"0.1 mi",  feat:"Flow, Obstacles",               desc:"A 549 ft intermediate trail with flowing sections, quick transitions, and interesting obstacles. Short but satisfying.",                                                                    q:"Markham+Park+MTB+Trails+Sunrise+Florida"},
  {name:"Washing Machine",      park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Moderate", dist:"0.4 mi",  feat:"Connector, Return",             desc:"Connects to Lost Ring and leads back toward the entrance — a useful return route after exploring the far end of the network.",                                                              q:"Markham+Park+MTB+Trails+Sunrise+Florida"},
  {name:"Bermuda Triangle",     park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Moderate", dist:"0.5 mi",  feat:"Twisty, Trees",                 desc:"2,659 ft of twisty singletrack through the trees. Moderate difficulty connecting to Ruben Loop and Deja Vu in the back section.",                                                         q:"Markham+Park+MTB+Bermuda+Triangle+Sunrise+Florida"},
  {name:"Déjà Vu",              park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Moderate", dist:"0.4 mi",  feat:"Flow, Connector",               desc:"A flowing connector trail ridden twice on the full advanced lap. Links Bermuda Triangle, Ruben Loop, and the back section.",                                                               q:"Markham+Park+MTB+Trails+Sunrise+Florida"},
  {name:"Ruben Loop",           park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Moderate", dist:"0.3 mi",  feat:"Loop, Flow",                    desc:"A looping trail between Bermuda Triangle and Déjà Vu. Moderate and fun — great filler on a full lap.",                                                                                     q:"Markham+Park+MTB+Trails+Sunrise+Florida"},
  {name:"Double Cross",         park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Moderate", dist:"0.3 mi",  feat:"Technical, Connector",          desc:"A split-off before Crime Scene in the advanced section. Moderate technical connector leading into the most challenging part of the network.",                                                 q:"Markham+Park+MTB+Trails+Sunrise+Florida"},
  {name:"Rock Garden",          park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Hard",     dist:"0.3 mi",  feat:"Rock Gardens, Drops",           desc:"Technical rocky sections and challenging drops. One of Markham's most beloved and frequently visited trails for testing maneuvering skills.",                                               q:"Markham+Park+MTB+Rock+Garden+Sunrise+Florida"},
  {name:"Iguana Ridge",         park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Hard",     dist:"0.2 mi",  feat:"Ridgeline, Drops",              desc:"Advanced ridgeline with tight turns and an optional drop. A steep climb entry makes it demanding even for intermediate riders.",                                                             q:"Markham+Park+MTB+Iguana+Ridge+Sunrise+Florida"},
  {name:"Iguana Return",        park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Hard",     dist:"0.2 mi",  feat:"Descent, Steepest",             desc:"The steepest trail at Markham at 3% average grade. Expert-level terrain — the hardest trail to ride cleanly in the park.",                                                                q:"Markham+Park+MTB+Iguana+Sunrise+Florida"},
  {name:"OBX Advanced",         park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Hard",     dist:"0.6 mi",  feat:"Top Rated, Expert",             desc:"The highest-rated trail at Markham Park (4.2/5). Expert-level singletrack with challenging features — the top choice for advanced riders.",                                              q:"Markham+Park+MTB+OBX+Sunrise+Florida"},
  {name:"Redback",              park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Hard",     dist:"0.4 mi",  feat:"Descent, Fast",                 desc:"The trail with the most descent at Markham (-25 ft). Fast, flowing descending singletrack rated among the park's very best.",                                                              q:"Markham+Park+MTB+Redback+Sunrise+Florida"},
  {name:"Area 51",              park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Hard",     dist:"0.4 mi",  feat:"Big Berms, Jumps, Drops",       desc:"Big berms, sharp dips, and the optional Pipeline wooden bridge. One of the most technically demanding and thrilling trails at Markham.",                                                  q:"Markham+Park+MTB+Area51+Sunrise+Florida"},
  {name:"Black Snake",          park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Hard",     dist:"0.4 mi",  feat:"Big Gulp, Technical",           desc:"Features the challenging Big Gulp section. Often combined with RTE 66 and Armadillo for a popular well-rounded sequence through the park.",                                               q:"Markham+Park+MTB+Black+Snake+Sunrise+Florida"},
  {name:"Outback",              park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Hard",     dist:"0.6 mi",  feat:"Climbs, Adventure",             desc:"Gut-buster climbs and an exciting outback extension. One of the park's most adventurous sections — described by riders as 'REALLY fun'.",                                                q:"Markham+Park+MTB+Outback+Sunrise+Florida"},
  {name:"Outback Return",       park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Hard",     dist:"0.4 mi",  feat:"Technical, Extension",          desc:"The return from the Outback section with an optional extension that loops back before connecting to Turtle Slide.",                                                                          q:"Markham+Park+MTB+Trails+Sunrise+Florida"},
  {name:"Turtle Slide",         park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Hard",     dist:"0.2 mi",  feat:"Slippery Descent",              desc:"A slippery, technical descent linking Outback Return to Double Cross and Crime Scene. Watch your speed.",                                                                                  q:"Markham+Park+MTB+Trails+Sunrise+Florida"},
  {name:"Pipeline",             park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Hard",     dist:"0.2 mi",  feat:"Wooden Skinny, Technical",      desc:"Features an optional wooden bridge skinny and technical challenges to refine the skills of experienced riders. Part of the Area 51 complex.",                                               q:"Markham+Park+MTB+Pipeline+Sunrise+Florida"},
  {name:"Crime Scene",          park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Hard",     dist:"0.3 mi",  feat:"Steep Climbs, Descents",        desc:"Steep technical climbs and descents. Connects to Jet Ski and Ted's Twisted Trail at the far end of the park. Not for the faint of heart.",                                               q:"Markham+Park+MTB+Crime+Scene+Sunrise+Florida"},
  {name:"Supercross",           park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Hard",     dist:"0.3 mi",  feat:"Big Jumps, High Speed",         desc:"Among the trails with the biggest jumps at Markham Park. Fast, high-energy terrain that rewards riders who carry serious speed.",                                                         q:"Markham+Park+MTB+Supercross+Sunrise+Florida"},
  {name:"Gun Range",            park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Hard",     dist:"1.3 mi",  feat:"Longest, G-Outs, Fast",         desc:"The longest trail at Markham at 1.3 miles. Fast, twisty singletrack with challenging sections, steep g-outs, and technical riding. Expert riders only.",                               q:"Markham+Park+MTB+Gun+Range+Sunrise+Florida"},
  {name:"Semper Fi",            park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Hard",     dist:"0.4 mi",  feat:"Technical, Back Section",       desc:"A demanding technical trail in the back section. Ted's Twisted Trail ends at the bottom of Semper Fi before connecting to Lost Ring.",                                                    q:"Markham+Park+MTB+Trails+Sunrise+Florida"},
  {name:"Lost Ring",            park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Hard",     dist:"0.3 mi",  feat:"Back Section, Technical",       desc:"Located at the furthest back section after Semper Fi and Ted's Twisted Trail. Connects to Déjà Vu on the full advanced lap.",                                                             q:"Markham+Park+MTB+Trails+Sunrise+Florida"},
  {name:"Jet Ski",              park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Expert",   dist:"0.2 mi",  feat:"Drop, Steep Incline",           desc:"A severe-difficulty trail — a 9m incline climb leads straight into a challenging drop. Optional on the full lap but not optional for your heart rate.",                                q:"Markham+Park+MTB+Jet+Ski+Sunrise+Florida"},
  {name:"Ted's Twisted Trail",  park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Expert",   dist:"0.3 mi",  feat:"Fast Downhill, Tight Turns",    desc:"Fast downhill with unpredictable tight turns — don't carry too much speed. Located at the far end of the park past Crime Scene.",                                                    q:"Markham+Park+MTB+Twisted+Trail+Sunrise+Florida"},
  {name:"Yo Mama",              park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Expert",   dist:"0.4 mi",  feat:"Drops, Ramps, Tight Turns",     desc:"Difficult and exciting with technical drops, ramps, and tight turns. One of Markham's most adrenaline-packed trails for expert riders.",                                                q:"Markham+Park+MTB+Yo+Mama+Sunrise+Florida"},
  {name:"Darkside",             park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Expert",   dist:"0.5 mi",  feat:"Expert Only, Unpredictable",    desc:"Reserved for the most experienced riders. Unpredictable technical terrain with very limited bail-out options.",                                                                           q:"Markham+Park+MTB+Darkside+Sunrise+Florida"},
  {name:"Alligator Alley",      park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Expert",   dist:"0.3 mi",  feat:"Narrow, Expert",                desc:"An expert-rated trail with gruelling, unpredictable narrow singletrack through the most challenging terrain in the park. Very few riders make it through clean.",                         q:"Markham+Park+MTB+Alligator+Alley+Sunrise+Florida"},
  {name:"Jumpline",             park:"Markham Park",      loc:"Sunrise, FL",        cat:"markham",      diff:"Expert",   dist:"0.2 mi",  feat:"Jumps, Freeride, Air",          desc:"Markham's dedicated jump line and freeride trail. Progressive jumps and ramps for riders who want to practice aerial maneuvers and hone freestyle skills.",                             q:"Markham+Park+MTB+Jumpline+Sunrise+Florida"},

  // QUIET WATERS PARK
  {name:"Warm Up Trail",        park:"Quiet Waters Park", loc:"Deerfield Beach, FL",cat:"quietwaters",  diff:"Easy",     dist:"0.7 mi",  feat:"Flow, Beginner",                desc:"Green-rated singletrack at the entrance to the trail system. 3,596 ft long, rideable in both directions. The natural starting point for any Quiet Waters session.",                  q:"Quiet+Waters+Park+MTB+Trails+Deerfield+Beach+Florida"},
  {name:"Cool Down Trail",      park:"Quiet Waters Park", loc:"Deerfield Beach, FL",cat:"quietwaters",  diff:"Easy",     dist:"0.4 mi",  feat:"Flow, Exit",                    desc:"The natural ending to the full Quiet Waters loop. Helps riders wind down after the technical sections as part of the full lap.",                                                        q:"Quiet+Waters+Park+MTB+Trails+Deerfield+Beach+Florida"},
  {name:"Full MTB Loop",        park:"Quiet Waters Park", loc:"Deerfield Beach, FL",cat:"quietwaters",  diff:"Easy",     dist:"4.6 mi",  feat:"Coral Rock, Boardwalks",        desc:"The main loop connecting nearly two dozen singletrack trails with coral rock features, boardwalks, and optional advanced sections across 7+ total miles.",                             q:"Quiet+Waters+Park+MTB+Loop+Deerfield+Beach+Florida"},
  {name:"Corkscrew",            park:"Quiet Waters Park", loc:"Deerfield Beach, FL",cat:"quietwaters",  diff:"Moderate", dist:"0.9 mi",  feat:"Longest, Winding",              desc:"The longest individual trail at Quiet Waters at 4,751 ft. Most elevation gain and descent in the park (20 ft up, 17 ft down) — winding and technical.",                              q:"Quiet+Waters+Park+MTB+Corkscrew+Deerfield+Beach+Florida"},
  {name:"Anaconda",             park:"Quiet Waters Park", loc:"Deerfield Beach, FL",cat:"quietwaters",  diff:"Moderate", dist:"0.6 mi",  feat:"Top Rated, All Levels",         desc:"The highest-rated trail at Quiet Waters (4.1/5). Described as 'perfect for all riders' with numerous challenging features throughout.",                                               q:"Quiet+Waters+Park+MTB+Anaconda+Deerfield+Beach+Florida"},
  {name:"Horseshoe Extension",  park:"Quiet Waters Park", loc:"Deerfield Beach, FL",cat:"quietwaters",  diff:"Moderate", dist:"0.4 mi",  feat:"Steepest, Extension",           desc:"The steepest trail at Quiet Waters with a 1.1% average grade. An extension loop adding variety and challenge to the main network.",                                                  q:"Quiet+Waters+Park+MTB+Horseshoe+Deerfield+Beach+Florida"},
  {name:"Turnpike Extension",   park:"Quiet Waters Park", loc:"Deerfield Beach, FL",cat:"quietwaters",  diff:"Moderate", dist:"0.5 mi",  feat:"Boardwalks, Back Section",      desc:"Features notable boardwalk sections in the back of the park — a highlight for riders who love elevated wooden trail features.",                                                        q:"Quiet+Waters+Park+MTB+Turnpike+Deerfield+Beach+Florida"},
  {name:"Power Drop",           park:"Quiet Waters Park", loc:"Deerfield Beach, FL",cat:"quietwaters",  diff:"Hard",     dist:"0.3 mi",  feat:"Technical Drops",               desc:"Technical drops make this a standout feature in an otherwise mostly flat park. The best-rated trail for technical challenge at Quiet Waters.",                                         q:"Quiet+Waters+Park+MTB+Power+Drop+Deerfield+Beach+Florida"},

  // NORTH AMERICA
  {name:"Whistler Bike Park",   park:"Whistler, BC",      loc:"British Columbia",   cat:"northamerica", diff:"Expert",   dist:"70 mi+",  feat:"World Class, Lift Access",      desc:"The most famous lift-accessed bike park in the world. Whistler's 70+ miles of trails define downhill and enduro mountain biking globally.",                                           q:"Whistler+Bike+Park+MTB+British+Columbia"},
  {name:"Revelstoke Bike Park", park:"Revelstoke, BC",    loc:"British Columbia",   cat:"northamerica", diff:"Expert",   dist:"25 mi",   feat:"Enduro, Epic Vertical",         desc:"World-class enduro riding with massive vertical, technical old-growth forest trails. Legendary routes attract riders from around the globe.",                                        q:"Revelstoke+Mountain+Resort+Bike+Park+British+Columbia"},
  {name:"Whole Enchilada",      park:"Moab, Utah",        loc:"Utah",               cat:"northamerica", diff:"Hard",     dist:"26 mi",   feat:"7,000 ft Descent, Epic",        desc:"One of the most iconic MTB descents in the world. 7,000 ft from alpine aspen forests to slickrock canyon. A true bucket-list ride.",                                               q:"Whole+Enchilada+MTB+Trail+Moab+Utah"},
  {name:"Slickrock Trail",      park:"Moab, Utah",        loc:"Utah",               cat:"northamerica", diff:"Hard",     dist:"12 mi",   feat:"Slickrock, Technical",          desc:"The most famous trail in Moab. Undulating cryptobiotic sandstone with massive exposure. An MTB rite of passage.",                                                                      q:"Slickrock+MTB+Trail+Moab+Utah"},
  {name:"Porcupine Rim",        park:"Moab, Utah",        loc:"Utah",               cat:"northamerica", diff:"Hard",     dist:"17 mi",   feat:"Rim Views, 2000ft Descent",     desc:"Stunning rim trail with 2,000+ ft of descent into Castle Valley. Exposed singletrack with Colorado River views and technical rocky sections.",                                       q:"Porcupine+Rim+MTB+Trail+Moab+Utah"},
  {name:"Downieville Downhill", park:"Downieville, CA",   loc:"California",         cat:"northamerica", diff:"Hard",     dist:"17 mi",   feat:"Enduro, Shuttle",               desc:"The crown jewel of Sierra Nevada riding. A shuttle-accessed descent from 6,700 ft through old growth forest to the Downieville town center.",                                      q:"Downieville+Downhill+MTB+Trail+California"},
  {name:"Alafia River SP",      park:"Alafia River SP",   loc:"Lithia, Florida",    cat:"northamerica", diff:"Hard",     dist:"20 mi",   feat:"Florida Technical, Drops",      desc:"The most technical trail system in Florida with man-made features, drops, and demanding singletrack. Florida's hardest MTB destination.",                                            q:"Alafia+River+State+Park+MTB+Trails+Lithia+Florida"},
  {name:"Phil's World",         park:"Cortez, Colorado",  loc:"Colorado",           cat:"northamerica", diff:"Moderate", dist:"15 mi",   feat:"Flowy, Perfect Berms",          desc:"Widely regarded as one of the best flowy trail systems in Colorado. Perfect berms, rollers, and singletrack.",                                                                        q:"Phils+World+MTB+Trail+Cortez+Colorado"},
  {name:"18 Road Trails",       park:"Fruita, Colorado",  loc:"Colorado",           cat:"northamerica", diff:"Moderate", dist:"30 mi+",  feat:"Desert, All Levels",            desc:"World-class desert singletrack near Fruita with flowing trails for every skill level. Prime riding from October through April.",                                                     q:"18+Road+MTB+Trails+Fruita+Colorado"},
  {name:"Kingdom Trails",       park:"East Burke, VT",    loc:"Vermont",            cat:"northamerica", diff:"Moderate", dist:"100 mi+", feat:"Northeast Classic, Foliage",    desc:"New England's most celebrated trail network with 100+ miles of singletrack through Vermont's Northeast Kingdom.",                                                                    q:"Kingdom+Trails+MTB+East+Burke+Vermont"},
  {name:"Galbraith Mountain",   park:"Bellingham, WA",    loc:"Washington",         cat:"northamerica", diff:"Moderate", dist:"60 mi+",  feat:"Pacific NW, Year-Round",        desc:"Over 60 miles of Pacific Northwest singletrack with technical root and rock features. Rideable year-round.",                                                                           q:"Galbraith+Mountain+MTB+Bellingham+Washington"},
  {name:"Bentonville Trails",   park:"Bentonville, AR",   loc:"Arkansas",           cat:"northamerica", diff:"Moderate", dist:"400 mi+", feat:"Best in US, Ozarks",            desc:"The Ozark MTB scene centered in Bentonville has exploded into one of America's top trail destinations with 400+ miles of purpose-built singletrack.",                                q:"Bentonville+MTB+Trails+Arkansas+Slaughter+Pen"},
  {name:"Santos Trails",        park:"Ocala, FL",         loc:"Florida",            cat:"northamerica", diff:"Easy",     dist:"80 mi+",  feat:"Florida's Best, Flow",          desc:"Florida's crown jewel of mountain biking. 80+ miles of fast, flowing singletrack through the Ocala National Forest. The best MTB destination in the southeast.",                    q:"Santos+MTB+Trails+Ocala+Florida"},
  {name:"Mammoth Bike Park",    park:"Mammoth Lakes, CA", loc:"California",         cat:"northamerica", diff:"Moderate", dist:"80 mi+",  feat:"Lift Access, All Levels",       desc:"World-class lift-accessed bike park in the Eastern Sierra with 80+ miles of trails from beginner-friendly to expert downhill.",                                                    q:"Mammoth+Mountain+Bike+Park+California"},
  {name:"Sun Valley Trails",    park:"Sun Valley, ID",    loc:"Idaho",              cat:"northamerica", diff:"Moderate", dist:"200 mi+", feat:"Alpine, Epic Views",            desc:"Sun Valley's massive trail network spans 200+ miles through the Sawtooth Range. World-class alpine singletrack with breathtaking scenery.",                                         q:"Sun+Valley+MTB+Trails+Idaho"},
  {name:"Orogenesis",           park:"Canada Border → Cabo San Lucas", loc:"WA · OR · CA · Baja Mexico", cat:"northamerica", diff:"Expert",   dist:"5,000 mi", feat:"World's Longest MTB Route, Bikepacking, Backcountry", desc:"The world's longest mountain bike trail — 5,000 miles of singletrack, gravel roads, and backcountry riding from the US/Canada border in Washington, through Oregon and California, connecting to the Baja Divide all the way to Cabo San Lucas, Mexico. Created by the Orogenesis Collective (founded by Gabriel Amadeus Tiller) and first fully completed in December 2025 by ultra-endurance rider Kurt Refsnider after 5 months on the trail. Connects the Cross-Washington Mountain Bike Route, Oregon Timber Trail, and Baja Divide into one epic spine. About 95% complete with ~200 miles of gaps still being built. The bikepacking equivalent of the Pacific Crest Trail.", q:"Orogenesis+MTB+trail+Canada+Baja+California+bikepacking"},
  {name:"Great Divide MTB Route",park:"Jasper, AB to Antelope Wells, NM",loc:"Canada to New Mexico",cat:"northamerica",diff:"Expert",dist:"3,084 mi",feat:"Bikepacking Classic, Continental Divide, 200k ft Climbing",desc:"The birthplace of bikepacking and the most iconic off-road route in North America. 3,084 miles tracing the Continental Divide from Jasper, Alberta to the US-Mexico border, 70% unpaved with over 200,000 feet of elevation through Montana, Idaho, Wyoming, Colorado, and New Mexico. Windswept plateaus, alpine passes, and remote frontier towns.",q:"Great+Divide+Mountain+Bike+Route+GDMBR+bikepacking"},
  {name:"Colorado Trail",park:"Denver to Durango",loc:"Colorado",cat:"northamerica",diff:"Expert",dist:"539 mi",feat:"Triple Crown, Alpine Singletrack, 10k ft Avg Elevation",desc:"539 miles of high-altitude singletrack through the Colorado Rockies. Average elevation of 10,000 feet with 66,000+ feet of total climbing. One of the three routes in the Bikepacking Triple Crown alongside the Great Divide and Arizona Trail. Steep technical climbs, stunning alpine meadows, and a narrow summer weather window.",q:"Colorado+Trail+MTB+bikepacking+Denver+Durango"},
  {name:"Arizona Trail",park:"US-Mexico Border to Utah",loc:"Arizona",cat:"northamerica",diff:"Expert",dist:"739 mi",feat:"Triple Crown, Grand Canyon Crossing, Desert and Pine Forest",desc:"739 miles through Arizona from the Mexican border to Utah — cactus deserts, pine forests, and the Grand Canyon where riders must carry their bikes across. One of the three legs of the Bikepacking Triple Crown. 65,000+ feet of elevation gain through some of the Southwest's most dramatic landscapes.",q:"Arizona+Trail+MTB+bikepacking+Grand+Canyon"},
  {name:"Oregon Timber Trail",park:"Lakeview to Columbia River Gorge",loc:"Oregon",cat:"northamerica",diff:"Expert",dist:"668 mi",feat:"Singletrack-Rich, Old-Growth Forest, Technically Demanding",desc:"668 miles bisecting Oregon from the California border to the Columbia River Gorge. Over half the miles on singletrack through old-growth forests, ridgelines, and farmland — one of the most technically challenging long-distance routes in the US. The northern anchor of the Orogenesis megaRoute.",q:"Oregon+Timber+Trail+MTB+bikepacking"},
  {name:"Baja Divide",park:"San Diego to Cabo San Lucas",loc:"California to Baja Mexico",cat:"northamerica",diff:"Expert",dist:"1,700 mi",feat:"Desert Wilderness, Remote, Backcountry Mexico",desc:"1,700 miles of remote desert bikepacking from San Diego to the southern tip of Baja California. Crosses desert mountains, dry river beds, and isolated coastline with minimal services and maximum solitude. The southern half of the Orogenesis route. Best ridden October through April.",q:"Baja+Divide+MTB+bikepacking+Baja+California+Mexico"},
  {name:"Maah Daah Hey Trail",park:"Theodore Roosevelt NP",loc:"North Dakota",cat:"northamerica",diff:"Hard",dist:"144 mi",feat:"Badlands Singletrack, Wildlife, Buttes",desc:"144 miles of mostly singletrack through the otherworldly North Dakota Badlands between the north and south units of Theodore Roosevelt National Park. Steep creek drainages, clay trail that destroys drivetrains in wet weather, and sweeping grassland views shared with elk, pronghorn, and bison.",q:"Maah+Daah+Hey+Trail+MTB+North+Dakota+Badlands"},
  {name:"Coconino Loop",park:"Flagstaff and Sedona",loc:"Arizona",cat:"northamerica",diff:"Expert",dist:"240 mi",feat:"Slickrock, Singletrack, 28k ft Climbing, Stage Race Route",desc:"240 miles of singletrack and dirt roads through the canyons and peaks of Northern Arizona. Half the route is Arizona finest singletrack — fast flowy descents into Flagstaff and grippy Sedona slickrock. 28,000 feet of climbing. Hosts a brutal stage race as part of the Arizona Endurance Series. Best tackled over a full week.",q:"Coconino+Loop+MTB+bikepacking+Flagstaff+Sedona+Arizona"},
  {name:"Trans-Virginia Route",park:"Front Royal to Damascus",loc:"Virginia",cat:"northamerica",diff:"Hard",dist:"473 mi",feat:"Appalachian Singletrack, Rugged East Coast, Waterfalls",desc:"473 miles through Virginia Appalachian Mountains from Front Royal to Damascus. Overgrown sections, brutally rugged terrain, and long hike-a-bike stretches make this one of the toughest east coast bikepacking routes. Stunning old-growth forests, waterfalls, and rumored secret hot springs along the way.",q:"Trans+Virginia+MTB+bikepacking+Appalachian"},
  {name:"Cross-Washington Route",park:"La Push to Tekoa",loc:"Washington",cat:"northamerica",diff:"Expert",dist:"700 mi",feat:"Coast to Desert, Alpine Passes, Rainforest to Scablands",desc:"700 miles from the Pacific rainforest at La Push to the wheat fields of Tekoa near the Idaho border. Traverses misty old-growth rainforest, snowy Cascade passes, volcanic scablands, and rolling farmland. The northern anchor of the Orogenesis megaRoute. Hosts an annual grand depart race.",q:"Cross+Washington+Mountain+Bike+Route+XWA+bikepacking"},
  {name:"Trans North Georgia",park:"Tennessee Border to Alabama",loc:"Georgia",cat:"northamerica",diff:"Expert",dist:"350 mi",feat:"Southern Appalachians, Remote, Waterfalls, Gravel",desc:"A gorgeous route stitching together roads and trails through the southern Appalachian mountains of Georgia. Dense deciduous canopies, waterfalls, and remote backcountry terrain. One of four parts of the Southern Highlands Traverse spanning Virginia to Alabama — a must-ride for east coast riders.",q:"Trans+North+Georgia+TNGA+MTB+bikepacking+Appalachian"},
  {name:"Idaho Hot Springs MTB Route",park:"Boise to Sun Valley",loc:"Idaho",cat:"northamerica",diff:"Hard",dist:"500 mi",feat:"Natural Hot Springs, Alpine Wilderness, Remote Backcountry",desc:"500 miles through Idaho rugged wilderness combining serious mountain riding with the unique reward of natural hot springs along the route. Remote backcountry terrain with dramatic alpine views and geothermal pools to soak your tired legs at the end of each day.",q:"Idaho+Hot+Springs+Mountain+Bike+Route+bikepacking"},
];

/* ═════════ FILTER STATE ═════════ */
let activeFilters = {cat:'all', diff:'all'};
let currentList = [];

function setFilter(group, val, btn) {
  activeFilters[group] = val;
  document.querySelectorAll(`[data-filter="${group}"]`).forEach(b => {
    b.className = 'filter-btn';
    if (b.dataset.val === val) {
      if (group==='cat'&&val==='markham')      b.classList.add('active-markham');
      else if (group==='cat'&&val==='quietwaters') b.classList.add('active-quietwaters');
      else if (group==='cat'&&val==='northamerica') b.classList.add('active-northamerica');
      else b.classList.add('active');
    }
  });
  filterTrails();
}

function filterTrails() {
  const q = document.getElementById('trailSearch').value.toLowerCase();
  const {cat,diff} = activeFilters;
  currentList = TRAILS.filter(t => {
    const mCat  = cat  === 'all' || t.cat  === cat;
    const mDiff = diff === 'all' || t.diff === diff;
    const mQ    = !q   || t.name.toLowerCase().includes(q)||t.park.toLowerCase().includes(q)||t.loc.toLowerCase().includes(q)||t.desc.toLowerCase().includes(q);
    return mCat && mDiff && mQ;
  });
  renderTrails(currentList);
}

const DC = {
  Easy:     {dot:'green', bar:'diff-green'},
  Moderate: {dot:'blue',  bar:'diff-blue'},
  Hard:     {dot:'red',   bar:'diff-red'},
  Expert:   {dot:'black', bar:'diff-black'},
};
const CL = {markham:'Markham Park', quietwaters:'Quiet Waters', northamerica:'North America'};

function renderTrails(list) {
  document.getElementById('trailCountNum').textContent = list.length;
  const g = document.getElementById('trailsGrid');
  if (!list.length) { g.innerHTML = '<div class="no-results">No trails match your filters</div>'; return; }
  g.innerHTML = list.map((t,i) => {
    const d = DC[t.diff]||DC.Moderate;
    return `<div class="trail-card ${d.bar} cat-${t.cat}" onclick="openModal(${i})">
      <div class="trail-badges">
        <span class="trail-diff-label"><span class="diff-dot ${d.dot}"></span>${t.diff}</span>
        <span class="cat-badge ${t.cat}">${CL[t.cat]}</span>
      </div>
      <div class="trail-name">${t.name}</div>
      <div class="trail-park">${t.park} · ${t.loc}</div>
      <div class="trail-stat-row">
        <div class="stat"><div class="stat-val">${t.dist}</div><div class="stat-key">Distance</div></div>
        <div class="stat"><div class="stat-val" style="font-size:0.82rem;color:var(--cream);letter-spacing:0">${t.feat.split(',')[0].trim()}</div><div class="stat-key">Feature</div></div>
      </div>
      <div class="trail-map-hint">🗺 View on map</div>
    </div>`;
  }).join('');
}

function openModal(idx) {
  const t = currentList[idx]; if (!t) return;
  const d = DC[t.diff]||DC.Moderate;
  document.getElementById('mTitle').textContent   = t.name;
  document.getElementById('mSub').textContent     = `${t.park} · ${t.loc}`;
  document.getElementById('mBadges').innerHTML    = `<span class="trail-diff-label"><span class="diff-dot ${d.dot}"></span>${t.diff}</span><span class="cat-badge ${t.cat}">${CL[t.cat]}</span>`;
  document.getElementById('mStats').innerHTML     = `<div class="stat"><div class="stat-val">${t.dist}</div><div class="stat-key">Distance</div></div><div class="stat"><div class="stat-val">${t.diff}</div><div class="stat-key">Difficulty</div></div><div class="stat"><div class="stat-val" style="font-size:0.9rem;color:var(--cream)">${t.feat}</div><div class="stat-key">Features</div></div>`;
  document.getElementById('mDesc').textContent   = t.desc;
  document.getElementById('mMapFrame').src       = `https://maps.google.com/maps?q=${t.q}&output=embed&z=15`;
  document.getElementById('mapModal').classList.add('open');
  document.body.style.overflow = 'hidden';
}
function closeModal() {
  document.getElementById('mapModal').classList.remove('open');
  document.body.style.overflow = '';
  setTimeout(()=>{ document.getElementById('mMapFrame').src=''; },300);
}
function outsideClose(e) { if (e.target.id==='mapModal') closeModal(); }
document.addEventListener('keydown', e => { if(e.key==='Escape') closeModal(); });

filterTrails();


/* ═══════════════════════════════════════════
   GAME ENGINE — Focus-based, no global conflicts
   Each game only responds to keys when its
   canvas is "active" (clicked).
═══════════════════════════════════════════ */
let activeGame = null; // 'tetris' | 'pac' | 'serpent'

/* Click any canvas to activate that game */
['tetrisCanvas','pacCanvas','serpentCanvas'].forEach(id=>{
  const el = document.getElementById(id);
  if(el) el.addEventListener('click', ()=>{ activeGame = id.replace('Canvas',''); });
});

/* Single global key handler — routes to active game */
document.addEventListener('keydown', e => {
  const tag = document.activeElement && document.activeElement.tagName;
  if(tag==='INPUT'||tag==='TEXTAREA') return;
  if(activeGame==='tetris')  tetrisKey(e);
  else if(activeGame==='pac') pacKey(e);
  else if(activeGame==='serpent') serpentKey(e);
  // If no game is focused, space starts all idle games
  if(!activeGame && e.code==='Space') {
    e.preventDefault();
    tetrisKey(e); pacKey(e); serpentKey(e);
  }
});

/* ═════════ TETRIS ═════════ */
const TETRIS = (function(){
  const cv  = document.getElementById('tetrisCanvas');
  const ctx = cv.getContext('2d');
  const nv  = document.getElementById('tetNext');
  const nctx= nv.getContext('2d');
  const BS=24, COLS=10, ROWS=20;
  const W=cv.width, H=cv.height;
  const scoreEl=document.getElementById('tetScore');
  const levelEl=document.getElementById('tetLevel');
  const linesEl=document.getElementById('tetLines');

  const SHAPES = [
    {s:[[1,1,1,1]],           c:'#00d4bb'}, // I
    {s:[[1,1],[1,1]],          c:'#e8c97a'}, // O
    {s:[[0,1,0],[1,1,1]],     c:'#c040e0'}, // T
    {s:[[1,0,0],[1,1,1]],     c:'#ff6b4a'}, // J
    {s:[[0,0,1],[1,1,1]],     c:'#46a0f0'}, // L
    {s:[[0,1,1],[1,1,0]],     c:'#2dd28c'}, // S
    {s:[[1,1,0],[0,1,1]],     c:'#ff4466'}, // Z
  ];

  let board, cur, nxt, sc, li, lv, running, paused, raf, lastDrop, dropSpeed;

  function newBoard(){ return Array.from({length:ROWS},()=>Array(COLS).fill(0)); }

  function newPiece(){
    const t = SHAPES[Math.floor(Math.random()*SHAPES.length)];
    return { s: t.s.map(r=>[...r]), c: t.c,
             x: Math.floor(COLS/2) - Math.floor(t.s[0].length/2), y: 0 };
  }

  function fits(p, dx, dy, shape){
    const s = shape||p.s;
    return s.every((row,ry)=>row.every((cell,cx)=>{
      if(!cell) return true;
      const nx=p.x+cx+(dx||0), ny=p.y+ry+(dy||0);
      return nx>=0 && nx<COLS && ny<ROWS && (ny<0 || !board[ny][nx]);
    }));
  }

  function lock(){
    cur.s.forEach((row,ry)=>row.forEach((cell,cx)=>{
      if(cell && cur.y+ry>=0) board[cur.y+ry][cur.x+cx]=cur.c;
    }));
    sweep();
    cur = nxt;
    nxt = newPiece();
    if(!fits(cur,0,0)){ endGame(); return; }
  }

  function sweep(){
    let cleared=0;
    for(let r=ROWS-1;r>=0;r--){
      if(board[r].every(c=>c)){
        board.splice(r,1);
        board.unshift(Array(COLS).fill(0));
        cleared++; r++;
      }
    }
    if(cleared){
      li+=cleared;
      sc+=[0,100,300,500,800][Math.min(cleared,4)]*lv;
      lv=Math.floor(li/10)+1;
      dropSpeed=Math.max(80,500-lv*42);
      scoreEl.textContent=sc;
      levelEl.textContent=lv;
      linesEl.textContent=li;
    }
  }

  function rotate(){
    const rot = cur.s[0].map((_,i)=>cur.s.map(r=>r[i]).reverse());
    // wall kicks
    for(const kick of [0,-1,1,-2,2]){
      if(fits(cur,kick,0,rot)){ cur.x+=kick; cur.s=rot; return; }
    }
  }

  function endGame(){
    running=false;
    ctx.fillStyle='rgba(5,13,20,0.88)'; ctx.fillRect(0,0,W,H);
    ctx.textAlign='center';
    ctx.font="bold 30px 'Bebas Neue',sans-serif";
    ctx.fillStyle='#ff6b4a'; ctx.fillText('GAME OVER',W/2,H/2-18);
    ctx.font="13px 'Barlow Condensed',sans-serif";
    ctx.fillStyle='rgba(240,236,224,0.55)';
    ctx.fillText('Click here + SPACE to restart',W/2,H/2+8);
    ctx.textAlign='left';
  }

  function drawBoard(){
    ctx.fillStyle='#050d14'; ctx.fillRect(0,0,W,H);
    // grid
    ctx.strokeStyle='rgba(0,180,160,0.05)'; ctx.lineWidth=0.5;
    for(let x=0;x<=COLS;x++){ctx.beginPath();ctx.moveTo(x*BS,0);ctx.lineTo(x*BS,H);ctx.stroke();}
    for(let y=0;y<=ROWS;y++){ctx.beginPath();ctx.moveTo(0,y*BS);ctx.lineTo(W,y*BS);ctx.stroke();}
    // placed blocks
    board.forEach((row,ry)=>row.forEach((c,cx)=>{
      if(c){ drawBlock(ctx,cx,ry,c); }
    }));
  }

  function drawBlock(c,cx,ry,color){
    c.fillStyle=color;
    c.fillRect(cx*BS+1,ry*BS+1,BS-2,BS-2);
    c.fillStyle='rgba(255,255,255,0.18)';
    c.fillRect(cx*BS+2,ry*BS+2,BS-4,4);
  }

  function drawCurrent(){
    if(!cur) return;
    // ghost
    let g={...cur,s:cur.s.map(r=>[...r])};
    while(fits(g,0,1)) g.y++;
    g.s.forEach((row,ry)=>row.forEach((cell,cx)=>{
      if(cell){ ctx.fillStyle='rgba(255,255,255,0.07)';
        ctx.fillRect((g.x+cx)*BS+1,(g.y+ry)*BS+1,BS-2,BS-2); }
    }));
    cur.s.forEach((row,ry)=>row.forEach((cell,cx)=>{
      if(cell) drawBlock(ctx,cur.x+cx,cur.y+ry,cur.c);
    }));
  }

  function drawNext(){
    nctx.fillStyle='#050d14'; nctx.fillRect(0,0,80,80);
    if(!nxt) return;
    const ox=Math.floor((4-nxt.s[0].length)/2);
    const oy=Math.floor((4-nxt.s.length)/2);
    nxt.s.forEach((row,ry)=>row.forEach((cell,cx)=>{
      if(cell){ nctx.fillStyle=nxt.c;
        nctx.fillRect((ox+cx)*19+2,(oy+ry)*19+2,17,17);
        nctx.fillStyle='rgba(255,255,255,0.18)';
        nctx.fillRect((ox+cx)*19+3,(oy+ry)*19+3,15,3);
      }
    }));
  }

  function render(ts){
    if(!running){ drawBoard(); drawCurrent(); drawNext(); return; }
    if(paused){
      ctx.fillStyle='rgba(5,13,20,0.7)'; ctx.fillRect(0,0,W,H);
      ctx.textAlign='center';
      ctx.font="bold 32px 'Bebas Neue',sans-serif";
      ctx.fillStyle='#e8c97a'; ctx.fillText('PAUSED',W/2,H/2);
      ctx.font="13px 'Barlow Condensed',sans-serif";
      ctx.fillStyle='rgba(240,236,224,0.4)';
      ctx.fillText('P to resume',W/2,H/2+22);
      ctx.textAlign='left';
      raf=requestAnimationFrame(render); return;
    }
    if(!lastDrop) lastDrop=ts;
    if(ts-lastDrop>dropSpeed){
      lastDrop=ts;
      if(fits(cur,0,1)) cur.y++;
      else lock();
    }
    drawBoard(); drawCurrent(); drawNext();
    raf=requestAnimationFrame(render);
  }

  function start(){
    board=newBoard(); sc=0; li=0; lv=1;
    dropSpeed=460; running=true; paused=false; lastDrop=0;
    cur=newPiece(); nxt=newPiece();
    scoreEl.textContent=0; levelEl.textContent=1; linesEl.textContent=0;
    cancelAnimationFrame(raf);
    raf=requestAnimationFrame(render);
    activeGame='tetris';
  }

  // Idle splash
  function splash(){
    ctx.fillStyle='#050d14'; ctx.fillRect(0,0,W,H);
    ctx.fillStyle='rgba(0,180,160,0.07)'; ctx.fillRect(0,0,W,H);
    ctx.textAlign='center';
    ctx.font="bold 28px 'Bebas Neue',sans-serif";
    ctx.fillStyle='#00b4a0'; ctx.fillText('RIDGE TETRIS',W/2,H/2-18);
    ctx.font="13px 'Barlow Condensed',sans-serif";
    ctx.fillStyle='rgba(240,236,224,0.45)';
    ctx.fillText('Click here, then SPACE to begin',W/2,H/2+8);
    ctx.textAlign='left';
    nctx.fillStyle='#050d14'; nctx.fillRect(0,0,80,80);
  }

  splash();
  cv.addEventListener('click',()=>{ activeGame='tetris'; if(!running) start(); });

  return {
    key(e){
      if(!running && (e.code==='Space'||e.key==='Enter')){ e.preventDefault(); start(); return; }
      if(!running) return;
      if(e.key==='p'||e.key==='P'){ paused=!paused; if(!paused){lastDrop=0;raf=requestAnimationFrame(render);} return; }
      if(paused) return;
      e.preventDefault();
      if(e.key==='ArrowLeft'  && fits(cur,-1,0)) { cur.x--; }
      if(e.key==='ArrowRight' && fits(cur, 1,0)) { cur.x++; }
      if(e.key==='ArrowDown') { if(fits(cur,0,1)) cur.y++; else lock(); }
      if(e.key==='ArrowUp')   { rotate(); }
      if(e.code==='Space')    { while(fits(cur,0,1)) cur.y++; lock(); lastDrop=0; }
      drawBoard(); drawCurrent(); drawNext();
    },
    start
  };
})();
function tetrisKey(e){ TETRIS.key(e); }

/* ═════════ PAC-MAN ═════════ */
const PACMAN = (function(){
  const cv  = document.getElementById('pacCanvas');
  const ctx = cv.getContext('2d');
  const scoreEl=document.getElementById('pacScore');
  const livesEl=document.getElementById('pacLives');

  const T=16; // tile size
  const COLS=28, ROWS=31;
  const CW=COLS*T, CH=ROWS*T;

  // 0=wall 1=dot 2=power 3=empty 4=ghost-house-door
  const BASE_MAP = [
    [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
    [0,1,1,1,1,1,1,1,1,1,1,1,1,0,0,1,1,1,1,1,1,1,1,1,1,1,1,0],
    [0,1,0,0,0,0,1,0,0,0,0,0,1,0,0,1,0,0,0,0,0,1,0,0,0,0,1,0],
    [0,2,0,0,0,0,1,0,0,0,0,0,1,0,0,1,0,0,0,0,0,1,0,0,0,0,2,0],
    [0,1,0,0,0,0,1,0,0,0,0,0,1,0,0,1,0,0,0,0,0,1,0,0,0,0,1,0],
    [0,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,0],
    [0,1,0,0,0,0,1,0,0,1,0,0,0,0,0,0,0,0,1,0,0,1,0,0,0,0,1,0],
    [0,1,0,0,0,0,1,0,0,1,0,0,0,0,0,0,0,0,1,0,0,1,0,0,0,0,1,0],
    [0,1,1,1,1,1,1,0,0,1,1,1,1,0,0,1,1,1,1,0,0,1,1,1,1,1,1,0],
    [0,0,0,0,0,0,1,0,0,0,0,0,3,0,0,3,0,0,0,0,0,1,0,0,0,0,0,0],
    [0,0,0,0,0,0,1,0,0,0,0,0,3,0,0,3,0,0,0,0,0,1,0,0,0,0,0,0],
    [0,0,0,0,0,0,1,0,0,3,3,3,3,3,3,3,3,3,3,0,0,1,0,0,0,0,0,0],
    [0,0,0,0,0,0,1,0,0,3,0,0,0,4,4,0,0,0,3,0,0,1,0,0,0,0,0,0],
    [1,1,1,1,1,1,1,0,0,3,0,3,3,3,3,3,3,0,3,0,0,1,1,1,1,1,1,1],
    [3,3,3,3,3,3,3,3,3,3,0,3,3,3,3,3,3,0,3,3,3,3,3,3,3,3,3,3],
    [1,1,1,1,1,1,1,0,0,3,0,3,3,3,3,3,3,0,3,0,0,1,1,1,1,1,1,1],
    [0,0,0,0,0,0,1,0,0,3,3,3,3,3,3,3,3,3,3,0,0,1,0,0,0,0,0,0],
    [0,0,0,0,0,0,1,0,0,3,0,0,0,0,0,0,0,0,3,0,0,1,0,0,0,0,0,0],
    [0,0,0,0,0,0,1,0,0,3,0,0,0,0,0,0,0,0,3,0,0,1,0,0,0,0,0,0],
    [0,1,1,1,1,1,1,1,1,1,1,1,1,0,0,1,1,1,1,1,1,1,1,1,1,1,1,0],
    [0,1,0,0,0,0,1,0,0,0,0,0,1,0,0,1,0,0,0,0,0,1,0,0,0,0,1,0],
    [0,1,0,0,0,0,1,0,0,0,0,0,1,0,0,1,0,0,0,0,0,1,0,0,0,0,1,0],
    [0,2,1,1,0,0,1,1,1,1,1,1,1,3,3,1,1,1,1,1,1,1,0,0,1,1,2,0],
    [0,0,0,1,0,0,1,0,0,1,0,0,0,0,0,0,0,0,1,0,0,1,0,0,1,0,0,0],
    [0,0,0,1,0,0,1,0,0,1,0,0,0,0,0,0,0,0,1,0,0,1,0,0,1,0,0,0],
    [0,1,1,1,1,1,1,0,0,1,1,1,1,0,0,1,1,1,1,0,0,1,1,1,1,1,1,0],
    [0,1,0,0,0,0,0,0,0,0,0,0,1,0,0,1,0,0,0,0,0,0,0,0,0,0,1,0],
    [0,1,0,0,0,0,0,0,0,0,0,0,1,0,0,1,0,0,0,0,0,0,0,0,0,0,1,0],
    [0,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,0],
    [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
    [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
  ];

  const GC = ['#ff4466','#ffb8ff','#00d4ff','#ffb852'];
  let map, pac, ghosts, score, lives, running, raf, frighTimer;

  function isWall(tx,ty){
    if(ty<0||ty>=ROWS) return true;
    if(tx<0||tx>=COLS) return false; // tunnel
    return map[ty][tx]===0;
  }

  function resetMap(){ map = BASE_MAP.map(r=>[...r]); }

  function resetPac(){
    pac={
      px:14*T, py:23*T,   // pixel pos (centre)
      dx:0, dy:0,          // current direction
      nx:0, ny:0,          // next direction
      speed:1.5,
      mouth:0.05, mdir:1
    };
  }

  function resetGhosts(){
    ghosts=[
      {px:13*T,py:11*T,dx: 1,dy:0,c:GC[0],fright:false,speed:1},
      {px:11*T,py:14*T,dx:-1,dy:0,c:GC[1],fright:false,speed:0.8},
      {px:14*T,py:14*T,dx: 1,dy:0,c:GC[2],fright:false,speed:0.8},
      {px:16*T,py:14*T,dx: 0,dy:1,c:GC[3],fright:false,speed:0.8},
    ];
  }

  function startGame(){
    resetMap(); resetPac(); resetGhosts();
    score=0; lives=3; running=true; frighTimer=0;
    scoreEl.textContent=0; livesEl.textContent=3;
    cancelAnimationFrame(raf);
    raf=requestAnimationFrame(gameLoop);
    activeGame='pac';
  }

  function tileOf(px){ return Math.floor(px/T); }

  function movePac(){
    const tx=tileOf(pac.px), ty=tileOf(pac.py);
    const cx=pac.px - tx*T, cy=pac.py - ty*T;
    const SNAP=3;
    // try to apply next dir when aligned enough
    const aligned = cx<=SNAP && cy<=SNAP;
    const alignedX = cy<=SNAP; // can turn left/right
    const alignedY = cx<=SNAP; // can turn up/down

    if((pac.nx!==0) && alignedX && !isWall(tx+pac.nx, ty)){
      // snap to grid
      pac.py = ty*T; pac.dx=pac.nx; pac.dy=0; pac.nx=0; pac.ny=0;
    } else if((pac.ny!==0) && alignedY && !isWall(tx, ty+pac.ny)){
      pac.px = tx*T; pac.dy=pac.ny; pac.dx=0; pac.nx=0; pac.ny=0;
    }

    const ntx=tileOf(pac.px+pac.dx*pac.speed);
    const nty=tileOf(pac.py+pac.dy*pac.speed);
    // wall check
    if(pac.dx!==0 && isWall(ntx+(pac.dx>0?0:0), ty)) { pac.dx=0; pac.px=tx*T; }
    if(pac.dy!==0 && isWall(tx, nty+(pac.dy>0?0:0))) { pac.dy=0; pac.py=ty*T; }

    pac.px+=pac.dx*pac.speed;
    pac.py+=pac.dy*pac.speed;

    // tunnel wrap
    if(pac.px < -T) pac.px = CW;
    if(pac.px > CW) pac.px = -T;

    pac.mouth+=0.04*pac.mdir;
    if(pac.mouth>0.22||pac.mouth<0.02) pac.mdir*=-1;

    // eat dots
    const etx=Math.round(pac.px/T), ety=Math.round(pac.py/T);
    if(ety>=0&&ety<ROWS&&etx>=0&&etx<COLS){
      if(map[ety][etx]===1){ map[ety][etx]=3; score+=10; scoreEl.textContent=score; }
      if(map[ety][etx]===2){ map[ety][etx]=3; score+=50; scoreEl.textContent=score;
        frighTimer=420;
        ghosts.forEach(g=>{ g.fright=true; g.dx=-g.dx; g.dy=-g.dy; });
      }
    }
  }

  function moveGhost(g){
    if(frighTimer>0) g.fright=true; else g.fright=false;
    const spd = g.fright ? 0.8 : g.speed*1.4;
    const tx=Math.round(g.px/T), ty=Math.round(g.py/T);
    // at tile boundary, pick new direction
    if(Math.abs(g.px-tx*T)<spd+0.5 && Math.abs(g.py-ty*T)<spd+0.5){
      g.px=tx*T; g.py=ty*T;
      const dirs=[{dx:1,dy:0},{dx:-1,dy:0},{dx:0,dy:1},{dx:0,dy:-1}];
      const opts=dirs.filter(d=>
        !(d.dx===-g.dx&&d.dy===-g.dy) && !isWall(tx+d.dx,ty+d.dy)
      );
      if(opts.length>0){
        const chosen=opts[Math.floor(Math.random()*opts.length)];
        g.dx=chosen.dx; g.dy=chosen.dy;
      }
    }
    g.px+=g.dx*spd; g.py+=g.dy*spd;
    if(g.px<-T) g.px=CW; if(g.px>CW) g.px=-T;
  }

  function checkHits(){
    ghosts.forEach(g=>{
      if(Math.hypot(g.px-pac.px, g.py-pac.py)<T*0.85){
        if(g.fright){
          score+=200; scoreEl.textContent=score;
          g.fright=false; g.px=14*T; g.py=14*T; g.dx=0; g.dy=-1;
        } else {
          lives--; livesEl.textContent=lives;
          if(lives<=0){ running=false; }
          else { resetPac(); }
        }
      }
    });
  }

  function drawScene(){
    ctx.fillStyle='#050d14'; ctx.fillRect(0,0,CW,CH);
    // walls
    map.forEach((row,ry)=>row.forEach((cell,cx)=>{
      if(cell===0){
        ctx.fillStyle='#1a3a7a';
        ctx.fillRect(cx*T,ry*T,T,T);
        ctx.strokeStyle='#0d2255';
        ctx.lineWidth=1;
        ctx.strokeRect(cx*T+0.5,ry*T+0.5,T-1,T-1);
      }
      if(cell===4){
        ctx.fillStyle='rgba(255,180,80,0.3)';
        ctx.fillRect(cx*T+2,ry*T+6,T-4,4);
      }
    }));
    // dots & power pellets
    map.forEach((row,ry)=>row.forEach((cell,cx)=>{
      const px=cx*T+T/2, py=ry*T+T/2;
      if(cell===1){ ctx.fillStyle='rgba(240,236,224,0.75)'; ctx.beginPath(); ctx.arc(px,py,2,0,Math.PI*2); ctx.fill(); }
      if(cell===2){
        const pulse = 0.65+0.35*Math.sin(Date.now()/200);
        ctx.fillStyle=`rgba(255,200,60,${pulse})`;
        ctx.beginPath(); ctx.arc(px,py,5,0,Math.PI*2); ctx.fill();
      }
    }));
    // ghosts
    ghosts.forEach(g=>{
      const gx=g.px+T/2, gy=g.py+T/2, gr=T/2-1;
      const flash = g.fright && frighTimer<120 && Math.floor(Date.now()/200)%2===0;
      ctx.fillStyle = g.fright ? (flash?'#fff':'#2020cc') : g.c;
      ctx.beginPath();
      ctx.arc(gx,gy-2,gr,Math.PI,0);
      ctx.lineTo(gx+gr,gy+gr);
      for(let i=2;i>=0;i--){
        ctx.lineTo(gx+gr*(i*2/3+1/3)-gr,gy+gr/2);
        ctx.lineTo(gx+gr*(i*2/3)-gr,gy+gr);
      }
      ctx.closePath(); ctx.fill();
      if(!g.fright){
        ctx.fillStyle='white';
        ctx.beginPath(); ctx.arc(gx-3,gy-3,2.5,0,Math.PI*2);
        ctx.arc(gx+3,gy-3,2.5,0,Math.PI*2); ctx.fill();
        ctx.fillStyle='#0a0a88';
        ctx.beginPath(); ctx.arc(gx-3+g.dx,gy-3+g.dy,1.2,0,Math.PI*2);
        ctx.arc(gx+3+g.dx,gy-3+g.dy,1.2,0,Math.PI*2); ctx.fill();
      }
    });
    // pac
    const px=pac.px+T/2, py=pac.py+T/2, pr=T/2-1;
    const ang = pac.dx||pac.dy ? Math.atan2(pac.dy,pac.dx) : 0;
    ctx.fillStyle='#ffe040';
    ctx.beginPath();
    ctx.moveTo(px,py);
    ctx.arc(px,py,pr, ang+pac.mouth*Math.PI, ang+(2-pac.mouth)*Math.PI);
    ctx.closePath(); ctx.fill();
  }

  function gameLoop(){
    if(!running){
      drawScene();
      ctx.fillStyle='rgba(5,13,20,0.82)'; ctx.fillRect(0,0,CW,CH);
      ctx.textAlign='center';
      ctx.font="bold 30px 'Bebas Neue',sans-serif";
      ctx.fillStyle=lives<=0?'#ff6b4a':'#00b4a0';
      ctx.fillText(lives<=0?'GAME OVER':'RIDGE PAC', CW/2, CH/2-18);
      ctx.font="13px 'Barlow Condensed',sans-serif";
      ctx.fillStyle='rgba(240,236,224,0.5)';
      ctx.fillText('Click here + SPACE to '+(lives<=0?'restart':'begin'), CW/2, CH/2+8);
      ctx.textAlign='left';
      return;
    }
    if(frighTimer>0) frighTimer--;
    movePac();
    ghosts.forEach(moveGhost);
    checkHits();
    drawScene();
    raf=requestAnimationFrame(gameLoop);
  }

  gameLoop(); // draw splash

  cv.addEventListener('click',()=>{ activeGame='pac'; if(!running) startGame(); });

  return {
    key(e){
      if(!running && (e.code==='Space'||e.key==='Enter')){ e.preventDefault(); startGame(); return; }
      if(!running) return;
      e.preventDefault();
      if(e.key==='ArrowUp')    { pac.nx=0;  pac.ny=-1; }
      if(e.key==='ArrowDown')  { pac.nx=0;  pac.ny=1;  }
      if(e.key==='ArrowLeft')  { pac.nx=-1; pac.ny=0;  }
      if(e.key==='ArrowRight') { pac.nx=1;  pac.ny=0;  }
    },
    start: startGame,
    dpad(dx,dy){ if(!running){startGame();return;} pac.nx=dx; pac.ny=dy; }
  };
})();
function pacKey(e){ PACMAN.key(e); }

/* ═════════ SERPENT ═════════ */
const SERPENT = (function(){
  const cv  = document.getElementById('serpentCanvas');
  const ctx = cv.getContext('2d');
  const W=cv.width, H=cv.height, C=20;
  const COLS=W/C, ROWS=H/C;
  const sEl=document.getElementById('serpentScore');
  const hEl=document.getElementById('serpentHigh');

  let sn, dir, ndir, food, sc, hi=0, running=false, dead=false, iv=null;

  function spawnFood(){
    let p;
    do { p={x:Math.floor(Math.random()*COLS), y:Math.floor(Math.random()*ROWS)}; }
    while(sn.some(s=>s.x===p.x&&s.y===p.y));
    food=p;
  }

  function init(){
    sn=[{x:5,y:10},{x:4,y:10},{x:3,y:10}];
    dir={x:1,y:0}; ndir={x:1,y:0};
    sc=0; dead=false;
    spawnFood(); sEl.textContent=0; draw();
  }

  function step(){
    dir={...ndir};
    const h={x:sn[0].x+dir.x, y:sn[0].y+dir.y};
    if(h.x<0||h.x>=COLS||h.y<0||h.y>=ROWS||sn.some(s=>s.x===h.x&&s.y===h.y)){
      running=false; dead=true; clearInterval(iv); draw(); return;
    }
    sn.unshift(h);
    if(h.x===food.x&&h.y===food.y){
      sc++; sEl.textContent=sc;
      if(sc>hi){ hi=sc; hEl.textContent=hi; }
      spawnFood();
    } else { sn.pop(); }
    draw();
  }

  function draw(){
    ctx.fillStyle='#050d14'; ctx.fillRect(0,0,W,H);
    ctx.strokeStyle='rgba(0,180,160,0.05)'; ctx.lineWidth=0.5;
    for(let x=0;x<=W;x+=C){ ctx.beginPath(); ctx.moveTo(x,0); ctx.lineTo(x,H); ctx.stroke(); }
    for(let y=0;y<=H;y+=C){ ctx.beginPath(); ctx.moveTo(0,y); ctx.lineTo(W,y); ctx.stroke(); }

    if(!running&&!dead){
      ctx.fillStyle='rgba(0,180,160,0.07)'; ctx.fillRect(0,0,W,H);
      ctx.textAlign='center';
      ctx.font="bold 26px 'Bebas Neue',sans-serif";
      ctx.fillStyle='#00b4a0'; ctx.fillText('RIDGE SERPENT',W/2,H/2-18);
      ctx.font="13px 'Barlow Condensed',sans-serif";
      ctx.fillStyle='rgba(240,236,224,0.45)';
      ctx.fillText('Click here + SPACE to begin',W/2,H/2+8);
      ctx.textAlign='left'; return;
    }

    // food
    const t=Date.now()/500, pulse=0.85+0.15*Math.sin(t*Math.PI*2);
    ctx.save(); ctx.translate(food.x*C+C/2,food.y*C+C/2); ctx.scale(pulse,pulse);
    ctx.fillStyle='#ff6b4a';
    ctx.beginPath(); ctx.moveTo(0,-7); ctx.lineTo(7,0); ctx.lineTo(0,7); ctx.lineTo(-7,0); ctx.closePath(); ctx.fill();
    ctx.restore();

    // snake
    sn.forEach((s,i)=>{
      const isHead=i===0;
      const ratio=1-(i/sn.length)*0.5;
      ctx.fillStyle=isHead?'#00d4bb':`rgb(${Math.round(5+ratio*10)},${Math.round(140+ratio*40)},${Math.round(130+ratio*20)})`;
      const pd=isHead?1:2, cr=isHead?4:3;
      const x=s.x*C, y=s.y*C;
      ctx.beginPath();
      ctx.moveTo(x+pd+cr,y+pd);
      ctx.lineTo(x+C-pd-cr,y+pd);
      ctx.quadraticCurveTo(x+C-pd,y+pd,x+C-pd,y+pd+cr);
      ctx.lineTo(x+C-pd,y+C-pd-cr);
      ctx.quadraticCurveTo(x+C-pd,y+C-pd,x+C-pd-cr,y+C-pd);
      ctx.lineTo(x+pd+cr,y+C-pd);
      ctx.quadraticCurveTo(x+pd,y+C-pd,x+pd,y+C-pd-cr);
      ctx.lineTo(x+pd,y+pd+cr);
      ctx.quadraticCurveTo(x+pd,y+pd,x+pd+cr,y+pd);
      ctx.closePath(); ctx.fill();
      if(isHead){
        ctx.fillStyle='#050d14';
        ctx.fillRect(s.x*C+5,s.y*C+5,3,3);
        ctx.fillRect(s.x*C+12,s.y*C+5,3,3);
      }
    });

    if(dead){
      ctx.fillStyle='rgba(5,13,20,0.8)'; ctx.fillRect(0,0,W,H);
      ctx.textAlign='center';
      ctx.font="bold 30px 'Bebas Neue',sans-serif";
      ctx.fillStyle='#ff6b4a'; ctx.fillText('GAME OVER',W/2,H/2-22);
      ctx.font="15px 'Barlow Condensed',sans-serif";
      ctx.fillStyle='rgba(240,236,224,0.65)';
      ctx.fillText(`Score: ${sc}   Best: ${hi}`,W/2,H/2+2);
      ctx.fillStyle='rgba(240,236,224,0.35)';
      ctx.fillText('Click here + SPACE to retry',W/2,H/2+26);
      ctx.textAlign='left';
    }
  }

  function startGame(){
    if(running) return;
    init(); running=true;
    clearInterval(iv);
    iv=setInterval(step, 130);
    activeGame='serpent';
  }

  // render loop for smooth food pulse
  (function animLoop(){
    if(!running) draw();
    requestAnimationFrame(animLoop);
  })();

  init();
  cv.addEventListener('click',()=>{ activeGame='serpent'; if(!running) startGame(); });

  // touch swipe
  let ts=null;
  cv.addEventListener('touchstart',e=>{ e.preventDefault(); ts={x:e.touches[0].clientX,y:e.touches[0].clientY}; if(!running) startGame(); },{passive:false});
  cv.addEventListener('touchend',e=>{
    if(!ts||!running) return;
    const dx=e.changedTouches[0].clientX-ts.x, dy=e.changedTouches[0].clientY-ts.y;
    if(Math.abs(dx)>Math.abs(dy)){
      if(dx>15&&dir.x!==-1) ndir={x:1,y:0};
      if(dx<-15&&dir.x!==1) ndir={x:-1,y:0};
    } else {
      if(dy>15&&dir.y!==-1) ndir={x:0,y:1};
      if(dy<-15&&dir.y!==1) ndir={x:0,y:-1};
    }
    ts=null;
  },{passive:false});

  return {
    key(e){
      if(!running && (e.code==='Space'||e.key==='Enter')){ e.preventDefault(); startGame(); return; }
      if(!running) return;
      e.preventDefault();
      if(e.key==='ArrowUp'   &&dir.y!==1)  ndir={x:0,y:-1};
      if(e.key==='ArrowDown' &&dir.y!==-1) ndir={x:0,y:1};
      if(e.key==='ArrowLeft' &&dir.x!==1)  ndir={x:-1,y:0};
      if(e.key==='ArrowRight'&&dir.x!==-1) ndir={x:1,y:0};
    },
    dpad(dx,dy){
      if(!running){startGame();return;}
      if(dx===1&&dir.x!==-1)  ndir={x:1,y:0};
      if(dx===-1&&dir.x!==1) ndir={x:-1,y:0};
      if(dy===1&&dir.y!==-1)  ndir={x:0,y:1};
      if(dy===-1&&dir.y!==1) ndir={x:0,y:-1};
    }
  };
})();
function serpentKey(e){ SERPENT.key(e); }



/* ═════════ CENTIPEDE ═════════ */
const CENTIPEDE = (function(){
  const cv  = document.getElementById('centCanvas');
  const ctx = cv.getContext('2d');
  const W = cv.width, H = cv.height;
  const COLS = 21, ROWS = 26;
  const TW = W / COLS, TH = H / ROWS;
  const scoreEl = document.getElementById('centScore');
  const livesEl = document.getElementById('centLives');

  // ── STATE ──
  let mushrooms, centipedes, bullets, player, fleas, spiders;
  let score, lives, level, running, dead, deathTimer, raf;
  let dirInput = 0; // -1 left, 0 still, 1 right
  let prevTime = 0;

  function initMushrooms() {
    mushrooms = [];
    const count = 30 + level * 5;
    for (let i = 0; i < count; i++) {
      const col = Math.floor(Math.random() * COLS);
      const row = Math.floor(Math.random() * (ROWS - 5)) + 1;
      if (!mushrooms.find(m => m.col === col && m.row === row)) {
        mushrooms.push({ col, row, hp: 4 });
      }
    }
  }

  function spawnCentipede(segments = 12) {
    const segs = [];
    for (let i = 0; i < segments; i++) {
      segs.push({
        col: COLS - 1 - i,
        row: 0,
        dx: 1,  // moving right initially, will flip
        dy: 0,
        px: (COLS - 1 - i) * TW + TW / 2,
        py: TH / 2,
        isHead: i === 0,
        targetRow: 0,
        moving: true,
      });
    }
    centipedes.push(...segs);
  }

  function init() {
    score  = score || 0;
    lives  = lives !== undefined ? lives : 3;
    level  = level || 1;
    dead   = false;
    deathTimer = 0;
    mushrooms  = [];
    centipedes = [];
    bullets    = [];
    fleas      = [];
    spiders    = [];
    initMushrooms();
    spawnCentipede(12);
    player = {
      px: W / 2, py: H - TH * 1.5,
      speed: TW * 8,
      fireRate: 0.22,
      fireCooldown: 0,
    };
    scoreEl.textContent = score;
    livesEl.textContent = lives;
  }

  function hasMushroom(col, row) {
    return mushrooms.find(m => m.col === col && m.row === row && m.hp > 0);
  }

  function update(dt) {
    // ── PLAYER MOVEMENT ──
    player.px += dirInput * player.speed * dt;
    player.px  = Math.max(TW / 2, Math.min(W - TW / 2, player.px));

    // ── AUTO FIRE when direction held ──
    player.fireCooldown -= dt;
    if (player.fireCooldown <= 0 && dirInput !== 0) {
      shootBullet();
      player.fireCooldown = player.fireRate;
    }

    // ── BULLETS ──
    const bulletSpeed = TH * 22;
    bullets = bullets.filter(b => {
      b.py -= bulletSpeed * dt;
      if (b.py < 0) return false;

      // Hit mushroom
      const col = Math.round((b.px - TW / 2) / TW);
      const row = Math.round((b.py - TH / 2) / TH);
      const mush = hasMushroom(col, row);
      if (mush) {
        mush.hp--;
        if (mush.hp <= 0) { mushrooms = mushrooms.filter(m => m !== mush); score += 1; }
        return false;
      }

      // Hit centipede
      for (let i = centipedes.length - 1; i >= 0; i--) {
        const seg = centipedes[i];
        if (Math.hypot(b.px - seg.px, b.py - seg.py) < TW * 0.6) {
          score += seg.isHead ? 100 : 10;
          scoreEl.textContent = score;
          // Leave mushroom
          const mc = Math.round((seg.px - TW / 2) / TW);
          const mr = Math.round((seg.py - TH / 2) / TH);
          if (!hasMushroom(mc, mr)) mushrooms.push({ col: mc, row: mr, hp: 4 });
          // Split centipede — segment after becomes a new head
          if (i + 1 < centipedes.length) centipedes[i + 1].isHead = true;
          centipedes.splice(i, 1);
          if (centipedes.length === 0) nextLevel();
          return false;
        }
      }

      // Hit flea
      fleas = fleas.filter(f => {
        if (Math.hypot(b.px - f.px, b.py - f.py) < TW * 0.6) {
          score += 200; scoreEl.textContent = score; return false;
        }
        return true;
      });

      // Hit spider
      spiders = spiders.filter(sp => {
        if (Math.hypot(b.px - sp.px, b.py - sp.py) < TW * 0.7) {
          score += 600; scoreEl.textContent = score; return false;
        }
        return true;
      });

      return true;
    });

    // ── CENTIPEDE MOVEMENT ──
    const cSpeed = TH * (4 + level * 0.6);
    centipedes.forEach(seg => {
      seg.px += seg.dx * cSpeed * dt;
      const col = seg.px / TW;

      // Hit wall or mushroom — turn down then reverse
      const atRightEdge = seg.dx > 0 && seg.px >= (COLS - 0.5) * TW;
      const atLeftEdge  = seg.dx < 0 && seg.px <= 0.5 * TW;
      const nextCol = Math.round(col + seg.dx);
      const nextRow = Math.round(seg.py / TH);
      const blocked = hasMushroom(nextCol, nextRow);

      if (atRightEdge || atLeftEdge || blocked) {
        seg.dx *= -1;
        seg.py += TH;
        // Clamp into player zone and reset
        if (seg.py >= H - TH) {
          seg.py = H - TH;
          seg.dx = seg.dx; // keep direction
        }
        // Snap x
        seg.px = Math.max(TW / 2, Math.min((COLS - 0.5) * TW, seg.px));
      }
    });

    // ── FLEA SPAWN ──
    if (Math.random() < 0.003 + level * 0.001) {
      fleas.push({ px: Math.random() * W, py: -TH, speed: TH * (12 + Math.random() * 8) });
    }
    fleas = fleas.filter(f => {
      f.py += f.speed * dt;
      // Drop mushrooms
      if (Math.random() < 0.04) {
        const fc = Math.round(f.px / TW - 0.5);
        const fr = Math.round(f.py / TH);
        if (fr >= 0 && fr < ROWS && !hasMushroom(fc, fr)) {
          mushrooms.push({ col: fc, row: fr, hp: 4 });
        }
      }
      return f.py < H + TH;
    });

    // ── SPIDER ──
    if (Math.random() < 0.002 + level * 0.0005 && spiders.length < 1) {
      const fromLeft = Math.random() < 0.5;
      spiders.push({
        px: fromLeft ? -TW : W + TW,
        py: H - TH * (2 + Math.random() * 4),
        dx: fromLeft ? 1 : -1,
        dy: 0,
        timer: 0,
        speed: TW * (6 + Math.random() * 4),
      });
    }
    spiders = spiders.filter(sp => {
      sp.timer += dt;
      if (sp.timer > 0.4) { sp.dy = (Math.random() - 0.5) * TH * 4; sp.timer = 0; }
      sp.px += sp.dx * sp.speed * dt;
      sp.py += sp.dy * dt;
      sp.py  = Math.max(H - TH * 7, Math.min(H - TH, sp.py));
      // Eat mushrooms
      const sc2 = Math.round(sp.px / TW - 0.5);
      const sr  = Math.round(sp.py / TH);
      const eaten = mushrooms.find(m => m.col === sc2 && m.row === sr);
      if (eaten) mushrooms = mushrooms.filter(m => m !== eaten);
      return sp.px > -TW * 2 && sp.px < W + TW * 2;
    });

    // ── COLLISION: centipede/flea/spider vs player ──
    const pr = TW * 0.55;
    [...centipedes, ...fleas, ...spiders].forEach(e => {
      if (Math.hypot(e.px - player.px, e.py - player.py) < pr * 1.8) {
        loseLife();
      }
    });
  }

  function loseLife() {
    lives--;
    livesEl.textContent = lives;
    if (lives <= 0) {
      running = false; dead = true;
    } else {
      // Reset player position, clear bullets
      player.px = W / 2;
      bullets = [];
      centipedes = [];
      fleas = [];
      spiders = [];
      spawnCentipede(12);
    }
  }

  function nextLevel() {
    level++;
    bullets = [];
    fleas   = [];
    spiders = [];
    initMushrooms();
    spawnCentipede(Math.min(20, 12 + level));
    player.px = W / 2;
  }

  function shootBullet() {
    bullets.push({ px: player.px, py: player.py - TH });
    player.fireCooldown = player.fireRate;
  }

  // ── DRAW ──
  function draw() {
    ctx.fillStyle = '#050d14';
    ctx.fillRect(0, 0, W, H);

    // Grid
    ctx.strokeStyle = 'rgba(0,180,160,0.04)'; ctx.lineWidth = 0.5;
    for (let x = 0; x <= W; x += TW) { ctx.beginPath(); ctx.moveTo(x, 0); ctx.lineTo(x, H); ctx.stroke(); }
    for (let y = 0; y <= H; y += TH) { ctx.beginPath(); ctx.moveTo(0, y); ctx.lineTo(W, y); ctx.stroke(); }

    // Player zone line
    ctx.strokeStyle = 'rgba(0,180,160,0.12)'; ctx.lineWidth = 1;
    ctx.setLineDash([4, 4]);
    ctx.beginPath(); ctx.moveTo(0, H - TH * 6); ctx.lineTo(W, H - TH * 6); ctx.stroke();
    ctx.setLineDash([]);

    // Mushrooms
    mushrooms.forEach(m => {
      const x = m.col * TW, y = m.row * TH;
      const hpColor = ['#883300','#bb4400','#dd7700','#00b46a'][Math.min(3, m.hp - 1)];
      ctx.fillStyle = hpColor;
      ctx.beginPath();
      ctx.arc(x + TW/2, y + TH/2, TW * 0.42, 0, Math.PI * 2);
      ctx.fill();
      ctx.fillStyle = 'rgba(255,255,255,0.12)';
      ctx.beginPath();
      ctx.arc(x + TW*0.35, y + TH*0.3, TW * 0.13, 0, Math.PI * 2);
      ctx.fill();
    });

    // Centipede
    centipedes.forEach((seg, i) => {
      const r = TW * 0.44;
      ctx.fillStyle = seg.isHead ? '#00d4bb' : '#2dd28c';
      ctx.beginPath(); ctx.arc(seg.px, seg.py, r, 0, Math.PI * 2); ctx.fill();
      // Head detail
      if (seg.isHead) {
        ctx.fillStyle = '#050d14';
        ctx.beginPath(); ctx.arc(seg.px - r * 0.3, seg.py - r * 0.25, r * 0.22, 0, Math.PI * 2); ctx.fill();
        ctx.beginPath(); ctx.arc(seg.px + r * 0.3, seg.py - r * 0.25, r * 0.22, 0, Math.PI * 2); ctx.fill();
        // Antennae
        ctx.strokeStyle = '#00d4bb'; ctx.lineWidth = 1.2;
        ctx.beginPath(); ctx.moveTo(seg.px - r*0.2, seg.py - r); ctx.lineTo(seg.px - r*0.5, seg.py - r*1.8); ctx.stroke();
        ctx.beginPath(); ctx.moveTo(seg.px + r*0.2, seg.py - r); ctx.lineTo(seg.px + r*0.5, seg.py - r*1.8); ctx.stroke();
      } else {
        ctx.fillStyle = 'rgba(0,0,0,0.25)';
        ctx.beginPath(); ctx.arc(seg.px, seg.py, r * 0.5, 0, Math.PI * 2); ctx.fill();
      }
      // Connect segments
      if (i < centipedes.length - 1) {
        const next = centipedes[i + 1];
        ctx.strokeStyle = 'rgba(45,210,140,0.4)'; ctx.lineWidth = TW * 0.35;
        ctx.beginPath(); ctx.moveTo(seg.px, seg.py); ctx.lineTo(next.px, next.py); ctx.stroke();
      }
    });

    // Bullets
    bullets.forEach(b => {
      ctx.fillStyle = '#ffe040';
      ctx.fillRect(b.px - 2, b.py - 7, 4, 14);
      ctx.fillStyle = 'rgba(255,220,0,0.3)';
      ctx.fillRect(b.px - 4, b.py - 10, 8, 20);
    });

    // Fleas
    fleas.forEach(f => {
      ctx.fillStyle = '#ff9900';
      ctx.beginPath(); ctx.arc(f.px, f.py, TW * 0.3, 0, Math.PI * 2); ctx.fill();
      ctx.fillStyle = '#ffcc00';
      ctx.beginPath(); ctx.arc(f.px - TW*0.1, f.py - TW*0.1, TW * 0.1, 0, Math.PI * 2); ctx.fill();
    });

    // Spiders
    spiders.forEach(sp => {
      ctx.fillStyle = '#cc44ff';
      ctx.beginPath(); ctx.arc(sp.px, sp.py, TW * 0.5, 0, Math.PI * 2); ctx.fill();
      // Spider legs
      ctx.strokeStyle = '#aa22dd'; ctx.lineWidth = 1.2;
      for (let l = 0; l < 4; l++) {
        const ang1 = (l / 4) * Math.PI;
        const ang2 = ang1 + Math.PI * 0.15;
        ctx.beginPath(); ctx.moveTo(sp.px, sp.py); ctx.lineTo(sp.px + Math.cos(ang1)*TW*0.9, sp.py + Math.sin(ang1)*TH*0.7); ctx.stroke();
        ctx.beginPath(); ctx.moveTo(sp.px, sp.py); ctx.lineTo(sp.px + Math.cos(ang1+Math.PI)*TW*0.9, sp.py + Math.sin(ang1+Math.PI)*TH*0.7); ctx.stroke();
      }
      ctx.fillStyle = '#ff66ff';
      ctx.beginPath(); ctx.arc(sp.px-TW*0.15, sp.py-TH*0.15, TW*0.14, 0, Math.PI*2); ctx.fill();
      ctx.beginPath(); ctx.arc(sp.px+TW*0.15, sp.py-TH*0.15, TW*0.14, 0, Math.PI*2); ctx.fill();
    });

    // Player ship
    const px = player.px, py = player.py;
    ctx.fillStyle = '#00b4a0';
    ctx.beginPath();
    ctx.moveTo(px, py - TH * 0.75);
    ctx.lineTo(px + TW * 0.55, py + TH * 0.5);
    ctx.lineTo(px + TW * 0.2, py + TH * 0.3);
    ctx.lineTo(px - TW * 0.2, py + TH * 0.3);
    ctx.lineTo(px - TW * 0.55, py + TH * 0.5);
    ctx.closePath(); ctx.fill();
    ctx.fillStyle = 'rgba(0,212,187,0.3)';
    ctx.beginPath(); ctx.arc(px, py, TW * 0.28, 0, Math.PI * 2); ctx.fill();
    // Engine glow
    ctx.fillStyle = '#ff6b4a';
    ctx.beginPath(); ctx.arc(px, py + TH * 0.38, TW * 0.14, 0, Math.PI * 2); ctx.fill();

    // HUD: level
    ctx.font = "bold 11px 'Barlow Condensed',sans-serif";
    ctx.fillStyle = 'rgba(0,180,160,0.5)';
    ctx.textAlign = 'right';
    ctx.fillText('LVL ' + level, W - 6, 14);
    ctx.textAlign = 'left';

    // Splash
    if (!running && !dead) {
      ctx.fillStyle = 'rgba(0,180,160,0.07)'; ctx.fillRect(0, 0, W, H);
      ctx.textAlign = 'center';
      ctx.font = "bold 28px 'Bebas Neue',sans-serif";
      ctx.fillStyle = '#00b4a0'; ctx.fillText('RIDGE CENTIPEDE', W/2, H/2 - 30);
      ctx.font = "13px 'Barlow Condensed',sans-serif";
      ctx.fillStyle = 'rgba(240,236,224,0.45)';
      ctx.fillText('Click here or SPACE to begin', W/2, H/2);
      ctx.fillText('Destroy all centipede segments to advance levels', W/2, H/2 + 20);
      ctx.textAlign = 'left';
    }

    // Death screen
    if (dead) {
      ctx.fillStyle = 'rgba(5,13,20,0.82)'; ctx.fillRect(0, 0, W, H);
      ctx.textAlign = 'center';
      ctx.font = "bold 30px 'Bebas Neue',sans-serif";
      ctx.fillStyle = '#ff6b4a'; ctx.fillText('GAME OVER', W/2, H/2 - 20);
      ctx.font = "15px 'Barlow Condensed',sans-serif";
      ctx.fillStyle = 'rgba(240,236,224,0.65)';
      ctx.fillText('Score: ' + score, W/2, H/2 + 6);
      ctx.fillStyle = 'rgba(240,236,224,0.35)';
      ctx.fillText('Click here + SPACE to retry', W/2, H/2 + 28);
      ctx.textAlign = 'left';
    }
  }

  // ── GAME LOOP ──
  function gameLoop(ts) {
    const dt = Math.min(0.05, (ts - (prevTime || ts)) / 1000);
    prevTime = ts;
    if (running && !dead) update(dt);
    draw();
    raf = requestAnimationFrame(gameLoop);
  }

  function startGame() {
    score = 0; lives = 3; level = 1;
    init();
    running = true;
    dead    = false;
    activeGame = 'centipede';
  }

  function restartGame() {
    score = 0; lives = 3; level = 1;
    init();
    running = true;
    dead    = false;
    activeGame = 'centipede';
  }

  // Start render loop immediately (shows splash)
  raf = requestAnimationFrame(gameLoop);
  init();

  // Click to start
  cv.addEventListener('click', () => {
    activeGame = 'centipede';
    if (!running || dead) restartGame();
  });

  // Touch swipe to move
  let touchX = null;
  cv.addEventListener('touchstart', e => {
    e.preventDefault();
    touchX = e.touches[0].clientX;
    activeGame = 'centipede';
    if (!running || dead) restartGame();
  }, { passive: false });
  cv.addEventListener('touchmove', e => {
    e.preventDefault();
    if (!running || touchX === null) return;
    const dx = e.touches[0].clientX - touchX;
    dirInput = dx > 5 ? 1 : dx < -5 ? -1 : 0;
  }, { passive: false });
  cv.addEventListener('touchend', e => {
    e.preventDefault();
    dirInput = 0;
    touchX = null;
    if (running) shootBullet();
  }, { passive: false });

  return {
    key(e) {
      if ((e.code === 'Space' || e.key === 'Enter') && (!running || dead)) {
        e.preventDefault(); restartGame(); return;
      }
      if (!running || dead) return;
      e.preventDefault();
      if (e.key === 'ArrowLeft')  dirInput = -1;
      if (e.key === 'ArrowRight') dirInput = 1;
      if (e.code === 'Space')     { shootBullet(); player.fireCooldown = player.fireRate; }
    },
    keyup(e) {
      if (e.key === 'ArrowLeft' && dirInput === -1)  dirInput = 0;
      if (e.key === 'ArrowRight' && dirInput === 1) dirInput = 0;
    },
    setDir(d) { dirInput = d; if (d !== 0 && running && !dead) shootBullet(); },
    fire()    { if (running && !dead) shootBullet(); }
  };
})();

// Hook centipede into global key router
document.addEventListener('keydown',  e => { if (activeGame === 'centipede') CENTIPEDE.key(e); });
document.addEventListener('keyup',    e => { if (activeGame === 'centipede') CENTIPEDE.keyup(e); });
document.getElementById('centCanvas').addEventListener('click', () => { activeGame = 'centipede'; });

/* ═════════ FULLSCREEN ═════════ */
function toggleFS(btn) {
  const panel = btn.closest('.game-panel');
  const isFS = document.fullscreenElement || document.webkitFullscreenElement || document.mozFullScreenElement;
  if (!isFS) {
    (panel.requestFullscreen || panel.webkitRequestFullscreen || panel.mozRequestFullScreen).call(panel);
    btn.textContent = '✕ Exit';
  } else {
    (document.exitFullscreen || document.webkitExitFullscreen || document.mozCancelFullScreen).call(document);
    btn.textContent = '⛶ Fullscreen';
  }
}
document.addEventListener('fullscreenchange', () => {
  if (!document.fullscreenElement) {
    document.querySelectorAll('.fs-btn').forEach(b => b.textContent = '⛶ Fullscreen');
  }
});
</script>
</body>
</html>
