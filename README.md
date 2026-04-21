<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Lak Tran — Developer Profile</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;600;700&family=Syne:wght@400;700;800&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0a0a0f;
    --surface: #0f0f1a;
    --card: #13131f;
    --border: #1e1e30;
    --accent: #00d4ff;
    --accent2: #7c3aed;
    --accent3: #00ff9d;
    --text: #e2e8f0;
    --muted: #64748b;
    --glow: 0 0 20px rgba(0, 212, 255, 0.3);
    --glow2: 0 0 20px rgba(124, 58, 237, 0.3);
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'JetBrains Mono', monospace;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* CANVAS BG */
  #canvas {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    z-index: 0;
    opacity: 0.35;
  }

  .wrapper {
    position: relative;
    z-index: 1;
    max-width: 900px;
    margin: 0 auto;
    padding: 48px 24px 80px;
  }

  /* HERO */
  .hero {
    display: flex;
    align-items: center;
    gap: 36px;
    margin-bottom: 52px;
    animation: fadeUp 0.8s ease both;
  }

  .avatar-ring {
    position: relative;
    flex-shrink: 0;
  }

  .avatar-ring::before {
    content: '';
    position: absolute;
    inset: -4px;
    border-radius: 50%;
    background: conic-gradient(var(--accent), var(--accent2), var(--accent3), var(--accent));
    animation: spin 4s linear infinite;
    z-index: -1;
  }

  .avatar {
    width: 110px;
    height: 110px;
    border-radius: 50%;
    background: linear-gradient(135deg, #0891b2 0%, #7c3aed 100%);
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'Syne', sans-serif;
    font-size: 38px;
    font-weight: 800;
    color: #fff;
    position: relative;
    z-index: 1;
    border: 3px solid var(--bg);
  }

  .hero-info { flex: 1; }

  .greeting {
    font-size: 13px;
    color: var(--accent);
    letter-spacing: 3px;
    text-transform: uppercase;
    margin-bottom: 6px;
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .wave {
    display: inline-block;
    animation: wave 2s ease-in-out infinite;
    transform-origin: 70% 70%;
    font-size: 18px;
  }

  @keyframes wave {
    0%, 100% { transform: rotate(0deg); }
    20% { transform: rotate(20deg); }
    40% { transform: rotate(-10deg); }
    60% { transform: rotate(15deg); }
    80% { transform: rotate(-5deg); }
  }

  .name {
    font-family: 'Syne', sans-serif;
    font-size: 46px;
    font-weight: 800;
    background: linear-gradient(135deg, #fff 30%, var(--accent));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    line-height: 1.1;
    margin-bottom: 8px;
  }

  .typewriter-wrap {
    font-size: 14px;
    color: var(--muted);
    height: 22px;
    overflow: hidden;
  }

  .typewriter {
    border-right: 2px solid var(--accent);
    padding-right: 4px;
    animation: blink 0.8s step-end infinite;
  }

  @keyframes blink { 50% { border-color: transparent; } }

  .meta {
    display: flex;
    gap: 20px;
    margin-top: 16px;
    flex-wrap: wrap;
  }

  .meta-item {
    display: flex;
    align-items: center;
    gap: 7px;
    font-size: 12px;
    color: var(--muted);
    transition: color 0.2s;
  }
  .meta-item:hover { color: var(--accent); }
  .meta-item .dot {
    width: 6px; height: 6px;
    border-radius: 50%;
    background: var(--accent3);
    animation: pulse 2s ease infinite;
  }

  @keyframes pulse { 0%,100% { opacity: 1; } 50% { opacity: 0.3; } }

  /* SECTION */
  .section {
    margin-bottom: 40px;
    animation: fadeUp 0.8s ease both;
  }

  .section:nth-child(2) { animation-delay: 0.1s; }
  .section:nth-child(3) { animation-delay: 0.2s; }
  .section:nth-child(4) { animation-delay: 0.3s; }
  .section:nth-child(5) { animation-delay: 0.4s; }

  .section-label {
    font-size: 11px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 16px;
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .section-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: linear-gradient(90deg, var(--border), transparent);
  }

  /* SKILLS */
  .skills-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }

  .skill-chip {
    display: flex;
    align-items: center;
    gap: 8px;
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 8px 14px;
    font-size: 12px;
    color: var(--text);
    cursor: default;
    transition: all 0.25s ease;
    position: relative;
    overflow: hidden;
  }

  .skill-chip::before {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    opacity: 0;
    transition: opacity 0.25s;
  }

  .skill-chip:hover::before { opacity: 0.1; }

  .skill-chip:hover {
    border-color: var(--accent);
    box-shadow: var(--glow);
    transform: translateY(-2px);
  }

  .skill-chip img {
    width: 20px;
    height: 20px;
    position: relative;
    z-index: 1;
  }

  .skill-chip span {
    position: relative;
    z-index: 1;
  }

  /* STATS */
  .stats-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
  }

  @media (max-width: 600px) {
    .stats-grid { grid-template-columns: 1fr; }
    .hero { flex-direction: column; text-align: center; }
    .meta { justify-content: center; }
    .name { font-size: 34px; }
  }

  .stat-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 14px;
    overflow: hidden;
    transition: all 0.3s ease;
  }

  .stat-card:hover {
    border-color: var(--accent);
    box-shadow: var(--glow);
    transform: translateY(-3px);
  }

  .stat-card img {
    width: 100%;
    display: block;
    border-radius: 13px;
  }

  /* SOCIALS */
  .socials {
    display: flex;
    gap: 14px;
    flex-wrap: wrap;
  }

  .social-btn {
    display: flex;
    align-items: center;
    gap: 10px;
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 12px 20px;
    font-size: 13px;
    color: var(--text);
    text-decoration: none;
    transition: all 0.25s ease;
    font-family: 'JetBrains Mono', monospace;
  }

  .social-btn:hover {
    border-color: var(--accent);
    color: var(--accent);
    box-shadow: var(--glow);
    transform: translateY(-2px);
  }

  .social-btn svg {
    width: 18px; height: 18px;
    fill: currentColor;
  }

  /* BADGE */
  .badge {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 6px 14px;
    font-size: 12px;
    color: var(--muted);
    margin-bottom: 20px;
  }
  .badge .b-accent { color: var(--accent); font-weight: 600; }

  /* TERMINAL CARD */
  .terminal {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 14px;
    overflow: hidden;
    margin-bottom: 40px;
    animation: fadeUp 0.8s ease 0.05s both;
  }

  .terminal-bar {
    background: var(--surface);
    padding: 10px 16px;
    display: flex;
    align-items: center;
    gap: 8px;
    border-bottom: 1px solid var(--border);
  }

  .dot-red { width: 12px; height: 12px; border-radius: 50%; background: #ff5f57; }
  .dot-yellow { width: 12px; height: 12px; border-radius: 50%; background: #febc2e; }
  .dot-green { width: 12px; height: 12px; border-radius: 50%; background: #28c840; }

  .terminal-title {
    flex: 1;
    text-align: center;
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 1px;
  }

  .terminal-body {
    padding: 20px 24px;
    font-size: 13px;
    line-height: 2;
  }

  .t-prompt { color: var(--accent3); }
  .t-cmd { color: var(--accent); }
  .t-out { color: var(--muted); }
  .t-val { color: #fff; }
  .t-str { color: #fbbf24; }

  /* ANIMATIONS */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to { opacity: 1; transform: translateY(0); }
  }

  @keyframes spin {
    to { transform: rotate(360deg); }
  }

  /* Scrollbar */
  ::-webkit-scrollbar { width: 6px; }
  ::-webkit-scrollbar-track { background: var(--bg); }
  ::-webkit-scrollbar-thumb { background: var(--border); border-radius: 3px; }
</style>
</head>
<body>

<canvas id="canvas"></canvas>

<div class="wrapper">

  <!-- HERO -->
  <div class="hero">
    <div class="avatar-ring">
      <div class="avatar">LT</div>
    </div>
    <div class="hero-info">
      <div class="greeting">
        <span class="wave">👋</span>
        Hi there, I'm
      </div>
      <div class="name">Lak Tran</div>
      <div class="typewriter-wrap">
        <span class="typewriter" id="typewriter"></span>
      </div>
      <div class="meta">
        <div class="meta-item">
          <div class="dot"></div>
          🌍 Vietnam
        </div>
        <div class="meta-item">
          ✉️ bestlak307@gmail.com
        </div>
      </div>
    </div>
  </div>

  <!-- TERMINAL -->
  <div class="terminal">
    <div class="terminal-bar">
      <div class="dot-red"></div>
      <div class="dot-yellow"></div>
      <div class="dot-green"></div>
      <div class="terminal-title">lak@dev ~ zsh</div>
    </div>
    <div class="terminal-body">
      <div><span class="t-prompt">➜</span> <span class="t-cmd">whoami</span></div>
      <div class="t-out">  <span class="t-val">Lak Tran</span> — Backend &amp; Systems Developer</div>
      <div><span class="t-prompt">➜</span> <span class="t-cmd">cat ./about.json</span></div>
      <div class="t-out">&nbsp;&nbsp;{</div>
      <div class="t-out">&nbsp;&nbsp;&nbsp;&nbsp;"location": <span class="t-str">"Ho Chi Minh City, Vietnam"</span>,</div>
      <div class="t-out">&nbsp;&nbsp;&nbsp;&nbsp;"focus": <span class="t-str">"Systems, Web & DevOps"</span>,</div>
      <div class="t-out">&nbsp;&nbsp;&nbsp;&nbsp;"github": <span class="t-str">"@BaekHyunLak"</span>,</div>
      <div class="t-out">&nbsp;&nbsp;&nbsp;&nbsp;"status": <span class="t-str">"open to opportunities"</span></div>
      <div class="t-out">&nbsp;&nbsp;}</div>
      <div><span class="t-prompt">➜</span> <span class="t-cmd">_</span><span style="animation:blink 0.8s step-end infinite;border-right:2px solid #00d4ff">&nbsp;</span></div>
    </div>
  </div>

  <!-- SKILLS -->
  <div class="section">
    <div class="section-label">// Tech Stack</div>
    <div class="skills-grid">
      <div class="skill-chip"><img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/c-colored.svg" alt="C"><span>C</span></div>
      <div class="skill-chip"><img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/cplusplus-colored.svg" alt="C++"><span>C++</span></div>
      <div class="skill-chip"><img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/javascript-colored.svg" alt="JS"><span>JavaScript</span></div>
      <div class="skill-chip"><img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/java-colored.svg" alt="Java"><span>Java</span></div>
      <div class="skill-chip"><img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/php-colored.svg" alt="PHP"><span>PHP</span></div>
      <div class="skill-chip"><img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/gnubash-colored.svg" alt="Bash"><span>Bash</span></div>
      <div class="skill-chip"><img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/html5-colored.svg" alt="HTML5"><span>HTML5</span></div>
      <div class="skill-chip"><img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/css3-colored.svg" alt="CSS3"><span>CSS3</span></div>
      <div class="skill-chip"><img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/mysql-colored.svg" alt="MySQL"><span>MySQL</span></div>
      <div class="skill-chip"><img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/git-colored.svg" alt="Git"><span>Git</span></div>
      <div class="skill-chip"><img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/docker-colored.svg" alt="Docker"><span>Docker</span></div>
      <div class="skill-chip"><img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/linux-colored.svg" alt="Linux"><span>Linux</span></div>
      <div class="skill-chip"><img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/ubuntu-colored.svg" alt="Ubuntu"><span>Ubuntu</span></div>
      <div class="skill-chip"><img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/skills/visualstudiocode-colored.svg" alt="VSCode"><span>VS Code</span></div>
    </div>
  </div>

  <!-- GITHUB STATS -->
  <div class="section">
    <div class="section-label">// GitHub Stats</div>
    <div class="stats-grid">
      <div class="stat-card">
        <img src="https://github-readme-stats.vercel.app/api?username=BaekHyunLak&show_icons=true&hide=&count_private=true&title_color=00d4ff&text_color=e2e8f0&icon_color=00d4ff&bg_color=13131f&hide_border=true&show_icons=true" alt="GitHub Stats">
      </div>
      <div class="stat-card">
        <img src="https://github-readme-streak-stats.herokuapp.com/?user=BaekHyunLak&stroke=e2e8f0&background=13131f&ring=00d4ff&fire=7c3aed&currStreakNum=ffffff&currStreakLabel=00d4ff&sideNums=e2e8f0&sideLabels=e2e8f0&dates=64748b&hide_border=true" alt="Streak Stats">
      </div>
      <div class="stat-card" style="grid-column: 1 / -1">
        <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=BaekHyunLak&langs_count=10&title_color=00d4ff&text_color=e2e8f0&icon_color=00d4ff&bg_color=13131f&hide_border=true&locale=en&custom_title=Top%20Languages&layout=compact" alt="Top Languages">
      </div>
    </div>
  </div>

  <!-- SOCIALS -->
  <div class="section">
    <div class="section-label">// Connect</div>
    <div class="socials">
      <a href="https://www.github.com/BaekHyunLak" target="_blank" class="social-btn">
        <svg viewBox="0 0 24 24"><path d="M12 2C6.477 2 2 6.477 2 12c0 4.42 2.865 8.17 6.839 9.49.5.092.682-.217.682-.482 0-.237-.008-.866-.013-1.7-2.782.603-3.369-1.342-3.369-1.342-.454-1.155-1.11-1.462-1.11-1.462-.908-.62.069-.608.069-.608 1.003.07 1.531 1.03 1.531 1.03.892 1.529 2.341 1.087 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.11-4.555-4.943 0-1.091.39-1.984 1.029-2.683-.103-.253-.446-1.27.098-2.647 0 0 .84-.269 2.75 1.025A9.578 9.578 0 0112 6.836c.85.004 1.705.115 2.504.337 1.909-1.294 2.747-1.025 2.747-1.025.546 1.377.203 2.394.1 2.647.64.699 1.028 1.592 1.028 2.683 0 3.842-2.339 4.687-4.566 4.935.359.309.678.919.678 1.852 0 1.336-.012 2.415-.012 2.741 0 .267.18.578.688.48C19.138 20.167 22 16.418 22 12c0-5.523-4.477-10-10-10z"/></svg>
        @BaekHyunLak
      </a>
      <a href="https://www.facebook.com/rualkwa/" target="_blank" class="social-btn">
        <svg viewBox="0 0 24 24"><path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"/></svg>
        Facebook
      </a>
      <a href="mailto:bestlak307@gmail.com" class="social-btn">
        <svg viewBox="0 0 24 24"><path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>
        Email Me
      </a>
    </div>
  </div>

</div>

<script>
// ── PARTICLE CANVAS ──────────────────────────────────────────
const canvas = document.getElementById('canvas');
const ctx = canvas.getContext('2d');

function resize() {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
}
resize();
window.addEventListener('resize', resize);

const particles = [];
const PARTICLE_COUNT = 80;

for (let i = 0; i < PARTICLE_COUNT; i++) {
  particles.push({
    x: Math.random() * window.innerWidth,
    y: Math.random() * window.innerHeight,
    r: Math.random() * 1.5 + 0.3,
    dx: (Math.random() - 0.5) * 0.4,
    dy: (Math.random() - 0.5) * 0.4,
    alpha: Math.random() * 0.6 + 0.2,
  });
}

function drawParticles() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  // Draw connections
  for (let i = 0; i < particles.length; i++) {
    for (let j = i + 1; j < particles.length; j++) {
      const dx = particles[i].x - particles[j].x;
      const dy = particles[i].y - particles[j].y;
      const dist = Math.sqrt(dx * dx + dy * dy);
      if (dist < 130) {
        ctx.beginPath();
        ctx.strokeStyle = `rgba(0, 212, 255, ${0.15 * (1 - dist / 130)})`;
        ctx.lineWidth = 0.5;
        ctx.moveTo(particles[i].x, particles[i].y);
        ctx.lineTo(particles[j].x, particles[j].y);
        ctx.stroke();
      }
    }
  }

  // Draw dots
  particles.forEach(p => {
    ctx.beginPath();
    ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
    ctx.fillStyle = `rgba(0, 212, 255, ${p.alpha})`;
    ctx.fill();

    p.x += p.dx;
    p.y += p.dy;

    if (p.x < 0 || p.x > canvas.width) p.dx *= -1;
    if (p.y < 0 || p.y > canvas.height) p.dy *= -1;
  });

  requestAnimationFrame(drawParticles);
}
drawParticles();

// ── TYPEWRITER ───────────────────────────────────────────────
const phrases = [
  'Systems Developer 🔧',
  'C / C++ Enthusiast ⚡',
  'Linux & Docker Fan 🐧',
  'Web & Backend Dev 🌐',
  'Open Source Curious 🚀',
];

let pi = 0, ci = 0, deleting = false;
const el = document.getElementById('typewriter');

function type() {
  const cur = phrases[pi];
  if (!deleting) {
    el.textContent = cur.slice(0, ++ci);
    if (ci === cur.length) { deleting = true; setTimeout(type, 1800); return; }
  } else {
    el.textContent = cur.slice(0, --ci);
    if (ci === 0) { deleting = false; pi = (pi + 1) % phrases.length; }
  }
  setTimeout(type, deleting ? 50 : 80);
}
type();

// ── SKILL CHIP STAGGER ───────────────────────────────────────
document.querySelectorAll('.skill-chip').forEach((chip, i) => {
  chip.style.opacity = '0';
  chip.style.transform = 'translateY(12px)';
  chip.style.transition = 'opacity 0.4s ease, transform 0.4s ease, border-color 0.25s, box-shadow 0.25s';
  setTimeout(() => {
    chip.style.opacity = '1';
    chip.style.transform = 'translateY(0)';
  }, 600 + i * 60);
});
</script>
</body>
</html>
