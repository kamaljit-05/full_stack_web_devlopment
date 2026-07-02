<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Full Stack Web Development Banner</title>

<!-- Devicon = free icon font with real brand logos (JS, Node, PHP, etc.) -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/devicon@2.15.1/devicon.min.css">

<!-- Type pairing: Space Grotesk for the headline, JetBrains Mono for everything code-flavored -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@500;700&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">

<style>

  /* ============ TOKENS ============ */
  :root {
    --bg-0: #07090a;
    --bg-1: #0d1210;
    --ink-0: #f3f5f0;
    --ink-1: #aab3ab;
    --lime: #9acd32;
    --lime-soft: #d4ff5f;
    --cyan: #56e0c9;
    --amber: #ffb066;
    --line: rgba(255, 255, 255, 0.14);
    --glass: rgba(255, 255, 255, 0.06);
    --font-display: 'Space Grotesk', 'Segoe UI', sans-serif;
    --font-mono: 'JetBrains Mono', 'Courier New', monospace;
  }

  /* ============ BASE RESET ============ */
  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    font-family: var(--font-display);
    background: var(--bg-0);
  }

  /* ============ HERO SECTION ============ */
  .hero {
    position: relative;
    width: 100%;
    height: 640px;
    overflow: hidden;
    background:
      radial-gradient(ellipse 70% 55% at 50% 42%, rgba(154,205,50,0.08), transparent 60%),
      url('https://images.unsplash.com/photo-1517694712202-14dd9538aa97?w=1400&q=80')
      center/cover no-repeat;
    box-shadow: inset 0 0 180px 70px rgba(0,0,0,0.6);
  }

  /* dark tint so everything on top stays readable, plus a slight gradient toward the edges */
  .hero::before {
    content: "";
    position: absolute;
    inset: 0;
    background:
      linear-gradient(180deg, rgba(7,9,10,0.88) 0%, rgba(9,12,10,0.82) 45%, rgba(7,9,10,0.92) 100%);
  }

  /* faint tech-grid pattern over the photo, adds a "code editor" feel */
  .hero::after {
    content: "";
    position: absolute;
    inset: 0;
    background-image:
      linear-gradient(rgba(86, 224, 201, 0.045) 1px, transparent 1px),
      linear-gradient(90deg, rgba(86, 224, 201, 0.045) 1px, transparent 1px);
    background-size: 42px 42px;
  }

  /* status pill: ties the whole banner back to "this repo is being actively worked on" */
  .status-badge {
    position: absolute;
    top: 26px;
    left: 26px;
    z-index: 4;
    display: flex;
    align-items: center;
    gap: 9px;
    font-family: var(--font-mono);
    font-size: 11px;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    color: var(--ink-1);
  }

  .status-dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: var(--amber);
    animation: statusPulse 2.2s ease-in-out infinite;
  }

  @keyframes statusPulse {
    0%   { box-shadow: 0 0 0 0 rgba(255, 176, 102, 0.55); }
    70%  { box-shadow: 0 0 0 9px rgba(255, 176, 102, 0); }
    100% { box-shadow: 0 0 0 0 rgba(255, 176, 102, 0); }
  }

  /* soft glowing blob behind the center circle, gently pulses */
  .glow {
    position: absolute;
    top: 50%;
    left: 50%;
    width: 440px;
    height: 440px;
    transform: translate(-50%, -50%);
    background: radial-gradient(circle, rgba(154,205,50,0.22) 0%, rgba(86,224,201,0.10) 45%, rgba(154,205,50,0) 72%);
    filter: blur(14px);
    animation: pulse 4.5s ease-in-out infinite;
  }

  @keyframes pulse {
    0%, 100% { opacity: 0.6; transform: translate(-50%, -50%) scale(1); }
    50%      { opacity: 1;   transform: translate(-50%, -50%) scale(1.07); }
  }

  /* ============ ORBIT WRAPPER ============ */
  .orbit-stage {
    position: absolute;
    top: 50%;
    left: 50%;
    width: 480px;
    height: 480px;
    transform: translate(-50%, -50%);
  }

  /* the ring itself rotates continuously — a slow orbit */
  .ring {
    position: absolute;
    inset: 0;
    border-radius: 50%;
    border: 1.5px dashed rgba(86, 224, 201, 0.3);
    animation: spin 42s linear infinite;
  }

  /* a second, tighter ring drifting the opposite way — cheap parallax, no extra icons needed */
  .ring-inner {
    position: absolute;
    inset: 46px;
    border-radius: 50%;
    border: 1px dashed rgba(154, 205, 50, 0.16);
    animation: spin-reverse-slow 60s linear infinite;
  }

  @keyframes spin {
    from { transform: rotate(0deg); }
    to   { transform: rotate(360deg); }
  }

  @keyframes spin-reverse-slow {
    from { transform: rotate(0deg); }
    to   { transform: rotate(-360deg); }
  }

  /* each icon "seat" is placed on the ring and spins WITH it... */
  .seat {
    position: absolute;
    top: 50%;
    left: 50%;
    width: 0;
    height: 0;
    animation: spin 42s linear infinite;
  }

  /* ...while the icon inside spins the opposite way at the same speed,
     cancelling the rotation out so logos always stay upright */
  .icon {
    position: absolute;
    width: 74px;
    height: 74px;
    margin: -37px 0 0 -37px;
    background: #f8f8f8;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 30px;
    box-shadow: 0 6px 18px rgba(0,0,0,0.55), 0 0 0 1px rgba(255,255,255,0.06);
    animation: spin-reverse 42s linear infinite;
    transition: transform 0.25s ease, box-shadow 0.25s ease;
    cursor: default;
  }

  @keyframes spin-reverse {
    from { transform: rotate(0deg); }
    to   { transform: rotate(-360deg); }
  }

  .icon:hover {
    transform: scale(1.18);
    box-shadow: 0 0 0 3px var(--lime), 0 0 26px rgba(154, 205, 50, 0.75);
    z-index: 5;
  }

  /* little name tag that appears above an icon on hover */
  .icon::after {
    content: attr(data-name);
    position: absolute;
    bottom: 115%;
    left: 50%;
    transform: translateX(-50%);
    background: var(--lime);
    color: #0b0d0a;
    font-family: var(--font-mono);
    font-size: 11px;
    font-weight: 700;
    padding: 3px 9px;
    border-radius: 5px;
    white-space: nowrap;
    opacity: 0;
    pointer-events: none;
    transition: opacity 0.2s ease;
  }

  .icon:hover::after { opacity: 1; }

  /* brand colors for each logo */
  .devicon-javascript-plain   { color: #f0db4f; }
  .devicon-mysql-plain        { color: #4479A1; }
  .devicon-bootstrap-plain    { color: #7952B3; }
  .devicon-nodejs-plain       { color: #3c873a; }
  .devicon-angularjs-plain    { color: #dd1b16; }
  .devicon-vuejs-plain        { color: #41b883; }
  .devicon-css3-plain         { color: #2965f1; }
  .devicon-html5-plain        { color: #e34f26; }
  .devicon-php-plain          { color: #777bb4; }
  .code-symbol                { color: #333; font-weight: 700; font-size: 24px; font-family: var(--font-mono); }
  .devicon-figma-plain        { color: #a259ff; }

  /* fade + pop entrance for icons */
  .icon { opacity: 0; animation: spin-reverse 42s linear infinite, pop-in 0.6s ease forwards; }
  @keyframes pop-in {
    from { opacity: 0; transform: scale(0.3); }
    to   { opacity: 1; transform: scale(1); }
  }

  /* ============ CENTER GLASS CIRCLE ============ */
  .center-text {
    position: absolute;
    top: 50%;
    left: 50%;
    width: 292px;
    height: 292px;
    transform: translate(-50%, -50%);
    background: rgba(255, 255, 255, 0.055);
    border: 1px solid rgba(255, 255, 255, 0.16);
    border-radius: 50%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
    backdrop-filter: blur(6px);
    -webkit-backdrop-filter: blur(6px);
    z-index: 2;
  }

  .center-text .eyebrow {
    font-family: var(--font-mono);
    font-size: 10px;
    letter-spacing: 3px;
    color: var(--cyan);
    text-transform: uppercase;
    margin-bottom: 10px;
  }

  .center-text h1 {
    font-size: 34px;
    font-weight: 700;
    letter-spacing: 0.5px;
    background: linear-gradient(90deg, var(--lime), var(--cyan), var(--lime-soft), var(--lime));
    background-size: 300% auto;
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
    animation: shine 5s linear infinite;
  }

  @keyframes shine {
    to { background-position: 300% center; }
  }

  .center-text p.subtitle {
    margin-top: 8px;
    font-family: var(--font-mono);
    font-size: 12px;
    letter-spacing: 3px;
    color: var(--ink-0);
  }

  .center-text span.divider {
    display: block;
    width: 36px;
    height: 2px;
    background: linear-gradient(90deg, var(--lime), var(--cyan));
    margin: 12px auto 0;
  }

  /* ============ TERMINAL STATUS LINE ============ */
  .terminal-bar {
    position: relative;
    z-index: 3;
    display: flex;
    justify-content: center;
    align-items: baseline;
    gap: 8px;
    padding: 26px 20px 4px;
    font-family: var(--font-mono);
    font-size: 13px;
    color: var(--ink-1);
    background: var(--bg-0);
  }

  .terminal-bar .prompt { color: var(--lime); }
  .terminal-bar .terminal-text { color: var(--ink-0); }
  .terminal-bar .cursor {
    color: var(--lime);
    animation: blink 1s step-end infinite;
  }

  @keyframes blink {
    0%, 100% { opacity: 1; }
    50%      { opacity: 0; }
  }

  /* ============ BOTTOM STACK TAGS ============ */
  .stack-pills {
    position: relative;
    z-index: 3;
    display: flex;
    justify-content: center;
    gap: 12px;
    flex-wrap: wrap;
    padding: 16px 20px 30px;
    background: var(--bg-0);
  }

  .pill {
    font-family: var(--font-mono);
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid var(--line);
    color: var(--ink-1);
    font-size: 12px;
    letter-spacing: 0.5px;
    padding: 8px 16px;
    border-radius: 6px;
    transition: 0.25s ease;
  }

  .pill .tag-prefix { color: var(--cyan); margin-right: 6px; }

  .pill:hover {
    background: linear-gradient(90deg, var(--lime), var(--cyan));
    color: #0b0d0a;
    border-color: transparent;
    transform: translateY(-3px);
  }

  .pill:hover .tag-prefix { color: #0b0d0a; }

  /* stagger the icon pop-in so they don't all appear at once */
  .seat:nth-child(1)  .icon { animation-delay: 0.05s; }
  .seat:nth-child(2)  .icon { animation-delay: 0.10s; }
  .seat:nth-child(3)  .icon { animation-delay: 0.15s; }
  .seat:nth-child(4)  .icon { animation-delay: 0.20s; }
  .seat:nth-child(5)  .icon { animation-delay: 0.25s; }
  .seat:nth-child(6)  .icon { animation-delay: 0.30s; }
  .seat:nth-child(7)  .icon { animation-delay: 0.35s; }
  .seat:nth-child(8)  .icon { animation-delay: 0.40s; }
  .seat:nth-child(9)  .icon { animation-delay: 0.45s; }
  .seat:nth-child(10) .icon { animation-delay: 0.50s; }

  /* respect reduced-motion preferences */
  @media (prefers-reduced-motion: reduce) {
    .ring, .ring-inner, .seat, .icon, .glow, .center-text h1 {
      animation: none !important;
    }
    .cursor { animation: none !important; opacity: 1; }
  }

  /* ============ RESPONSIVE ============ */
  @media (max-width: 700px) {
    .hero { height: 540px; }
    .orbit-stage { width: 300px; height: 300px; }
    .glow { width: 270px; height: 270px; }
    .ring-inner { inset: 28px; }
    .center-text { width: 186px; height: 186px; }
    .center-text .eyebrow { font-size: 8px; letter-spacing: 2px; margin-bottom: 6px; }
    .center-text h1 { font-size: 21px; }
    .center-text p.subtitle { font-size: 9px; letter-spacing: 2px; }
    .icon { width: 46px; height: 46px; margin: -23px 0 0 -23px; font-size: 18px; }
    .status-badge { font-size: 9px; top: 16px; left: 16px; }
    .terminal-bar { font-size: 11px; padding: 20px 16px 4px; flex-wrap: wrap; text-align: center; }
    .stack-pills { display: none; } /* keep mobile clean */
  }

</style>
</head>
<body>

  <section class="hero">

    <div class="status-badge">
      <span class="status-dot"></span>
      <span>actively learning &amp; building</span>
    </div>

    <div class="glow"></div>

    <div class="orbit-stage">
      <div class="ring"></div>
      <div class="ring-inner"></div>

      <!--
        Each "seat" is rotated to its spot on the circle (JS below sets the
        angle), then the .icon inside counter-rotates so the logo itself
        never looks upside down, even while the ring spins.
      -->
      <div class="seats"></div>

      <div class="center-text">
        <p class="eyebrow">Practice Repository</p>
        <h1>Full Stack</h1>
        <p class="subtitle">WEB DEVELOPMENT</p>
        <span class="divider"></span>
      </div>
    </div>

  </section>

  <div class="terminal-bar">
    <span class="prompt">$</span>
    <span class="terminal-text" id="terminalText"></span>
    <span class="cursor">▌</span>
  </div>

  <div class="stack-pills">
    <div class="pill"><span class="tag-prefix">&gt;</span>Frontend</div>
    <div class="pill"><span class="tag-prefix">&gt;</span>Backend</div>
    <div class="pill"><span class="tag-prefix">&gt;</span>Database</div>
    <div class="pill"><span class="tag-prefix">&gt;</span>Version Control</div>
    <div class="pill"><span class="tag-prefix">&gt;</span>Deployment</div>
  </div>

<script>
  // list of technologies to place around the ring, in clockwise order
  const techs = [
    { name: 'JavaScript', html: '<i class="devicon-javascript-plain"></i>' },
    { name: 'MySQL',      html: '<i class="devicon-mysql-plain"></i>' },
    { name: 'Bootstrap',  html: '<i class="devicon-bootstrap-plain"></i>' },
    { name: 'Code',       html: '<span class="code-symbol">&lt;/&gt;</span>' },
    { name: 'Design',     html: '<i class="devicon-figma-plain"></i>' },
    { name: 'Node.js',    html: '<i class="devicon-nodejs-plain"></i>' },
    { name: 'Angular',    html: '<i class="devicon-angularjs-plain"></i>' },
    { name: 'Vue.js',     html: '<i class="devicon-vuejs-plain"></i>' },
    { name: 'CSS3',       html: '<i class="devicon-css3-plain"></i>' },
    { name: 'HTML5',      html: '<i class="devicon-html5-plain"></i>' },
    { name: 'PHP',        html: '<span style="font-family:\'JetBrains Mono\',monospace;font-weight:700;color:#777bb4">PHP</span>' }
  ];

  const seatsContainer = document.querySelector('.seats');
  const radius = 220; // distance of icons from the center, in px

  techs.forEach((tech, i) => {
    const angle = (360 / techs.length) * i; // evenly space around 360°

    // "seat" positions the icon on the circle by rotating then pushing
    // it outward by `radius`, exactly like a clock hand
    const seat = document.createElement('div');
    seat.className = 'seat';
    seat.style.transform = `rotate(${angle}deg) translate(${radius}px)`;

    const icon = document.createElement('div');
    icon.className = 'icon';
    icon.setAttribute('data-name', tech.name);
    icon.innerHTML = tech.html;
    // rotate the icon back so it reads upright at its seat
    icon.style.transform = `rotate(${-angle}deg)`;

    seat.appendChild(icon);
    seatsContainer.appendChild(seat);
  });

  // one-shot typewriter for the terminal status line — a small, orchestrated
  // moment rather than a looping gimmick
  const terminalPhrase = 'status: building full-stack skills, one commit at a time';
  const terminalEl = document.getElementById('terminalText');
  let charIndex = 0;

  function typeTerminal() {
    if (charIndex <= terminalPhrase.length) {
      terminalEl.textContent = terminalPhrase.slice(0, charIndex);
      charIndex++;
      setTimeout(typeTerminal, 32);
    }
  }
  typeTerminal();
</script>

</body>
</html>