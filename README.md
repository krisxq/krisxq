<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;700;800&family=JetBrains+Mono:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #080c12;
    --bg2: #0d1520;
    --surface: #111927;
    --border: rgba(99,180,255,0.12);
    --accent: #63b4ff;
    --accent2: #a78bfa;
    --accent3: #34d399;
    --text: #e8f4ff;
    --muted: #6b8cad;
    --glow: rgba(99,180,255,0.15);
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'JetBrains Mono', monospace;
    min-height: 100vh;
    overflow-x: hidden;
    position: relative;
  }

  /* ── Grid Background ── */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(99,180,255,0.04) 1px, transparent 1px),
      linear-gradient(90deg, rgba(99,180,255,0.04) 1px, transparent 1px);
    background-size: 48px 48px;
    pointer-events: none;
    z-index: 0;
  }

  /* ── Floating orbs ── */
  .orb {
    position: fixed;
    border-radius: 50%;
    filter: blur(80px);
    pointer-events: none;
    z-index: 0;
    animation: drift 14s ease-in-out infinite alternate;
  }
  .orb1 { width: 420px; height: 420px; background: rgba(99,180,255,0.08); top: -100px; left: -100px; animation-delay: 0s; }
  .orb2 { width: 320px; height: 320px; background: rgba(167,139,250,0.07); bottom: 10%; right: -80px; animation-delay: -5s; }
  .orb3 { width: 260px; height: 260px; background: rgba(52,211,153,0.06); top: 50%; left: 50%; animation-delay: -9s; }

  @keyframes drift {
    from { transform: translate(0, 0) scale(1); }
    to { transform: translate(30px, 20px) scale(1.05); }
  }

  /* ── Wrapper ── */
  .wrapper {
    position: relative;
    z-index: 1;
    max-width: 780px;
    margin: 0 auto;
    padding: 60px 32px 80px;
  }

  /* ── Hero ── */
  .hero {
    text-align: center;
    margin-bottom: 64px;
    opacity: 0;
    animation: fadeUp 0.9s cubic-bezier(0.22,1,0.36,1) 0.1s forwards;
  }

  .hero-badge {
    display: inline-block;
    font-size: 11px;
    letter-spacing: 0.18em;
    color: var(--accent);
    border: 1px solid rgba(99,180,255,0.3);
    padding: 5px 14px;
    border-radius: 100px;
    margin-bottom: 28px;
    text-transform: uppercase;
    background: rgba(99,180,255,0.05);
  }

  .hero-name {
    font-family: 'Syne', sans-serif;
    font-size: clamp(42px, 8vw, 72px);
    font-weight: 800;
    line-height: 1.0;
    letter-spacing: -0.03em;
    background: linear-gradient(135deg, #e8f4ff 0%, #63b4ff 50%, #a78bfa 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    margin-bottom: 16px;
  }

  .hero-snowflake {
    display: inline-block;
    -webkit-text-fill-color: initial;
    color: #93c5fd;
    animation: spin-slow 12s linear infinite;
    margin-left: 8px;
    font-size: 0.7em;
    vertical-align: middle;
  }

  @keyframes spin-slow {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }

  /* ── Typewriter role ── */
  .hero-role {
    font-size: 15px;
    color: var(--muted);
    letter-spacing: 0.05em;
    margin-bottom: 28px;
    height: 24px;
  }

  .typewriter {
    color: var(--accent3);
    border-right: 2px solid var(--accent3);
    padding-right: 3px;
    animation: blink 0.8s step-end infinite;
    white-space: nowrap;
    overflow: hidden;
  }

  @keyframes blink { 50% { border-color: transparent; } }

  .hero-tagline {
    font-size: 13px;
    color: var(--muted);
    max-width: 460px;
    margin: 0 auto;
    line-height: 1.8;
  }

  /* ── Divider ── */
  .divider {
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--border), rgba(167,139,250,0.15), var(--border), transparent);
    margin: 48px 0;
  }

  /* ── Section ── */
  .section {
    margin-bottom: 52px;
    opacity: 0;
    animation: fadeUp 0.8s cubic-bezier(0.22,1,0.36,1) forwards;
  }
  .section:nth-child(2) { animation-delay: 0.3s; }
  .section:nth-child(3) { animation-delay: 0.5s; }
  .section:nth-child(4) { animation-delay: 0.7s; }
  .section:nth-child(5) { animation-delay: 0.9s; }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(28px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .section-label {
    font-size: 10px;
    letter-spacing: 0.22em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .section-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  /* ── Education card ── */
  .edu-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 22px 26px;
    display: flex;
    align-items: flex-start;
    gap: 18px;
    transition: border-color 0.3s, box-shadow 0.3s;
  }

  .edu-card:hover {
    border-color: rgba(99,180,255,0.3);
    box-shadow: 0 0 28px rgba(99,180,255,0.07);
  }

  .edu-icon {
    width: 44px;
    height: 44px;
    border-radius: 10px;
    background: rgba(99,180,255,0.1);
    border: 1px solid rgba(99,180,255,0.2);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 20px;
    flex-shrink: 0;
  }

  .edu-title {
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    font-size: 15px;
    color: var(--text);
    margin-bottom: 4px;
  }

  .edu-sub {
    font-size: 12px;
    color: var(--muted);
    line-height: 1.6;
  }

  /* ── About list ── */
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
  }

  @media (max-width: 520px) { .about-grid { grid-template-columns: 1fr; } }

  .about-item {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 14px 16px;
    font-size: 12px;
    color: var(--muted);
    display: flex;
    align-items: flex-start;
    gap: 10px;
    line-height: 1.6;
    transition: border-color 0.3s, transform 0.3s;
  }

  .about-item:hover {
    border-color: rgba(99,180,255,0.25);
    transform: translateY(-2px);
  }

  .about-dot {
    width: 6px;
    height: 6px;
    border-radius: 50%;
    flex-shrink: 0;
    margin-top: 5px;
  }

  /* ── Tech Stack ── */
  .stack-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }

  .tech-pill {
    display: flex;
    align-items: center;
    gap: 7px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 8px 14px;
    font-size: 12px;
    color: var(--muted);
    transition: all 0.25s;
    cursor: default;
    position: relative;
    overflow: hidden;
  }

  .tech-pill::before {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, transparent 60%, rgba(99,180,255,0.05));
    opacity: 0;
    transition: opacity 0.3s;
  }

  .tech-pill:hover {
    border-color: var(--pill-color, rgba(99,180,255,0.35));
    color: var(--text);
    transform: translateY(-2px);
    box-shadow: 0 4px 16px rgba(0,0,0,0.3);
  }

  .tech-pill:hover::before { opacity: 1; }

  .tech-pill svg, .tech-pill img {
    width: 15px;
    height: 15px;
    flex-shrink: 0;
  }

  /* ── Focus Tags ── */
  .tags {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    margin-top: 8px;
  }

  .tag {
    font-size: 11px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 6px 14px;
    border-radius: 6px;
    border: 1px solid;
    font-weight: 500;
  }

  .tag-blue  { border-color: rgba(99,180,255,0.4);  color: #93c5fd; background: rgba(99,180,255,0.07); }
  .tag-purple{ border-color: rgba(167,139,250,0.4); color: #c4b5fd; background: rgba(167,139,250,0.07); }
  .tag-green { border-color: rgba(52,211,153,0.4);  color: #6ee7b7; background: rgba(52,211,153,0.07); }
  .tag-amber { border-color: rgba(251,191,36,0.4);  color: #fcd34d; background: rgba(251,191,36,0.07); }

  /* ── Stats Row ── */
  .stats-row {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 12px;
  }

  .stat-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 20px;
    text-align: center;
    transition: border-color 0.3s, transform 0.3s;
  }

  .stat-card:hover {
    border-color: rgba(99,180,255,0.3);
    transform: translateY(-3px);
  }

  .stat-num {
    font-family: 'Syne', sans-serif;
    font-size: 28px;
    font-weight: 800;
    background: linear-gradient(135deg, #63b4ff, #a78bfa);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .stat-label {
    font-size: 11px;
    color: var(--muted);
    margin-top: 4px;
    letter-spacing: 0.05em;
  }

  /* ── Currently bar ── */
  .currently {
    background: var(--surface);
    border: 1px solid var(--border);
    border-left: 3px solid var(--accent3);
    border-radius: 0 12px 12px 0;
    padding: 16px 20px;
    display: flex;
    align-items: center;
    gap: 14px;
    font-size: 13px;
  }

  .pulse-dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: var(--accent3);
    flex-shrink: 0;
    animation: pulse 1.8s ease-in-out infinite;
  }

  @keyframes pulse {
    0%, 100% { box-shadow: 0 0 0 0 rgba(52,211,153,0.5); }
    50%       { box-shadow: 0 0 0 8px rgba(52,211,153,0); }
  }

  .currently-text { color: var(--muted); }
  .currently-text strong { color: var(--text); font-weight: 500; }

  /* ── Footer sig ── */
  .footer-sig {
    text-align: center;
    margin-top: 60px;
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.1em;
    opacity: 0;
    animation: fadeUp 0.8s ease 1.2s forwards;
  }

  .footer-sig span {
    color: var(--accent);
  }

  /* ── Scan line animation on load ── */
  @keyframes scanline {
    from { transform: translateY(-100%); }
    to   { transform: translateY(100vh); }
  }

  .scanline {
    position: fixed;
    top: 0; left: 0; right: 0;
    height: 3px;
    background: linear-gradient(90deg, transparent, rgba(99,180,255,0.6), transparent);
    pointer-events: none;
    z-index: 100;
    animation: scanline 1.2s ease-out 0s 1 forwards;
  }
</style>
</head>
<body>

<div class="scanline"></div>
<div class="orb orb1"></div>
<div class="orb orb2"></div>
<div class="orb orb3"></div>

<div class="wrapper">

  <!-- ── HERO ── -->
  <div class="hero">
    <div class="hero-badge">// github profile</div>
    <h1 class="hero-name">
      Krish Chaudhary
      <span class="hero-snowflake">❄</span>
    </h1>
    <div class="hero-role">
      <span class="typewriter" id="typewriter"></span>
    </div>
    <p class="hero-tagline">
      Building things for the web and mobile — one commit at a time.<br>
      Currently deep-diving into Flutter & modern app architecture.
    </p>
  </div>

  <!-- ── CURRENTLY ── -->
  <div class="section">
    <div class="currently">
      <div class="pulse-dot"></div>
      <div class="currently-text">
        <strong>Currently learning</strong> — Flutter app development concepts &amp; clean architecture patterns
      </div>
    </div>
  </div>

  <div class="divider"></div>

  <!-- ── EDUCATION ── -->
  <div class="section">
    <div class="section-label">Education</div>
    <div class="edu-card">
      <div class="edu-icon">🎓</div>
      <div>
        <div class="edu-title">BSc (Hons) Computing</div>
        <div class="edu-sub">Ithari International College &nbsp;·&nbsp; In Progress<br>
        Coursework spanning software engineering, systems design &amp; web technologies</div>
      </div>
    </div>
  </div>

  <!-- ── ABOUT ── -->
  <div class="section">
    <div class="section-label">About</div>
    <div class="about-grid">
      <div class="about-item">
        <div class="about-dot" style="background:#63b4ff;"></div>
        Passionate about building cross-platform mobile apps with Flutter &amp; Dart
      </div>
      <div class="about-item">
        <div class="about-dot" style="background:#a78bfa;"></div>
        Focused on clean UI/UX and responsive design principles
      </div>
      <div class="about-item">
        <div class="about-dot" style="background:#34d399;"></div>
        Exploring backend development with Django &amp; MongoDB
      </div>
      <div class="about-item">
        <div class="about-dot" style="background:#fbbf24;"></div>
        Continuously shipping projects to sharpen real-world skills
      </div>
    </div>
  </div>

  <!-- ── TECH STACK ── -->
  <div class="section">
    <div class="section-label">Tech Stack</div>
    <div class="stack-grid" id="stack"></div>
  </div>

  <!-- ── STATS ── -->
  <div class="section">
    <div class="section-label">At a Glance</div>
    <div class="stats-row">
      <div class="stat-card">
        <div class="stat-num" id="count-lang">0</div>
        <div class="stat-label">Languages</div>
      </div>
      <div class="stat-card">
        <div class="stat-num" id="count-tech">0</div>
        <div class="stat-label">Technologies</div>
      </div>
      <div class="stat-card">
        <div class="stat-num" id="count-years">1+</div>
        <div class="stat-label">Years Learning</div>
      </div>
    </div>
  </div>

  <!-- ── FOCUS ── -->
  <div class="section">
    <div class="section-label">Focus Areas</div>
    <div class="tags">
      <span class="tag tag-blue">App Development</span>
      <span class="tag tag-purple">Flutter &amp; Dart</span>
      <span class="tag tag-green">Web Development</span>
      <span class="tag tag-amber">Backend &amp; DBs</span>
      <span class="tag tag-blue">Responsive Design</span>
      <span class="tag tag-purple">UI / UX</span>
    </div>
  </div>

  <!-- ── FOOTER ── -->
  <div class="footer-sig">
    crafted with <span>❄</span> by Krish Chaudhary &nbsp;·&nbsp; <span>Open to collaborate</span>
  </div>

</div>

<script>
  // Typewriter
  const roles = [
    'Flutter Developer',
    'BSc Computing Student',
    'Frontend Enthusiast',
    'App Builder',
  ];
  let ri = 0, ci = 0, deleting = false;
  const tw = document.getElementById('typewriter');

  function type() {
    const word = roles[ri];
    if (!deleting) {
      tw.textContent = word.slice(0, ++ci);
      if (ci === word.length) { deleting = true; setTimeout(type, 1800); return; }
    } else {
      tw.textContent = word.slice(0, --ci);
      if (ci === 0) { deleting = false; ri = (ri + 1) % roles.length; }
    }
    setTimeout(type, deleting ? 55 : 90);
  }
  setTimeout(type, 800);

  // Tech stack data
  const techs = [
    { name: 'HTML5',       color: '#e34f26', svg: '<svg viewBox="0 0 24 24" fill="#e34f26"><path d="M1.5 0h21l-1.91 21.563L11.977 24l-8.565-2.438L1.5 0zm7.031 9.75l-.232-2.718 10.059.003.23-2.622L5.412 4.41l.698 8.01h9.126l-.326 3.426-2.91.804-2.955-.81-.188-2.11H6.248l.33 4.171L12 19.351l5.379-1.443.744-8.157H8.531z"/></svg>' },
    { name: 'CSS3',        color: '#1572b6', svg: '<svg viewBox="0 0 24 24" fill="#1572b6"><path d="M1.5 0h21l-1.91 21.563L11.977 24l-8.564-2.438L1.5 0zm17.09 4.413L5.41 4.41l.213 2.622 10.125.002-.255 2.716h-6.64l.24 2.573h6.182l-.366 3.523-2.91.804-2.956-.81-.188-2.11h-2.61l.29 3.855L12 19.288l5.373-1.53L18.59 4.414v-.001z"/></svg>' },
    { name: 'JavaScript',  color: '#f7df1e', svg: '<svg viewBox="0 0 24 24" fill="#f7df1e"><path d="M0 0h24v24H0V0zm22.034 18.276c-.175-1.095-.888-2.015-3.003-2.873-.736-.345-1.554-.585-1.797-1.14-.091-.33-.105-.51-.046-.705.15-.646.915-.84 1.515-.66.39.12.75.42.976.9 1.034-.676 1.034-.676 1.755-1.125-.27-.42-.404-.601-.586-.78-.63-.705-1.469-1.065-2.834-1.034l-.705.089c-.676.165-1.32.525-1.71 1.005-1.14 1.291-.811 3.541.569 4.471 1.365 1.02 3.361 1.244 3.616 2.205.24 1.17-.87 1.545-1.966 1.41-.811-.18-1.26-.586-1.755-1.336l-1.83 1.051c.21.48.45.689.81 1.109 1.74 1.756 6.09 1.666 6.871-1.004.029-.09.24-.705.074-1.65l.046.067zm-8.983-7.245h-2.248c0 1.938-.009 3.864-.009 5.805 0 1.232.063 2.363-.138 2.711-.33.689-1.18.601-1.566.48-.396-.196-.597-.466-.83-.855-.063-.105-.11-.196-.127-.196l-1.825 1.125c.305.63.75 1.172 1.324 1.517.855.51 2.004.675 3.207.405.783-.226 1.458-.691 1.811-1.411.51-.93.402-2.07.397-3.346.012-2.054 0-4.109 0-6.179l.004-.056z"/></svg>' },
    { name: 'Java',        color: '#f89820', svg: '<svg viewBox="0 0 24 24" fill="#f89820"><path d="M8.851 18.56s-.917.534.653.714c1.902.218 2.874.187 4.969-.211 0 0 .552.346 1.321.646-4.699 2.013-10.633-.118-6.943-1.149M8.276 15.933s-1.028.761.542.924c2.032.209 3.636.227 6.413-.308 0 0 .384.389.987.602-5.679 1.661-12.007.13-7.942-1.218M13.116 11.475c1.158 1.333-.304 2.533-.304 2.533s2.939-1.518 1.589-3.418c-1.261-1.772-2.228-2.652 3.007-5.688 0-.001-8.216 2.051-4.292 6.573M19.33 20.504s.679.559-.747.991c-2.712.822-11.288 1.069-13.669.033-.856-.373.75-.89 1.254-.998.527-.114.828-.093.828-.093-.953-.671-6.156 1.317-2.643 1.887 9.58 1.553 17.462-.7 14.977-1.82M9.292 13.21s-4.362 1.036-1.544 1.412c1.189.159 3.561.123 5.77-.062 1.806-.152 3.618-.477 3.618-.477s-.637.272-1.098.587c-4.429 1.165-12.986.623-10.522-.568 2.082-1.006 3.776-.892 3.776-.892M17.116 17.584c4.503-2.34 2.421-4.589.968-4.285-.355.074-.515.138-.515.138s.132-.207.385-.297c2.875-1.011 5.086 2.981-.928 4.562 0-.001.07-.062.09-.118M14.401 0s2.494 2.494-2.365 6.33c-3.896 3.077-.888 4.832-.001 6.836-2.274-2.053-3.943-3.858-2.824-5.539 1.644-2.469 6.197-3.665 5.19-7.627M9.734 23.924c4.322.277 10.959-.153 11.116-2.198 0 0-.302.775-3.572 1.391-3.688.694-8.239.613-10.937.168 0-.001.553.457 3.393.639"/></svg>' },
    { name: 'Python',      color: '#3776ab', svg: '<svg viewBox="0 0 24 24" fill="#3776ab"><path d="M14.25.18l.9.2.73.26.59.3.45.32.34.34.25.34.16.33.1.3.04.26.02.2-.01.13V8.5l-.05.63-.13.55-.21.46-.26.38-.3.31-.33.25-.35.19-.35.14-.33.1-.3.07-.26.04-.21.02H8.83l-.69.05-.59.14-.5.22-.41.27-.33.32-.27.35-.2.36-.15.37-.1.35-.07.32-.04.27-.02.21v3.06H3.23l-.21-.03-.28-.07-.32-.12-.35-.18-.36-.26-.36-.36-.35-.46-.32-.59-.28-.73-.21-.88-.14-1.05-.05-1.23.06-1.22.16-1.04.24-.87.32-.71.36-.57.4-.44.42-.33.42-.24.4-.16.36-.1.32-.05.24-.01h.16l.06.01h8.16v-.83H6.24l-.01-2.75-.02-.37.05-.34.11-.31.17-.28.25-.26.31-.23.38-.2.44-.18.51-.15.58-.12.64-.1.71-.06.77-.04.84-.02 1.27.05zm-6.3 1.98l-.23.33-.08.41.08.41.23.34.33.22.41.09.41-.09.33-.22.23-.34.08-.41-.08-.41-.23-.33-.33-.22-.41-.09-.41.09zm13.09 3.95l.28.06.32.12.35.18.36.27.36.35.35.47.32.59.28.73.21.88.14 1.04.05 1.23-.06 1.23-.16 1.04-.24.86-.32.71-.36.57-.4.45-.42.33-.42.24-.4.16-.36.09-.32.05-.24.02-.16-.01h-8.22v.82h5.84l.01 2.76.02.36-.05.34-.11.31-.17.29-.25.26-.31.23-.38.2-.44.18-.51.15-.58.12-.64.1-.71.06-.77.04-.84.02-1.27-.05-1.06-.13-.91-.21-.77-.29-.66-.36-.54-.42-.43-.47-.33-.5-.23-.51-.13-.49-.03-.46.01-.4.12-.37.22-.35.31-.31.4-.28.48-.25.55-.21.61-.17.66-.13.7-.1.73-.07.76-.04.77-.02h1.17v-.82H13.7v-3.07h3.44l.71.05.58-.14.49-.21.41-.28.33-.32.27-.35.2-.37.14-.36.1-.35.06-.32.04-.26.02-.21-.01-.14v-5.55l.06-.66.13-.57.21-.47.27-.38.31-.32.35-.26.36-.2.36-.14.35-.1.32-.07.28-.04.22-.02.15-.01h.14l-.01.02zm-9.15 3.14l-.23.33-.08.41.08.41.23.33.33.23.41.08.41-.08.33-.23.23-.33.08-.41-.08-.41-.23-.33-.33-.23-.41-.08-.41.08z"/></svg>' },
    { name: 'Dart',        color: '#0175c2', svg: '<svg viewBox="0 0 24 24" fill="#0175c2"><path d="M4.105 4.105S9.158 1.58 11.684.316a3.079 3.079 0 0 1 1.481-.316 3.08 3.08 0 0 1 1.481.316C15.84 1.58 20.895 4.105 20.895 4.105l-3.163 3.163-1.264-1.264-4.157 3.163-4.158-3.163-1.264 1.264L4.105 4.105zm15.79 15.79S23.42 14.84 23.684 12.316a3.079 3.079 0 0 0 .316-1.481 3.08 3.08 0 0 0-.316-1.481C22.42 7.158 19.895 4.105 19.895 4.105L16.732 7.27l1.264 1.264-3.163 4.157 3.163 4.158 1.264-1.264 3.636 4.21zm-15.79 0S1.58 14.84.316 12.316A3.079 3.079 0 0 1 0 10.835a3.08 3.08 0 0 1 .316-1.481C1.58 7.158 4.105 4.105 4.105 4.105L7.27 7.27 6.004 8.534l3.163 4.157-3.163 4.158-1.264-1.264L0 19.895zm15.79 0l-3.163-3.163 1.264-1.264-4.157-3.163-4.158 3.163 1.264 1.264L4.105 19.895C6.632 22.42 9.158 24 11.684 24h.001a3.079 3.079 0 0 0 1.481-.316C15.84 22.42 19.895 19.895 19.895 19.895z"/></svg>' },
    { name: 'Flutter',     color: '#54c5f8', svg: '<svg viewBox="0 0 24 24" fill="#54c5f8"><path d="M14.314 0L2.3 12 6 15.7 21.684 0h-7.37zm.014 11.072L7.857 17.53l6.47 6.47H21.7l-6.46-6.468 6.46-6.46h-7.372z"/></svg>' },
    { name: 'Django',      color: '#092e20', svg: '<svg viewBox="0 0 24 24" fill="#44b78b"><path d="M11.146 0h3.924v18.166c-2.013.382-3.491.535-5.096.535-4.791 0-7.288-2.166-7.288-6.32 0-4.002 2.65-6.6 6.753-6.6.637 0 1.121.05 1.707.203V0zm0 9.143a3.894 3.894 0 0 0-1.325-.204c-1.988 0-3.134 1.223-3.134 3.364 0 2.09 1.096 3.236 3.109 3.236.433 0 .79-.025 1.35-.102V9.142zM21.314 6.06v11.565c0 3.975-1.071 5.936-3.389 7.148-2.012 1.01-3.924 1.35-6.296 1.35l-.637-3.136c1.987-.357 3.363-.663 4.484-1.198 1.249-.56 1.708-1.376 1.708-3.32V6.06h4.13zM17.185 0h4.13v4.256h-4.13V0z"/></svg>' },
    { name: 'MongoDB',     color: '#47a248', svg: '<svg viewBox="0 0 24 24" fill="#47a248"><path d="M17.193 9.555c-1.264-5.58-4.252-7.414-4.573-8.115-.28-.394-.53-.954-.735-1.44-.036.495-.055.685-.523 1.184-.723.566-4.438 3.682-4.74 10.02-.282 5.912 4.27 9.435 4.888 9.884l.07.05A73.49 73.49 0 0 1 11.91 24h.481c.114-1.032.284-2.056.51-3.07.417-.019.843-.046 1.273-.104.468-.057.933-.15 1.38-.245l.026-.006c.032-.006.06-.014.09-.02a16.7 16.7 0 0 0 1.3-.393l.053-.019.067-.025.06-.022.096-.038.065-.025a8.937 8.937 0 0 0 2.726-1.897 8.418 8.418 0 0 0 2.26-5.266 8.38 8.38 0 0 0-.8-4.222zm-5.403 7.723A5.76 5.76 0 0 0 12 17.07l.007.022.005.018a5.77 5.77 0 0 0-2.394-1.06 5.77 5.77 0 0 1-.007-.033 5.76 5.76 0 0 0 2.186-.739z"/></svg>' },
    { name: 'MySQL/XAMPP', color: '#4479a1', svg: '<svg viewBox="0 0 24 24" fill="#4479a1"><path d="M16.405 5.501c-.115 0-.193.014-.274.033v.013h.014c.054.104.146.18.214.273.054.107.1.214.154.32l.014-.015c.094-.066.14-.172.14-.333-.04-.047-.046-.094-.08-.134-.04-.04-.067-.086-.12-.113l-.046-.045h-.02zm-3.234.063c-.054 0-.12.015-.159.015-.067.01-.129.01-.186.01-.078 0-.158.015-.258.015.006.027.006.046.02.066.174.098.285.218.285.405 0 .287-.215.47-.619.47-.228 0-.456-.07-.593-.202-.054-.052-.068-.13-.068-.198 0-.106.037-.196.11-.267.054-.047.12-.094.195-.12.027-.012.054-.012.08-.012-.04-.093-.103-.2-.156-.293h-.015a1.14 1.14 0 0 0-.437.345 1.087 1.087 0 0 0-.24.694c0 .187.04.38.13.545.254.494.888.784 1.55.784.52 0 1.005-.174 1.309-.472.24-.224.38-.528.38-.874 0-.29-.12-.55-.316-.728-.133-.12-.3-.21-.496-.25zm7.47 9.23c-.437-.15-1.027-.165-1.513-.165-.173 0-.347.01-.507.032-.107.013-.22.027-.333.04l-.066.012-.08.013c-.11.013-.22.027-.335.04-.493.06-.96.12-1.3.236a.844.844 0 0 0-.24.147c.08.053.146.12.2.187.027.04.054.08.066.12.054.16.054.334.054.508 0 .173 0 .347-.053.507a.844.844 0 0 1-.16.28c.04.023.08.035.12.044.28.072.584.122.874.147.067.006.135.006.202.006.067 0 .135 0 .202-.006.33-.04.646-.13.9-.3a1.33 1.33 0 0 0 .56-.76c.05-.133.08-.267.08-.4 0-.293-.1-.56-.28-.773zm-5.53-1.533a3.413 3.413 0 0 0-.33-.04c-.092 0-.186.013-.28.013-.2.013-.4.04-.6.08-.2.04-.394.094-.573.16a2.43 2.43 0 0 0-.52.24 1.99 1.99 0 0 0-.4.374c-.093.12-.173.253-.24.4.013 0 .027.007.04.007.04 0 .067-.007.107-.007.186 0 .373.013.546.053.08.014.16.04.24.067.28.09.52.226.707.4.133.126.24.266.307.4.04.094.08.2.107.306a3.49 3.49 0 0 0 .28-.27 3.427 3.427 0 0 0 .68-2.173c0-.026 0-.053-.013-.066l-.06.055zM12 0C5.373 0 0 5.373 0 12s5.373 12 12 12 12-5.373 12-12S18.627 0 12 0zm5.684 14.764c-.014.28-.067.56-.174.828a3.18 3.18 0 0 1-.44.786 3.176 3.176 0 0 1-.68.614 3.147 3.147 0 0 1-.88.347 4.45 4.45 0 0 1-.933.08c-.293 0-.586-.013-.866-.053a4.697 4.697 0 0 1-.8-.186 3.65 3.65 0 0 1-.7-.32 2.66 2.66 0 0 1-.56-.46 2.257 2.257 0 0 1-.373-.6 1.99 1.99 0 0 1-.134-.733c0-.347.067-.667.2-.947.12-.267.294-.494.507-.68a2.437 2.437 0 0 1 .74-.44c.014 0 .014.013.028.013-.093-.187-.16-.387-.2-.587-.04-.2-.06-.4-.06-.6 0-.36.08-.706.24-1.013.16-.307.387-.574.66-.786.28-.22.6-.387.947-.48.347-.106.72-.16 1.093-.16.08 0 .16 0 .24.014.08.013.16.027.24.04.08.013.16.04.24.066.08.027.16.054.24.094a3.028 3.028 0 0 0-.266-.147c-.307-.16-.64-.24-.973-.24-.174 0-.334.02-.48.054-.147.04-.28.093-.4.173a1.1 1.1 0 0 0-.307.28.894.894 0 0 0-.14.4c0 .266.08.506.24.693.16.186.38.306.613.333.228.014.456-.013.667-.093.213-.08.413-.214.573-.4.04-.047.08-.08.12-.12-.306.013-.6-.054-.84-.2a1.293 1.293 0 0 1-.52-.547c-.08-.187-.107-.387-.08-.573.027-.187.107-.36.22-.494a.94.94 0 0 1 .413-.3 1.25 1.25 0 0 1 .547-.08c.24 0 .467.054.667.16.28.147.48.374.573.654.053.16.04.333-.027.48-.066.146-.173.28-.32.386-.147.107-.307.18-.48.2-.16.027-.32.014-.48-.026.28.107.573.173.867.173.094 0 .186 0 .28-.013.094-.014.187-.04.267-.08a.97.97 0 0 0 .227-.147c.074-.066.12-.146.16-.24l.027-.066-.027-.054a.647.647 0 0 1-.04-.12c-.026-.08-.04-.16-.04-.24 0-.134.027-.254.08-.36.053-.107.133-.2.24-.267.106-.066.226-.1.36-.1.133 0 .253.034.36.1.106.067.186.16.24.267.053.106.08.226.08.36 0 .08-.014.16-.04.24a.646.646 0 0 1-.04.12l-.027.054.027.066c.04.094.08.174.16.24a.97.97 0 0 0 .226.147c.08.04.173.066.267.08.094.013.186.013.28.013.12 0 .24-.014.36-.027.2-.027.4-.08.58-.16.32-.12.607-.3.853-.52.24-.22.44-.48.573-.773.12-.28.187-.586.18-.9-.014-.347-.107-.673-.28-.96-.18-.3-.44-.547-.747-.733a2.633 2.633 0 0 0-1.013-.373c-.186-.027-.373-.04-.56-.04-.24 0-.48.026-.706.08-.227.053-.44.14-.64.253a2.57 2.57 0 0 0-.52.414 2.518 2.518 0 0 0-.387.573 2.37 2.37 0 0 0-.2.707c-.013.133-.013.267 0 .4.027.267.094.52.213.747.12.226.28.44.48.613.066.054.133.107.2.16-.027.014-.054.027-.08.04a2.847 2.847 0 0 0-.48.293 2.763 2.763 0 0 0-.453.44 2.39 2.39 0 0 0-.32.574 2.263 2.263 0 0 0-.12.666 2.5 2.5 0 0 0 .24 1.107c.2.36.494.68.853.9.36.226.773.373 1.2.44.2.026.4.04.6.04.226 0 .44-.014.646-.04.68-.094 1.32-.374 1.773-.8.28-.253.494-.56.64-.9.147-.333.2-.7.187-1.053z"/></svg>' },
  ];

  const stackEl = document.getElementById('stack');
  techs.forEach(t => {
    const pill = document.createElement('div');
    pill.className = 'tech-pill';
    pill.style.setProperty('--pill-color', t.color + '55');
    pill.innerHTML = `${t.svg}<span>${t.name}</span>`;
    stackEl.appendChild(pill);
  });

  // Animate counters
  function animCount(el, target, suffix = '') {
    let n = 0;
    const step = Math.ceil(target / 30);
    const t = setInterval(() => {
      n = Math.min(n + step, target);
      el.textContent = n + suffix;
      if (n >= target) clearInterval(t);
    }, 40);
  }

  setTimeout(() => {
    animCount(document.getElementById('count-lang'), 6);
    animCount(document.getElementById('count-tech'), 5);
  }, 900);
</script>
</body>
</html>
