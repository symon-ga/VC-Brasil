# VC-Brasil
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>VC Brasil — Sistema de Inteligência de Mercado</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400&family=IBM+Plex+Mono:wght@300;400;500&family=IBM+Plex+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0a0a08;
    --surface: #111110;
    --border: rgba(255,255,255,0.07);
    --border-accent: rgba(212,175,55,0.3);
    --gold: #d4af37;
    --gold-dim: rgba(212,175,55,0.15);
    --gold-bright: #f0d060;
    --text: #e8e4d9;
    --text-dim: rgba(232,228,217,0.45);
    --text-mid: rgba(232,228,217,0.7);
    --red: #c0392b;
    --green: #2ecc71;
    --accent-blue: #4a9eff;
    --grid-col: 12px;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'IBM Plex Sans', sans-serif;
    font-size: 15px;
    line-height: 1.7;
    overflow-x: hidden;
  }

  /* ── NOISE TEXTURE ── */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.035'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 999;
    opacity: 0.6;
  }

  /* ── NAVIGATION ── */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 100;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 48px;
    height: 60px;
    background: rgba(10,10,8,0.92);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid var(--border);
  }

  .nav-logo {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 12px;
    letter-spacing: 0.15em;
    color: var(--gold);
    text-decoration: none;
    font-weight: 500;
  }

  .nav-links {
    display: flex;
    gap: 36px;
    list-style: none;
  }

  .nav-links a {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.12em;
    color: var(--text-dim);
    text-decoration: none;
    transition: color 0.2s;
    text-transform: uppercase;
  }

  .nav-links a:hover { color: var(--gold); }

  .nav-tag {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 9px;
    color: var(--text-dim);
    letter-spacing: 0.1em;
    border: 1px solid var(--border);
    padding: 4px 10px;
  }

  /* ── HERO ── */
  #hero {
    min-height: 100vh;
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding-top: 60px;
    position: relative;
    overflow: hidden;
  }

  .hero-grid-lines {
    position: absolute;
    inset: 0;
    background-image:
      linear-gradient(rgba(255,255,255,0.02) 1px, transparent 1px),
      linear-gradient(90deg, rgba(255,255,255,0.02) 1px, transparent 1px);
    background-size: 80px 80px;
  }

  .hero-glow {
    position: absolute;
    top: 20%;
    left: 5%;
    width: 600px;
    height: 600px;
    background: radial-gradient(ellipse, rgba(212,175,55,0.06) 0%, transparent 70%);
    pointer-events: none;
  }

  .hero-left {
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 80px 64px 80px 80px;
    position: relative;
    z-index: 2;
  }

  .hero-label {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.2em;
    color: var(--gold);
    text-transform: uppercase;
    margin-bottom: 32px;
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .hero-label::before {
    content: '';
    width: 24px;
    height: 1px;
    background: var(--gold);
  }

  h1 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(48px, 6vw, 80px);
    font-weight: 900;
    line-height: 1.0;
    letter-spacing: -0.02em;
    margin-bottom: 32px;
  }

  h1 em {
    font-style: italic;
    color: var(--gold);
  }

  .hero-desc {
    font-size: 15px;
    color: var(--text-mid);
    max-width: 440px;
    line-height: 1.8;
    margin-bottom: 48px;
    font-weight: 300;
  }

  .hero-cta-row {
    display: flex;
    gap: 16px;
    align-items: center;
  }

  .btn-primary {
    background: var(--gold);
    color: #0a0a08;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    padding: 14px 28px;
    text-decoration: none;
    font-weight: 500;
    transition: background 0.2s;
  }

  .btn-primary:hover { background: var(--gold-bright); }

  .btn-ghost {
    color: var(--text-dim);
    font-family: 'IBM Plex Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    text-decoration: none;
    border-bottom: 1px solid var(--border);
    padding-bottom: 2px;
    transition: color 0.2s;
  }

  .btn-ghost:hover { color: var(--text); }

  .hero-right {
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
    z-index: 2;
    padding: 80px 48px;
  }

  .hero-stats-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2px;
    width: 100%;
    max-width: 460px;
  }

  .stat-card {
    background: var(--surface);
    border: 1px solid var(--border);
    padding: 28px;
    position: relative;
    overflow: hidden;
    animation: fadeUp 0.6s ease both;
  }

  .stat-card:nth-child(1) { animation-delay: 0.1s; }
  .stat-card:nth-child(2) { animation-delay: 0.2s; }
  .stat-card:nth-child(3) { animation-delay: 0.3s; }
  .stat-card:nth-child(4) { animation-delay: 0.4s; }

  .stat-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0;
    width: 2px;
    height: 100%;
    background: var(--gold);
    opacity: 0.4;
  }

  .stat-num {
    font-family: 'Playfair Display', serif;
    font-size: 40px;
    font-weight: 700;
    color: var(--gold);
    line-height: 1;
    margin-bottom: 8px;
  }

  .stat-label {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 9px;
    letter-spacing: 0.12em;
    color: var(--text-dim);
    text-transform: uppercase;
    line-height: 1.5;
  }

  .stat-context {
    font-size: 11px;
    color: var(--text-dim);
    margin-top: 6px;
    font-style: italic;
  }

  /* ── SECTION LAYOUT ── */
  section {
    border-top: 1px solid var(--border);
    padding: 80px;
    position: relative;
    max-width: 1440px;
    margin: 0 auto;
  }

  .section-header {
    display: grid;
    grid-template-columns: 60px 1fr auto;
    gap: 24px;
    align-items: start;
    margin-bottom: 64px;
  }

  .section-num {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 11px;
    color: var(--gold);
    letter-spacing: 0.1em;
    padding-top: 6px;
  }

  .section-titles h2 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(28px, 3.5vw, 44px);
    font-weight: 700;
    line-height: 1.1;
    margin-bottom: 12px;
  }

  .section-titles h2 em { font-style: italic; color: var(--gold); }

  .section-titles p {
    color: var(--text-mid);
    font-weight: 300;
    max-width: 540px;
    font-size: 14px;
  }

  .section-tag {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 9px;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--text-dim);
    border: 1px solid var(--border);
    padding: 6px 12px;
    height: fit-content;
    white-space: nowrap;
  }

  /* ── INSIGHT BLOCK ── */
  .insight-block {
    background: var(--gold-dim);
    border: 1px solid var(--border-accent);
    border-left: 3px solid var(--gold);
    padding: 24px 28px;
    margin: 32px 0;
  }

  .insight-block .insight-label {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 9px;
    letter-spacing: 0.15em;
    color: var(--gold);
    text-transform: uppercase;
    margin-bottom: 10px;
  }

  .insight-block p {
    font-size: 14px;
    color: var(--text);
    line-height: 1.75;
  }

  /* ── DATA GRID ── */
  .data-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2px;
    margin: 32px 0;
  }

  .data-cell {
    background: var(--surface);
    border: 1px solid var(--border);
    padding: 24px;
  }

  .data-cell-label {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 9px;
    letter-spacing: 0.12em;
    color: var(--text-dim);
    text-transform: uppercase;
    margin-bottom: 12px;
  }

  .data-cell-val {
    font-family: 'Playfair Display', serif;
    font-size: 32px;
    color: var(--text);
    font-weight: 700;
    margin-bottom: 4px;
  }

  .data-cell-desc {
    font-size: 12px;
    color: var(--text-dim);
    line-height: 1.6;
  }

  /* ── VISUAL CHART MOCKUPS ── */
  .chart-container {
    background: var(--surface);
    border: 1px solid var(--border);
    padding: 32px;
    margin: 32px 0;
  }

  .chart-title {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.12em;
    color: var(--text-dim);
    text-transform: uppercase;
    margin-bottom: 24px;
    display: flex;
    justify-content: space-between;
  }

  /* Bar chart */
  .bar-chart { display: flex; flex-direction: column; gap: 14px; }

  .bar-row {
    display: grid;
    grid-template-columns: 160px 1fr 60px;
    align-items: center;
    gap: 16px;
  }

  .bar-label {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 10px;
    color: var(--text-mid);
    letter-spacing: 0.05em;
    text-align: right;
  }

  .bar-track {
    background: rgba(255,255,255,0.04);
    height: 8px;
    position: relative;
    overflow: hidden;
  }

  .bar-fill {
    position: absolute;
    left: 0; top: 0; bottom: 0;
    background: var(--gold);
    opacity: 0.7;
    transform-origin: left;
    animation: barGrow 1s ease both;
  }

  @keyframes barGrow {
    from { transform: scaleX(0); }
    to { transform: scaleX(1); }
  }

  .bar-pct {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 10px;
    color: var(--gold);
  }

  /* ── FLOW DIAGRAM ── */
  .flow-diagram {
    display: flex;
    align-items: center;
    gap: 0;
    margin: 32px 0;
    overflow-x: auto;
    padding: 24px 0;
  }

  .flow-node {
    background: var(--surface);
    border: 1px solid var(--border);
    padding: 16px 20px;
    min-width: 140px;
    text-align: center;
    flex-shrink: 0;
    position: relative;
  }

  .flow-node.active {
    border-color: var(--gold);
    background: var(--gold-dim);
  }

  .flow-node-label {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 9px;
    letter-spacing: 0.1em;
    color: var(--text-dim);
    text-transform: uppercase;
    margin-bottom: 6px;
  }

  .flow-node-val {
    font-family: 'Playfair Display', serif;
    font-size: 20px;
    color: var(--text);
  }

  .flow-arrow {
    font-size: 18px;
    color: var(--text-dim);
    padding: 0 12px;
    flex-shrink: 0;
  }

  /* ── TWO-COL LAYOUT ── */
  .two-col {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 32px;
    margin: 32px 0;
  }

  .two-col-left { }
  .two-col-right { }

  /* ── STRATEGY CARDS ── */
  .strategy-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 2px;
    margin: 32px 0;
  }

  .strategy-card {
    background: var(--surface);
    border: 1px solid var(--border);
    padding: 32px;
    position: relative;
  }

  .strategy-card:hover { border-color: rgba(212,175,55,0.3); }

  .strategy-icon {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 9px;
    letter-spacing: 0.15em;
    color: var(--gold);
    text-transform: uppercase;
    margin-bottom: 16px;
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .strategy-icon::before {
    content: '';
    display: inline-block;
    width: 16px;
    height: 1px;
    background: var(--gold);
  }

  .strategy-card h3 {
    font-family: 'Playfair Display', serif;
    font-size: 22px;
    font-weight: 700;
    margin-bottom: 12px;
    line-height: 1.2;
  }

  .strategy-card p {
    font-size: 13px;
    color: var(--text-mid);
    line-height: 1.75;
    margin-bottom: 20px;
  }

  .strategy-meta {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
    margin-top: 20px;
    padding-top: 20px;
    border-top: 1px solid var(--border);
  }

  .meta-block-label {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 9px;
    color: var(--text-dim);
    letter-spacing: 0.1em;
    text-transform: uppercase;
    margin-bottom: 4px;
  }

  .meta-block-val {
    font-size: 12px;
    color: var(--text-mid);
    line-height: 1.5;
  }

  /* ── HEAT MAP visual ── */
  .heat-map {
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    gap: 4px;
    margin: 24px 0;
  }

  .heat-cell {
    aspect-ratio: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 8px;
    text-align: center;
    letter-spacing: 0.05em;
    padding: 8px;
    color: var(--text-dim);
    text-transform: uppercase;
    line-height: 1.3;
  }

  .heat-cell.high { background: rgba(212,175,55,0.35); color: var(--gold-bright); }
  .heat-cell.mid { background: rgba(212,175,55,0.12); color: var(--text-mid); }
  .heat-cell.low { background: rgba(255,255,255,0.03); }
  .heat-cell.gap { background: rgba(192,57,43,0.15); color: #e67e73; }

  /* ── TIMELINE ── */
  .timeline {
    position: relative;
    padding-left: 40px;
    margin: 32px 0;
  }

  .timeline::before {
    content: '';
    position: absolute;
    left: 12px; top: 0; bottom: 0;
    width: 1px;
    background: linear-gradient(to bottom, var(--gold), transparent);
  }

  .timeline-item {
    position: relative;
    margin-bottom: 32px;
    padding-left: 8px;
  }

  .timeline-item::before {
    content: '';
    position: absolute;
    left: -32px;
    top: 6px;
    width: 8px;
    height: 8px;
    background: var(--gold);
    border-radius: 50%;
  }

  .timeline-year {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 10px;
    color: var(--gold);
    letter-spacing: 0.1em;
    margin-bottom: 6px;
  }

  .timeline-text {
    font-size: 13px;
    color: var(--text-mid);
    line-height: 1.7;
  }

  /* ── POWER MAP ── */
  .power-map {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2px;
    margin: 24px 0;
  }

  .power-node {
    background: var(--surface);
    border: 1px solid var(--border);
    padding: 24px 20px;
    text-align: center;
  }

  .power-node.center {
    background: var(--gold-dim);
    border-color: var(--border-accent);
  }

  .power-node-title {
    font-family: 'Playfair Display', serif;
    font-size: 16px;
    font-weight: 700;
    margin-bottom: 8px;
  }

  .power-node-desc {
    font-size: 11px;
    color: var(--text-dim);
    line-height: 1.6;
  }

  /* ── UNCERTAINTY TAG ── */
  .uncertainty {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 9px;
    letter-spacing: 0.1em;
    color: #e67e73;
    text-transform: uppercase;
    border: 1px solid rgba(192,57,43,0.3);
    padding: 4px 10px;
    margin: 4px;
  }

  .certainty {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 9px;
    letter-spacing: 0.1em;
    color: var(--green);
    text-transform: uppercase;
    border: 1px solid rgba(46,204,113,0.3);
    padding: 4px 10px;
    margin: 4px;
  }

  /* ── FOOTER ── */
  footer {
    border-top: 1px solid var(--border);
    padding: 48px 80px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .footer-logo {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 12px;
    color: var(--gold);
    letter-spacing: 0.15em;
  }

  .footer-note {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 9px;
    color: var(--text-dim);
    letter-spacing: 0.1em;
    text-align: right;
    line-height: 1.8;
  }

  /* ── UTILITY ── */
  .mono {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 12px;
    color: var(--text-mid);
  }

  .gold { color: var(--gold); }
  .dim { color: var(--text-dim); }
  .body-text { font-size: 14px; color: var(--text-mid); line-height: 1.8; font-weight: 300; }

  h3 {
    font-family: 'Playfair Display', serif;
    font-size: 20px;
    font-weight: 700;
    margin-bottom: 12px;
  }

  .divider {
    width: 100%;
    height: 1px;
    background: var(--border);
    margin: 32px 0;
  }

  .list-item {
    display: flex;
    gap: 12px;
    align-items: flex-start;
    margin-bottom: 12px;
    font-size: 13px;
    color: var(--text-mid);
  }

  .list-item::before {
    content: '→';
    color: var(--gold);
    flex-shrink: 0;
    font-family: 'IBM Plex Mono', monospace;
    margin-top: 2px;
  }

  .full-border-block {
    border: 1px solid var(--border);
    padding: 28px;
    margin: 16px 0;
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* scroll animations */
  .reveal {
    opacity: 0;
    transform: translateY(24px);
    transition: opacity 0.6s ease, transform 0.6s ease;
  }
  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }

  /* section bg alternation */
  section:nth-child(even) { background: rgba(255,255,255,0.01); }

  /* ── RESPONSIVE ── */
  @media (max-width: 900px) {
    nav { padding: 0 24px; }
    .nav-links { display: none; }
    #hero { grid-template-columns: 1fr; }
    .hero-right { display: none; }
    .hero-left { padding: 60px 24px; }
    section { padding: 48px 24px; }
    .section-header { grid-template-columns: 40px 1fr; }
    .section-tag { display: none; }
    .data-grid { grid-template-columns: 1fr 1fr; }
    .strategy-grid { grid-template-columns: 1fr; }
    .two-col { grid-template-columns: 1fr; }
    .power-map { grid-template-columns: 1fr; }
    .heat-map { grid-template-columns: repeat(3, 1fr); }
    footer { flex-direction: column; gap: 24px; text-align: center; }
    .footer-note { text-align: center; }
  }
</style>
</head>
<body>

<!-- NAVIGATION -->
<nav>
  <a href="#hero" class="nav-logo">VC//BRASIL</a>
  <ul class="nav-links">
    <li><a href="#overview">Mercado</a></li>
    <li><a href="#concentration">Concentração</a></li>
    <li><a href="#flow">Fluxo de Capital</a></li>
    <li><a href="#power">Estrutura</a></li>
    <li><a href="#gaps">Gaps</a></li>
    <li><a href="#capture">Captura</a></li>
    <li><a href="#outlook">Outlook</a></li>
  </ul>
  <span class="nav-tag">Sistema de Inteligência · 2024–25</span>
</nav>

<!-- HERO -->
<div id="hero">
  <div class="hero-grid-lines"></div>
  <div class="hero-glow"></div>

  <div class="hero-left">
    <div class="hero-label">Mapa estratégico do VC no Brasil</div>
    <h1>Onde está o<br><em>poder real</em><br>no mercado.</h1>
    <p class="hero-desc">Um sistema de decisão para founders, operadores e fundos emergentes que precisam entender como o capital realmente se move — antes de agir.</p>
    <div class="hero-cta-row">
      <a href="#overview" class="btn-primary">Entrar no sistema →</a>
      <a href="#capture" class="btn-ghost">Ver estratégias de captura</a>
    </div>
  </div>

  <div class="hero-right">
    <div class="hero-stats-grid">
      <div class="stat-card">
        <div class="stat-num">~$3B</div>
        <div class="stat-label">Capital investido<br>no pico (2021)</div>
        <div class="stat-context">↘ contração significativa em 2022–23</div>
      </div>
      <div class="stat-card">
        <div class="stat-num">~50%</div>
        <div class="stat-label">Capital concentrado<br>em SP</div>
        <div class="stat-context">Com Rio e BH somando ~15%</div>
      </div>
      <div class="stat-card">
        <div class="stat-num">#1</div>
        <div class="stat-label">LatAm em volume<br>de deals VC</div>
        <div class="stat-context">Brasil lidera consistentemente</div>
      </div>
      <div class="stat-card">
        <div class="stat-num">~70%</div>
        <div class="stat-label">Deals em fintech<br>+ saúde + SaaS</div>
        <div class="stat-context">Alta concentração setorial</div>
      </div>
    </div>
  </div>
</div>

<!-- SECTION 1: MARKET OVERVIEW -->
<section id="overview">
  <div class="section-header reveal">
    <div class="section-num">01</div>
    <div class="section-titles">
      <h2>Visão Geral do <em>Mercado</em></h2>
      <p>Estrutura histórica, ciclos de crescimento e posição do Brasil no ecossistema global de venture capital.</p>
    </div>
    <span class="section-tag">Market Overview</span>
  </div>

  <div class="two-col reveal">
    <div>
      <h3>Ciclos e Estrutura</h3>
      <div class="timeline">
        <div class="timeline-item">
          <div class="timeline-year">2010–2016 · Formação</div>
          <div class="timeline-text">Surgimento dos primeiros fundos institucionais. Predominância de angels e FIPs. Capital escasso, mas ecosystem em construção. Kaszek, Monashees e Redpoint emergem como referências locais.</div>
        </div>
        <div class="timeline-item">
          <div class="timeline-year">2017–2020 · Expansão</div>
          <div class="timeline-text">Entrada de capital estrangeiro (SoftBank, Tiger). Proliferação de fintechs. Nubank, iFood e VTEX atraem rounds de escala. Valorizações começam a descolar dos fundamentos.</div>
        </div>
        <div class="timeline-item">
          <div class="timeline-year">2021 · Pico</div>
          <div class="timeline-text">Ano recorde em volume. Juros globais próximos de zero impulsionam apetite por risco. Múltiplos inflados. Rounds de série B+ com valuations de growth. Mercado superaquecido.</div>
        </div>
        <div class="timeline-item">
          <div class="timeline-year">2022–2023 · Correção</div>
          <div class="timeline-text">Alta de juros no Brasil e nos EUA. Capital estrangeiro retrai. Valuations deflacionam. Fundos adotam postura defensiva. Early-stage resiliente; growth stage contrai.</div>
        </div>
        <div class="timeline-item">
          <div class="timeline-year">2024–25 · Recuperação seletiva</div>
          <div class="timeline-text">Retorno gradual do capital. Foco em eficiência, unit economics reais, IA aplicada. Fundos mais disciplinados. Janela de oportunidade para novos entrantes posicionados corretamente.</div>
        </div>
      </div>
    </div>
    <div>
      <h3>Brasil vs LatAm vs Global</h3>
      <div class="chart-container">
        <div class="chart-title"><span>Share do volume VC na LatAm</span><span>Estimativa estrutural</span></div>
        <div class="bar-chart">
          <div class="bar-row">
            <div class="bar-label">Brasil</div>
            <div class="bar-track"><div class="bar-fill" style="width:65%; animation-delay:0.1s"></div></div>
            <div class="bar-pct">~65%</div>
          </div>
          <div class="bar-row">
            <div class="bar-label">México</div>
            <div class="bar-track"><div class="bar-fill" style="width:20%; animation-delay:0.2s"></div></div>
            <div class="bar-pct">~20%</div>
          </div>
          <div class="bar-row">
            <div class="bar-label">Colombia</div>
            <div class="bar-track"><div class="bar-fill" style="width:7%; animation-delay:0.3s"></div></div>
            <div class="bar-pct">~7%</div>
          </div>
          <div class="bar-row">
            <div class="bar-label">Demais</div>
            <div class="bar-track"><div class="bar-fill" style="width:8%; animation-delay:0.4s"></div></div>
            <div class="bar-pct">~8%</div>
          </div>
        </div>
      </div>

      <div class="insight-block">
        <div class="insight-label">→ Implicação estratégica</div>
        <p>Brasil é o mercado VC dominante na LatAm com margem consistente. Isso cria tanto oportunidades — maior volume de deals — quanto riscos de saturação em setores como fintech. Fundos entrantes precisam escolher: competir no core ou explorar adjacências.</p>
      </div>
    </div>
  </div>

  <div class="data-grid reveal">
    <div class="data-cell">
      <div class="data-cell-label">Profundidade do mercado</div>
      <div class="data-cell-val">~2%</div>
      <div class="data-cell-desc">VC como % do PIB — ainda muito abaixo de mercados maduros como EUA (~0.5% do PIB, mas com PIB 10x maior). Espaço estrutural de crescimento.</div>
    </div>
    <div class="data-cell">
      <div class="data-cell-label">Fundos ativos estimados</div>
      <div class="data-cell-val">200+</div>
      <div class="data-cell-desc">Entre funds institucionais, micro-VCs, CVCs e family offices com postura VC. Metade desse número opera de forma consistente.</div>
    </div>
    <div class="data-cell">
      <div class="data-cell-label">Unicórnios ativos</div>
      <div class="data-cell-val">~15</div>
      <div class="data-cell-desc">Número oscila com ciclos de valuation. Nubank, Totvs, iFood, VTEX, QuintoAndar, Gympass entre os mais sólidos em fundamentos reais.</div>
    </div>
  </div>
</section>

<!-- SECTION 2: MARKET SHARE -->
<section id="concentration">
  <div class="section-header reveal">
    <div class="section-num">02</div>
    <div class="section-titles">
      <h2>Distribuição do <em>Market-Share</em></h2>
      <p>Onde o capital está concentrado, quem controla o deal flow e onde existe fragmentação explorável.</p>
    </div>
    <span class="section-tag">Power Map</span>
  </div>

  <div class="two-col reveal">
    <div>
      <h3>Concentração por Fundo</h3>
      <div class="chart-container">
        <div class="chart-title"><span>Peso relativo por tipo de fundo</span></div>
        <div class="bar-chart">
          <div class="bar-row">
            <div class="bar-label">Top 5 fundos locais</div>
            <div class="bar-track"><div class="bar-fill" style="width:45%; animation-delay:0.1s"></div></div>
            <div class="bar-pct">~45%</div>
          </div>
          <div class="bar-row">
            <div class="bar-label">Fundos globais</div>
            <div class="bar-track"><div class="bar-fill" style="width:25%; animation-delay:0.2s"></div></div>
            <div class="bar-pct">~25%</div>
          </div>
          <div class="bar-row">
            <div class="bar-label">CVCs</div>
            <div class="bar-track"><div class="bar-fill" style="width:15%; animation-delay:0.3s"></div></div>
            <div class="bar-pct">~15%</div>
          </div>
          <div class="bar-row">
            <div class="bar-label">Micro-VCs + angels</div>
            <div class="bar-track"><div class="bar-fill" style="width:10%; animation-delay:0.4s"></div></div>
            <div class="bar-pct">~10%</div>
          </div>
          <div class="bar-row">
            <div class="bar-label">Family offices</div>
            <div class="bar-track"><div class="bar-fill" style="width:5%; animation-delay:0.5s"></div></div>
            <div class="bar-pct">~5%</div>
          </div>
        </div>
      </div>
    </div>
    <div>
      <h3>Concentração por Estágio</h3>
      <div class="chart-container">
        <div class="chart-title"><span>Volume de capital por estágio</span></div>
        <div class="bar-chart">
          <div class="bar-row">
            <div class="bar-label">Série A+</div>
            <div class="bar-track"><div class="bar-fill" style="width:55%; animation-delay:0.1s"></div></div>
            <div class="bar-pct">~55%</div>
          </div>
          <div class="bar-row">
            <div class="bar-label">Seed</div>
            <div class="bar-track"><div class="bar-fill" style="width:25%; animation-delay:0.2s"></div></div>
            <div class="bar-pct">~25%</div>
          </div>
          <div class="bar-row">
            <div class="bar-label">Pre-seed / angel</div>
            <div class="bar-track"><div class="bar-fill" style="width:12%; animation-delay:0.3s"></div></div>
            <div class="bar-pct">~12%</div>
          </div>
          <div class="bar-row">
            <div class="bar-label">Late-stage / growth</div>
            <div class="bar-track"><div class="bar-fill" style="width:8%; animation-delay:0.4s"></div></div>
            <div class="bar-pct">~8%</div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <h3 class="reveal" style="margin: 40px 0 20px">Mapa de Calor Setorial</h3>
  <p class="body-text reveal" style="margin-bottom: 20px">Concentração de capital e atenção dos fundos por setor. <span class="gold">Dourado = alta concentração.</span> <span style="color:#e67e73">Vermelho = gap estrutural.</span></p>

  <div class="heat-map reveal">
    <div class="heat-cell high">Fintech</div>
    <div class="heat-cell high">SaaS B2B</div>
    <div class="heat-cell mid">Healthtech</div>
    <div class="heat-cell mid">Edtech</div>
    <div class="heat-cell low">Proptech</div>
    <div class="heat-cell gap">Manufatura</div>
    <div class="heat-cell mid">Agritech</div>
    <div class="heat-cell gap">Logística 2ª</div>
    <div class="heat-cell high">IA Aplicada</div>
    <div class="heat-cell low">Climatech</div>
    <div class="heat-cell gap">Hardware</div>
    <div class="heat-cell gap">Deep Tech</div>
    <div class="heat-cell mid">E-commerce</div>
    <div class="heat-cell gap">Norte/NE</div>
    <div class="heat-cell low">Legaltech</div>
    <div class="heat-cell gap">Biotech</div>
    <div class="heat-cell mid">HR Tech</div>
    <div class="heat-cell low">Segurança</div>
  </div>

  <div class="insight-block reveal">
    <div class="insight-label">→ Implicação estratégica</div>
    <p>A concentração extrema em fintech criou saturação competitiva — fundos lutam pelos mesmos 30 founders. Setores como deep tech, biotech e manufatura têm fundadores qualificados com acesso limitado a capital especializado. Esse gap não é acidente: exige expertise que a maioria dos fundos generalistas não tem. Quem desenvolve essa tese antes da janela fechar, captura market-share com menor concorrência.</p>
  </div>
</section>

<!-- SECTION 3: CAPITAL FLOW -->
<section id="flow">
  <div class="section-header reveal">
    <div class="section-num">03</div>
    <div class="section-titles">
      <h2>Dinâmica de <em>Fluxo de Capital</em></h2>
      <p>Para onde o dinheiro está indo agora, e o que isso revela sobre a estrutura real do mercado.</p>
    </div>
    <span class="section-tag">Capital Dynamics</span>
  </div>

  <div class="two-col reveal">
    <div>
      <h3>Shift de Paradigma: 2021 → Hoje</h3>
      <div class="full-border-block">
        <div class="data-cell-label">2021 — Crescimento a qualquer custo</div>
        <div class="list-item">Múltiplos de ARR 40–80x em rounds seed</div>
        <div class="list-item">Burn rate elevado tolerado com CAC/LTV desfavorável</div>
        <div class="list-item">Capital estrangeiro abundante e acrítico</div>
        <div class="list-item">Founders com tração mínima levantando rounds seed de $3M+</div>
      </div>
      <div class="full-border-block" style="border-color: rgba(212,175,55,0.3);">
        <div class="data-cell-label" style="color: var(--gold);">2024–25 — Eficiência como filtro</div>
        <div class="list-item">Unit economics real como critério primário</div>
        <div class="list-item">Runway de 24+ meses como sinal de qualidade</div>
        <div class="list-item">Capital estrangeiro mais seletivo e lento</div>
        <div class="list-item">Founders com revenue real + margem saudável têm vantagem</div>
      </div>
    </div>
    <div>
      <h3>Capital Externo vs Local</h3>
      <div class="chart-container">
        <div class="chart-title"><span>Composição do capital por origem</span><span>Estimativa por ciclo</span></div>
        <div style="margin-bottom: 24px;">
          <div class="data-cell-label">Ciclo 2019–21 (boom)</div>
          <div class="bar-chart">
            <div class="bar-row">
              <div class="bar-label">Capital externo</div>
              <div class="bar-track"><div class="bar-fill" style="width:60%; animation-delay:0.1s"></div></div>
              <div class="bar-pct">~60%</div>
            </div>
            <div class="bar-row">
              <div class="bar-label">Capital local</div>
              <div class="bar-track"><div class="bar-fill" style="width:40%; animation-delay:0.2s; opacity:0.4"></div></div>
              <div class="bar-pct" style="color:var(--text-dim)">~40%</div>
            </div>
          </div>
        </div>
        <div>
          <div class="data-cell-label">Ciclo 2023–25 (recuperação)</div>
          <div class="bar-chart">
            <div class="bar-row">
              <div class="bar-label">Capital externo</div>
              <div class="bar-track"><div class="bar-fill" style="width:35%; animation-delay:0.3s"></div></div>
              <div class="bar-pct">~35%</div>
            </div>
            <div class="bar-row">
              <div class="bar-label">Capital local</div>
              <div class="bar-track"><div class="bar-fill" style="width:65%; animation-delay:0.4s; opacity:0.4"></div></div>
              <div class="bar-pct" style="color:var(--text-dim)">~65%</div>
            </div>
          </div>
        </div>
      </div>
      <div class="insight-block">
        <div class="insight-label">→ Implicação estratégica</div>
        <p>A retração do capital estrangeiro não eliminou o mercado — concentrou poder nos fundos locais. Quem tem relacionamento com LP local e entende a dinâmica regulatória brasileira está em posição superior. Fundos emergentes têm janela para capturar deals que os grandes fundos estrangeiros não estão alcançando.</p>
      </div>
    </div>
  </div>

  <h3 class="reveal" style="margin: 40px 0 20px">Fluxo de um Deal no Mercado Atual</h3>
  <div class="flow-diagram reveal">
    <div class="flow-node">
      <div class="flow-node-label">Origem</div>
      <div class="flow-node-val">Founder</div>
    </div>
    <div class="flow-arrow">→</div>
    <div class="flow-node active">
      <div class="flow-node-label">Acesso ao Capital</div>
      <div class="flow-node-val">Network</div>
    </div>
    <div class="flow-arrow">→</div>
    <div class="flow-node">
      <div class="flow-node-label">Filtro</div>
      <div class="flow-node-val">Reputação</div>
    </div>
    <div class="flow-arrow">→</div>
    <div class="flow-node">
      <div class="flow-node-label">Qualificação</div>
      <div class="flow-node-val">Tese do Fundo</div>
    </div>
    <div class="flow-arrow">→</div>
    <div class="flow-node">
      <div class="flow-node-label">Decisão</div>
      <div class="flow-node-val">Deal / Pass</div>
    </div>
    <div class="flow-arrow">→</div>
    <div class="flow-node active">
      <div class="flow-node-label">Dinâmica</div>
      <div class="flow-node-val">Follow-on</div>
    </div>
  </div>
  <p class="body-text reveal" style="margin-top: 12px; font-size: 12px;">O nó crítico é o acesso: 70–80% dos deals que chegam aos fundos top-tier vêm de network direto, não de cold outreach.</p>
</section>

<!-- SECTION 4: POWER STRUCTURE -->
<section id="power">
  <div class="section-header reveal">
    <div class="section-num">04</div>
    <div class="section-titles">
      <h2>Estrutura de <em>Poder e Acesso</em></h2>
      <p>Como os deals realmente acontecem — e por que alguns fundos veem as melhores oportunidades primeiro.</p>
    </div>
    <span class="section-tag">Deal Access</span>
  </div>

  <div class="power-map reveal">
    <div class="power-node">
      <div class="power-node-title">Reputação de Portfolio</div>
      <div class="power-node-desc">Fundos com exits conhecidos ou portfólio de prestígio atraem founders que buscam o "sinal" que o investidor emite. Reputação é ativo composto.</div>
    </div>
    <div class="power-node center">
      <div class="power-node-title" style="color:var(--gold)">Deal Flow de Qualidade</div>
      <div class="power-node-desc">O objetivo real de todo fundo. Controlado por quem domina os três nós ao redor.</div>
    </div>
    <div class="power-node">
      <div class="power-node-title">Network de Founders</div>
      <div class="power-node-desc">Founders de portfólio que recomendam outros founders. Loop auto-reforçador. Primeiro check define quem entra no ecossistema.</div>
    </div>
    <div class="power-node">
      <div class="power-node-title">Aceleradoras e Hubs</div>
      <div class="power-node-desc">YC alumni, Endeavor, Cubo, Inovabra. Quem atua próximo dessas estruturas tem visibilidade antecipada de deals pré-qualificados.</div>
    </div>
    <div class="power-node">
      <div class="power-node-title">Presença de Conteúdo</div>
      <div class="power-node-desc">GPs que publicam teses, análises e insights atraem inbound de founders qualificados. Distribuição substitui parte do network frio.</div>
    </div>
    <div class="power-node">
      <div class="power-node-title">Capital Estrangeiro como Sinal</div>
      <div class="power-node-desc">Fundos co-investindo com Sequoia, a16z ou Softbank ganham credibilidade local mesmo sem track record próprio extenso.</div>
    </div>
  </div>

  <div class="insight-block reveal">
    <div class="insight-label">→ Implicação estratégica</div>
    <p>A barreira de entrada real não é capital — é acesso a deal flow qualificado. Fundos estabelecidos têm loops de reputação que se auto-reforçam. Para fundos emergentes, a estratégia não é competir diretamente nesses loops: é criar canais alternativos de deal flow através de conteúdo, especialização setorial ou presença em mercados geográficos sub-servidos.</p>
  </div>

  <div class="two-col reveal">
    <div>
      <h3>Por que alguns fundos veem os melhores deals primeiro</h3>
      <div class="list-item">Investiram em founders que se tornaram referências — e esses founders indicam os próximos</div>
      <div class="list-item">Têm GPs com histórico como founders — credibilidade de par</div>
      <div class="list-item">Participam de eventos fechados onde deals são discutidos informalmente</div>
      <div class="list-item">Constroem reputação de founders-friendly — velocidade de decisão, sem micro-gestão</div>
      <div class="list-item">Publicam perspectivas de investimento que funcionam como filtro e ímã</div>
    </div>
    <div>
      <h3>Barreiras de Entrada não Declaradas</h3>
      <div class="full-border-block" style="border-color: rgba(192,57,43,0.3);">
        <div class="data-cell-label" style="color: #e67e73">Barriers estruturais</div>
        <div class="list-item">Founders de alto potencial evitam fundos sem track record publicamente verificável</div>
        <div class="list-item">Syndicatos e co-investimentos favorecem fundos com relacionamento pré-existente</div>
        <div class="list-item">LPs institucionais preferem fundos com histórico de 2+ fundos anteriores</div>
        <div class="list-item">Eventos de deal sourcing muitas vezes são invite-only ou por indicação</div>
      </div>
    </div>
  </div>
</section>

<!-- SECTION 5: GAPS -->
<section id="gaps">
  <div class="section-header reveal">
    <div class="section-num">05</div>
    <div class="section-titles">
      <h2>Ineficiências e <em>Gaps</em></h2>
      <p>Onde o capital está mal alocado, quais founders estão sub-servidos e onde as blind spots geográficas criam assimetria.</p>
    </div>
    <span class="section-tag">Market Gaps</span>
  </div>

  <div class="strategy-grid reveal">
    <div class="strategy-card">
      <div class="strategy-icon">Gap 01</div>
      <h3>Founders fora do eixo SP–RJ</h3>
      <p>O capital VC brasileiro é geograficamente concentrado de forma desproporcional ao potencial real. Norte, Nordeste e Centro-Oeste têm ecossistemas embrionários com founders qualificados e valorizações estruturalmente mais baixas.</p>
      <div class="strategy-meta">
        <div>
          <div class="meta-block-label">Tipo de gap</div>
          <div class="meta-block-val">Geográfico + Acesso</div>
        </div>
        <div>
          <div class="meta-block-label">Nível de certeza</div>
          <div class="meta-block-val">Alto — estrutural</div>
        </div>
      </div>
    </div>
    <div class="strategy-card">
      <div class="strategy-icon">Gap 02</div>
      <h3>Deep Tech e Ciência Aplicada</h3>
      <p>Biotecnologia, materiais avançados, hardware — setores com barreiras técnicas reais têm capital insuficiente porque exigem expertise que fundos generalistas não têm. Há pesquisa universitária de qualidade sem ponte para o mercado.</p>
      <div class="strategy-meta">
        <div>
          <div class="meta-block-label">Tipo de gap</div>
          <div class="meta-block-val">Expertise + Paciência</div>
        </div>
        <div>
          <div class="meta-block-label">Nível de certeza</div>
          <div class="meta-block-val">Alto — crônico</div>
        </div>
      </div>
    </div>
    <div class="strategy-card">
      <div class="strategy-icon">Gap 03</div>
      <h3>B2B para setores "tradicionais"</h3>
      <p>Agro-industrial, construção, logística de segundo e terceiro tier, manufatura — têm digitalização em estágio inicial e demanda real não coberta. Founders com tração nesses setores frequentemente não sabem como acessar VC.</p>
      <div class="strategy-meta">
        <div>
          <div class="meta-block-label">Tipo de gap</div>
          <div class="meta-block-val">Distribuição + Tese</div>
        </div>
        <div>
          <div class="meta-block-label">Nível de certeza</div>
          <div class="meta-block-val">Médio — depende de setor</div>
        </div>
      </div>
    </div>
    <div class="strategy-card">
      <div class="strategy-icon">Gap 04</div>
      <h3>Pre-seed institucional escasso</h3>
      <p>Há poucos fundos com processo disciplinado e tese clara operando em pre-seed. O espaço é dominado por angels desorganizados ou aceleradoras com equity dilutivo. Founders nesse estágio têm acesso ruim a capital inteligente.</p>
      <div class="strategy-meta">
        <div>
          <div class="meta-block-label">Tipo de gap</div>
          <div class="meta-block-val">Estágio + Estrutura</div>
        </div>
        <div>
          <div class="meta-block-label">Nível de certeza</div>
          <div class="meta-block-val">Alto — visível</div>
        </div>
      </div>
    </div>
  </div>

  <div class="insight-block reveal">
    <div class="insight-label">→ Advertência estratégica</div>
    <p>Gaps são reais, mas nem todo gap é oportunidade. Alguns setores estão sub-capitalizados por razões estruturais válidas: ciclos longos, exits escassos, dificuldade de precificação. O filtro correto não é "onde há menos capital" — mas "onde há menos capital dado o tamanho real da oportunidade e os exits possíveis."</p>
  </div>
</section>

<!-- SECTION 6: CAPTURE STRATEGIES -->
<section id="capture">
  <div class="section-header reveal">
    <div class="section-num">06</div>
    <div class="section-titles">
      <h2>Captura de <em>Market-Share</em></h2>
      <p>Estratégias estruturais para founders, operadores e fundos emergentes que querem capturar posição no mercado como ele realmente funciona.</p>
    </div>
    <span class="section-tag">Strategic Plays</span>
  </div>

  <!-- A: Entry -->
  <h3 class="reveal" style="margin-bottom: 8px">A · Estratégias de Entrada</h3>
  <p class="body-text reveal" style="margin-bottom: 24px">Para fundos emergentes ou novos entrantes que precisam criar posição sem as vantagens dos players estabelecidos.</p>

  <div class="strategy-grid reveal">
    <div class="strategy-card">
      <div class="strategy-icon">Entrada A1</div>
      <h3>Tese de Nicho com Profundidade Real</h3>
      <p>Em vez de competir como generalista, construir expertise verticalmente profunda em um setor onde o conhecimento do GP é vantagem operacional real — não só branding.</p>
      <div class="strategy-meta">
        <div>
          <div class="meta-block-label">Quando funciona</div>
          <div class="meta-block-val">GP com background operacional no setor. Acesso a deal flow específico já existe.</div>
        </div>
        <div>
          <div class="meta-block-label">Quando falha</div>
          <div class="meta-block-val">Nicho muito pequeno para construir portfolio diversificado. Exits históricos escassos no setor.</div>
        </div>
      </div>
    </div>
    <div class="strategy-card">
      <div class="strategy-icon">Entrada A2</div>
      <h3>Arbitragem Geográfica</h3>
      <p>Operar em mercados onde a competição por deals é menor — Nordeste, Norte, interior de SP e MG. Valuations mais baixos, founders com menos opções de capital, presença local como diferencial.</p>
      <div class="strategy-meta">
        <div>
          <div class="meta-block-label">Quando funciona</div>
          <div class="meta-block-val">GP fisicamente presente na região. Tese compatible com o tecido econômico local.</div>
        </div>
        <div>
          <div class="meta-block-label">Quando falha</div>
          <div class="meta-block-val">Ecossistema local não tem massa crítica de founders tech. Exits dependem de compradores nacionais ausentes.</div>
        </div>
      </div>
    </div>
  </div>

  <!-- B: Asymmetric -->
  <h3 class="reveal" style="margin: 48px 0 8px">B · Vantagens Assimétricas</h3>
  <p class="body-text reveal" style="margin-bottom: 24px">Canais alternativos de deal flow que fundos estabelecidos não conseguem replicar facilmente.</p>

  <div class="strategy-grid reveal">
    <div class="strategy-card">
      <div class="strategy-icon">Assimetria B1</div>
      <h3>Conteúdo como Deal Magnet</h3>
      <p>GPs que publicam análises de mercado, teses de investimento e frameworks operacionais constroem audiência de founders qualificados. Inbound substitui cold outreach. Custo de deal sourcing cai estruturalmente.</p>
      <div class="strategy-meta">
        <div>
          <div class="meta-block-label">Condição necessária</div>
          <div class="meta-block-val">Qualidade real de conteúdo. Consistência de publicação mínima 12 meses.</div>
        </div>
        <div>
          <div class="meta-block-label">Timeline realista</div>
          <div class="meta-block-val">18–36 meses para deal flow inbound consistente.</div>
        </div>
      </div>
    </div>
    <div class="strategy-card">
      <div class="strategy-icon">Assimetria B2</div>
      <h3>Comunidade como Infraestrutura</h3>
      <p>Construir ou ancorar comunidades de founders em setores específicos cria visibilidade antecipada em deals pré-valuação. O custo é tempo e consistência — não capital.</p>
      <div class="strategy-meta">
        <div>
          <div class="meta-block-label">Condição necessária</div>
          <div class="meta-block-val">Capacidade de criar valor real para membros antes de extrair deal flow.</div>
        </div>
        <div>
          <div class="meta-block-label">Timeline realista</div>
          <div class="meta-block-val">12–24 meses para comunidade com densidade suficiente.</div>
        </div>
      </div>
    </div>
  </div>

  <!-- C: Timing -->
  <h3 class="reveal" style="margin: 48px 0 8px">C · Estratégias de Timing</h3>
  <p class="body-text reveal" style="margin-bottom: 24px">Posicionamento no ciclo de mercado como vantagem competitiva.</p>

  <div class="strategy-grid reveal">
    <div class="strategy-card">
      <div class="strategy-icon">Timing C1</div>
      <h3>Investimento Anti-Cíclico</h3>
      <p>Momentos de contração de mercado criam deals com valuations normalizados e founders mais comprometidos com fundamentos. Fundos com dry powder em ciclos de baixa têm vantagem de precificação real.</p>
      <div class="strategy-meta">
        <div>
          <div class="meta-block-label">Condição necessária</div>
          <div class="meta-block-val">LPs com horizonte longo. Disciplina para não perseguir deals no pico.</div>
        </div>
        <div>
          <div class="meta-block-label">Risco</div>
          <div class="meta-block-val">Ciclos de correção podem ser mais longos que o previsto. Fundos com safra 2022 ainda digerindo portfolio.</div>
        </div>
      </div>
    </div>
    <div class="strategy-card">
      <div class="strategy-icon">Timing C2</div>
      <h3>Posição Early-Stage como Opção</h3>
      <p>Pre-seed e seed em fundadores com tese setorial clara têm retorno assimétrico. A maioria vai a zero — mas os que funcionam compensam com múltiplos que rounds posteriores não permitem capturar.</p>
      <div class="strategy-meta">
        <div>
          <div class="meta-block-label">Condição necessária</div>
          <div class="meta-block-val">Portfolio size adequado (20+ deals). Processo de seleção disciplinado e replicável.</div>
        </div>
        <div>
          <div class="meta-block-label">Risco</div>
          <div class="meta-block-val">Concentração em poucos deals early destrói o modelo. Diversificação é condição, não opção.</div>
        </div>
      </div>
    </div>
  </div>

  <!-- D: Structural -->
  <h3 class="reveal" style="margin: 48px 0 8px">D · Jogadas Estruturais</h3>
  <p class="body-text reveal" style="margin-bottom: 24px">Modelos híbridos e estruturas alternativas ao VC tradicional.</p>

  <div class="strategy-grid reveal">
    <div class="strategy-card">
      <div class="strategy-icon">Estrutural D1</div>
      <h3>Venture Studio com Tese Setorial</h3>
      <p>Em vez de investir em founders existentes, co-fundar empresas com profissionais técnicos de setores específicos. Controle maior, dependência menor de deal flow externo, valuation de entrada mais baixo.</p>
      <div class="strategy-meta">
        <div>
          <div class="meta-block-label">Quando funciona</div>
          <div class="meta-block-val">GP com capacidade operacional real. Acesso a talentos técnicos de domínio específico.</div>
        </div>
        <div>
          <div class="meta-block-label">Quando falha</div>
          <div class="meta-block-val">Studio sem founder de qualidade. Tentativa de operar 5+ empresas simultâneas com equipe pequena.</div>
        </div>
      </div>
    </div>
    <div class="strategy-card">
      <div class="strategy-icon">Estrutural D2</div>
      <h3>VC + Serviços como Acelerador</h3>
      <p>Fundos que oferecem serviços operacionais reais (go-to-market, finanças, tech) criam valor diferencial que justifica termos melhores e atrai founders que precisam de mais que capital.</p>
      <div class="strategy-meta">
        <div>
          <div class="meta-block-label">Quando funciona</div>
          <div class="meta-block-val">Equipe com experiência operacional real. Serviços escaláveis sem destruir economics do fundo.</div>
        </div>
        <div>
          <div class="meta-block-label">Quando falha</div>
          <div class="meta-block-val">Serviços consomem GP time sem retorno proporcional. Conflito de interesse em portfolio.</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- SECTION 7: PATTERNS -->
<section id="patterns">
  <div class="section-header reveal">
    <div class="section-num">07</div>
    <div class="section-titles">
      <h2>Padrões de <em>Fundos que Funcionam</em></h2>
      <p>Estrutura, não storytelling. O que distingue fundos bem-sucedidos no Brasil — independente da narrativa pública.</p>
    </div>
    <span class="section-tag">Case Patterns</span>
  </div>

  <div class="two-col reveal">
    <div>
      <h3>Padrões estruturais observáveis</h3>
      <div class="timeline">
        <div class="timeline-item">
          <div class="timeline-year">Padrão 01 · Tese clara antes do capital</div>
          <div class="timeline-text">Fundos que definiram tese de investimento específica antes de levantar LP capital tiveram deal flow mais qualificado. Kaszek, Monashees e Redpoint entraram com tese setorial/geográfica antes de escalar.</div>
        </div>
        <div class="timeline-item">
          <div class="timeline-year">Padrão 02 · GP-founder alignment</div>
          <div class="timeline-text">GPs com background operacional como founders — não apenas finanças — têm acesso diferenciado a deals pré-competitivos. Founders confiam mais em pares do que em analistas financeiros.</div>
        </div>
        <div class="timeline-item">
          <div class="timeline-year">Padrão 03 · Portfolio que vira deal sourcing</div>
          <div class="timeline-text">Fundos que constroem rede de founders de portfólio criam multiplicador de deal flow. Cada empresa do portfolio é canal de indicação para as próximas.</div>
        </div>
        <div class="timeline-item">
          <div class="timeline-year">Padrão 04 · Disciplina em valuation</div>
          <div class="timeline-text">Fundos que mantiveram disciplina de pricing no pico de 2021 saíram melhor da correção de 2022–23. Fundos que perseguiram deals com múltiplos inflados ainda carregam portfolio problemático.</div>
        </div>
      </div>
    </div>
    <div>
      <h3>O que diferencia em termos operacionais</h3>
      <div class="data-grid" style="grid-template-columns: 1fr; gap: 2px;">
        <div class="data-cell">
          <div class="data-cell-label">Velocidade de decisão</div>
          <div class="data-cell-desc">Fundos top-tier decidem em semanas, não meses. Founders de alta qualidade não esperam processos longos. A lentidão é sinal negativo.</div>
        </div>
        <div class="data-cell">
          <div class="data-cell-label">Suporte pós-investimento</div>
          <div class="data-cell-desc">Ajuda real em contratações estratégicas, próximo round e clientes. Não coaching genérico. Founders validam isso publicamente ou em privado.</div>
        </div>
        <div class="data-cell">
          <div class="data-cell-label">Transparência de tese</div>
          <div class="data-cell-desc">Fundos que publicam o que investem e por quê recebem deal flow pré-filtrado. Founders que chegam já entendem o fit — menos tempo desperdiçado para ambos.</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- SECTION 8: OUTLOOK -->
<section id="outlook">
  <div class="section-header reveal">
    <div class="section-num">08</div>
    <div class="section-titles">
      <h2>Outlook <em>Realista</em></h2>
      <p>O que é provável, o que é incerto e como navegar as variáveis que mais impactam o mercado nos próximos 24–36 meses.</p>
    </div>
    <span class="section-tag">Forward View</span>
  </div>

  <div class="two-col reveal">
    <div>
      <h3>Alta probabilidade</h3>
      <div class="full-border-block">
        <div class="certainty">Alta certeza</div>
        <div class="list-item" style="margin-top: 16px">IA aplicada continuará recebendo capital desproporcional — seja como tese direta ou como camada em qualquer vertical</div>
        <div class="list-item">Fundos estrangeiros continuarão seletivos — capital local manterá posição dominante por 2–3 anos</div>
        <div class="list-item">Eficiência de capital como critério primário de avaliação — burn múltiplo e payback period como filtros básicos</div>
        <div class="list-item">Consolidação de fundos — menos fundos novos levantando, os existentes absorvendo mais capital</div>
      </div>
    </div>
    <div>
      <h3>Alta incerteza</h3>
      <div class="full-border-block" style="border-color: rgba(192,57,43,0.3);">
        <div class="uncertainty">Incerteza real</div>
        <div class="list-item" style="margin-top: 16px">Ritmo de recuperação do mercado: pode ser 2025, pode ser 2027. Depende de juros globais e câmbio</div>
        <div class="list-item">Impacto regulatório: Banco Central, CVM e mudanças em marco legal de startups podem criar ou destruir setores inteiros</div>
        <div class="list-item">Janela de exits: mercado de IPO brasileiro historicamente limitado. M&A depende de compradores estratégicos escassos</div>
        <div class="list-item">IA como disruptor de setores inteiros: edtech, legaltech, healthtech podem ter seus modelos reconfigurados antes da tese de investimento maturar</div>
      </div>
    </div>
  </div>

  <div class="insight-block reveal">
    <div class="insight-label">→ Síntese estratégica final</div>
    <p>O mercado VC brasileiro está em recuperação seletiva após ciclo de correção. A janela 2024–26 oferece deals com valuations normalizados, menor competição por founders de nicho, e capital local em posição dominante. Os fundos que capturarão market-share real nos próximos 5 anos serão os que combinam: tese setorial específica + deal flow alternativo (conteúdo ou comunidade) + disciplina de precificação + GPs com credibilidade operacional. Não é uma fórmula — é um conjunto de condições. Qualquer uma pode falhar individualmente.</p>
  </div>

  <div class="data-grid reveal">
    <div class="data-cell">
      <div class="data-cell-label">Janela atual</div>
      <div class="data-cell-val" style="font-size: 24px; color: var(--green)">Aberta</div>
      <div class="data-cell-desc">Para fundos pre-seed/seed com tese clara e deal flow alternativo. Competição mais baixa que em 2020–21.</div>
    </div>
    <div class="data-cell">
      <div class="data-cell-label">Risco de timing</div>
      <div class="data-cell-val" style="font-size: 24px; color: var(--gold)">Médio</div>
      <div class="data-cell-desc">Recuperação pode ser mais lenta que esperada. Fundos levantados agora precisam de paciência de LPs.</div>
    </div>
    <div class="data-cell">
      <div class="data-cell-label">Competição nos nichos</div>
      <div class="data-cell-val" style="font-size: 24px; color: var(--green)">Baixa</div>
      <div class="data-cell-desc">Deep tech, geo-arbitrage e B2B tradicional ainda têm poucos fundos com tese séria e equipe adequada.</div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-logo">VC // BRASIL</div>
  <div class="footer-note">
    Sistema de inteligência de mercado · Uso estratégico<br>
    Dados estruturais estimados — verificar fontes primárias antes de decisões<br>
    ABVCAP · LAVCA · Crunchbase · Análise estrutural interna
  </div>
</footer>

<script>
  // Scroll reveal
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.classList.add('visible');
      }
    });
  }, { threshold: 0.08 });

  document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

  // Active nav link
  const sections = document.querySelectorAll('section[id]');
  const navLinks = document.querySelectorAll('.nav-links a');

  window.addEventListener('scroll', () => {
    let current = '';
    sections.forEach(s => {
      if (window.scrollY >= s.offsetTop - 100) current = s.id;
    });
    navLinks.forEach(a => {
      a.style.color = a.getAttribute('href') === '#' + current
        ? 'var(--gold)'
        : '';
    });
  });
</script>
</body>
</html>
