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
    <li><a href="#hero">Home</a></li>
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
  <p style="max-width:500px;color:rgba(240,236,224,0.65);font-size:0.95rem;line-height:1.8;">Two games built right here on the mountain. Fully playable below.</p>
  <div class="games-layout">
    <div class="game-panel">
      <div class="game-header">
        <div class="game-tag">Sandbox · Simulation · 188 Elements</div>
        <div class="game-title">⬡ Elemental</div>
      </div>
      <div style="position:relative;width:100%;height:700px;background:#07080c;">
        <iframe src="elemental.html" style="width:100%;height:100%;border:none;display:block;" title="Elemental Sandbox Game" allowfullscreen></iframe>
      </div>
      <div class="game-controls">Click/drag to place elements &nbsp;·&nbsp; 188+ real elements &nbsp;·&nbsp; Full Periodic Table &nbsp;·&nbsp; Heat · Cool · Zap · Grind tools</div>
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

<footer>
  <div class="footer-logo">RidgeRush<span class="dash">-</span><span class="mtb">MTB</span></div>
  <div class="footer-links">
    <a href="#practice">Skills Areas</a>
    <a href="#trails">Trails</a>
    <a href="#games">Arcade</a>
    <a href="#">Contact</a>
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

/* ═════════ SERPENT ═════════ */
(function(){
  const cv=document.getElementById('serpentCanvas'),ctx=cv.getContext('2d');
  const W=cv.width,H=cv.height,C=20,COLS=W/C,ROWS=H/C;
  const sEl=document.getElementById('serpentScore'),hEl=document.getElementById('serpentHigh');
  let sn,dir,ndir,food,sc,hi=0,run=false,dead=false,iv=null;
  function init(){sn=[{x:5,y:10},{x:4,y:10},{x:3,y:10}];dir={x:1,y:0};ndir={x:1,y:0};sc=0;dead=false;spawnF();sEl.textContent=0;draw();}
  function spawnF(){let p;do{p={x:Math.floor(Math.random()*COLS),y:Math.floor(Math.random()*ROWS)}}while(sn.some(s=>s.x===p.x&&s.y===p.y));food=p;}
  function step(){
    dir=ndir;const h={x:sn[0].x+dir.x,y:sn[0].y+dir.y};
    if(h.x<0||h.x>=COLS||h.y<0||h.y>=ROWS||sn.some(s=>s.x===h.x&&s.y===h.y)){run=false;dead=true;clearInterval(iv);draw();return;}
    sn.unshift(h);
    if(h.x===food.x&&h.y===food.y){sc++;sEl.textContent=sc;if(sc>hi){hi=sc;hEl.textContent=hi;}spawnF();}else{sn.pop();}
    draw();
  }
  function draw(){
    ctx.fillStyle='#050d14';ctx.fillRect(0,0,W,H);
    ctx.strokeStyle='rgba(0,180,160,0.05)';ctx.lineWidth=0.5;
    for(let x=0;x<=W;x+=C){ctx.beginPath();ctx.moveTo(x,0);ctx.lineTo(x,H);ctx.stroke();}
    for(let y=0;y<=H;y+=C){ctx.beginPath();ctx.moveTo(0,y);ctx.lineTo(W,y);ctx.stroke();}
    if(!run&&!dead){
      ctx.fillStyle='rgba(0,180,160,0.07)';ctx.fillRect(0,0,W,H);
      ctx.font="bold 26px 'Bebas Neue',sans-serif";ctx.fillStyle='#00b4a0';ctx.textAlign='center';
      ctx.fillText('RIDGE SERPENT',W/2,H/2-20);
      ctx.font="14px 'Barlow Condensed',sans-serif";ctx.fillStyle='rgba(240,236,224,0.5)';
      ctx.fillText('Press SPACE to begin',W/2,H/2+15);ctx.textAlign='left';return;
    }
    const t=Date.now()/500,p=0.85+0.15*Math.sin(t*Math.PI*2);
    ctx.save();ctx.translate(food.x*C+C/2,food.y*C+C/2);ctx.scale(p,p);
    ctx.fillStyle='#ff6b4a';ctx.beginPath();ctx.moveTo(0,-7);ctx.lineTo(7,0);ctx.lineTo(0,7);ctx.lineTo(-7,0);ctx.closePath();ctx.fill();ctx.restore();
    sn.forEach((s,i)=>{
      const iH=i===0,r=1-(i/sn.length)*0.5;
      ctx.fillStyle=iH?'#00d4bb':`rgb(${Math.round(0+r*10)},${Math.round(140+r*40)},${Math.round(140+r*20)})`;
      const pd=iH?1:2,cr=iH?4:3;
      ctx.beginPath();ctx.moveTo(s.x*C+pd+cr,s.y*C+pd);ctx.lineTo(s.x*C+C-pd-cr,s.y*C+pd);ctx.quadraticCurveTo(s.x*C+C-pd,s.y*C+pd,s.x*C+C-pd,s.y*C+pd+cr);ctx.lineTo(s.x*C+C-pd,s.y*C+C-pd-cr);ctx.quadraticCurveTo(s.x*C+C-pd,s.y*C+C-pd,s.x*C+C-pd-cr,s.y*C+C-pd);ctx.lineTo(s.x*C+pd+cr,s.y*C+C-pd);ctx.quadraticCurveTo(s.x*C+pd,s.y*C+C-pd,s.x*C+pd,s.y*C+C-pd-cr);ctx.lineTo(s.x*C+pd,s.y*C+pd+cr);ctx.quadraticCurveTo(s.x*C+pd,s.y*C+pd,s.x*C+pd+cr,s.y*C+pd);ctx.closePath();ctx.fill();
      if(iH){ctx.fillStyle='#050d14';ctx.fillRect(s.x*C+5,s.y*C+5,3,3);ctx.fillRect(s.x*C+12,s.y*C+5,3,3);}
    });
    if(dead){
      ctx.fillStyle='rgba(5,13,20,0.78)';ctx.fillRect(0,0,W,H);
      ctx.font="bold 30px 'Bebas Neue',sans-serif";ctx.fillStyle='#ff6b4a';ctx.textAlign='center';ctx.fillText('GAME OVER',W/2,H/2-25);
      ctx.font="16px 'Barlow Condensed',sans-serif";ctx.fillStyle='rgba(240,236,224,0.7)';ctx.fillText(`Score: ${sc}   High: ${hi}`,W/2,H/2+5);
      ctx.fillStyle='rgba(240,236,224,0.4)';ctx.fillText('Press SPACE to play again',W/2,H/2+30);ctx.textAlign='left';
    }
  }
  function start(){if(run)return;init();run=true;clearInterval(iv);iv=setInterval(step,140);}
  document.addEventListener('keydown',e=>{
    if(e.code==='Space'){e.preventDefault();if(!run||dead)start();}
    if(!run)return;
    if(e.key==='ArrowUp'&&dir.y!==1)ndir={x:0,y:-1};
    if(e.key==='ArrowDown'&&dir.y!==-1)ndir={x:0,y:1};
    if(e.key==='ArrowLeft'&&dir.x!==1)ndir={x:-1,y:0};
    if(e.key==='ArrowRight'&&dir.x!==-1)ndir={x:1,y:0};
  });
  let ts=null;
  cv.addEventListener('touchstart',e=>{e.preventDefault();ts={x:e.touches[0].clientX,y:e.touches[0].clientY};if(!run||dead)start();},{passive:false});
  cv.addEventListener('touchend',e=>{
    if(!ts||!run)return;
    const dx=e.changedTouches[0].clientX-ts.x,dy=e.changedTouches[0].clientY-ts.y;
    if(Math.abs(dx)>Math.abs(dy)){if(dx>20&&dir.x!==-1)ndir={x:1,y:0};if(dx<-20&&dir.x!==1)ndir={x:-1,y:0};}
    else{if(dy>20&&dir.y!==-1)ndir={x:0,y:1};if(dy<-20&&dir.y!==1)ndir={x:0,y:-1};}
    ts=null;
  },{passive:false});
  function loop(){if(!run){draw();requestAnimationFrame(loop);}}
  init();loop();
})();
</script>
</body>
</html>
