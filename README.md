<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Santhosh Kumar K — Developer & Data Analyst</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,300&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #040810;
    --bg2: #080f1e;
    --bg3: #0c1628;
    --accent: #00d4ff;
    --accent2: #7c3aed;
    --accent3: #f59e0b;
    --text: #e8f0fe;
    --muted: #6b7fa8;
    --card: rgba(12,22,44,0.8);
    --border: rgba(0,212,255,0.15);
    --glow: 0 0 40px rgba(0,212,255,0.2);
  }

  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    overflow-x: hidden;
    cursor: none;
  }

  /* CUSTOM CURSOR */
  .cursor {
    width: 12px; height: 12px;
    background: var(--accent);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9999;
    transition: transform 0.1s;
    mix-blend-mode: screen;
  }
  .cursor-trail {
    width: 36px; height: 36px;
    border: 1.5px solid rgba(0,212,255,0.5);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9998;
    transition: transform 0.3s ease, width 0.3s, height 0.3s;
  }
  body:hover .cursor { transform: scale(1); }

  /* CANVAS BG */
  #canvas-bg {
    position: fixed; top: 0; left: 0;
    width: 100%; height: 100%;
    z-index: 0; opacity: 0.4;
  }

  /* NAV */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    display: flex; align-items: center; justify-content: space-between;
    padding: 1.5rem 4rem;
    backdrop-filter: blur(20px);
    background: rgba(4,8,16,0.7);
    border-bottom: 1px solid rgba(0,212,255,0.08);
    transition: padding 0.3s;
  }
  .nav-logo {
    font-family: 'Syne', sans-serif;
    font-size: 1.5rem; font-weight: 800;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    letter-spacing: -0.5px;
  }
  .nav-links { display: flex; gap: 2.5rem; list-style: none; }
  .nav-links a {
    color: var(--muted); text-decoration: none;
    font-size: 0.85rem; font-weight: 500; letter-spacing: 0.1em;
    text-transform: uppercase;
    transition: color 0.3s;
    position: relative;
  }
  .nav-links a::after {
    content: ''; position: absolute; bottom: -4px; left: 0;
    width: 0; height: 1px; background: var(--accent);
    transition: width 0.3s;
  }
  .nav-links a:hover { color: var(--accent); }
  .nav-links a:hover::after { width: 100%; }
  .nav-cta {
    padding: 0.5rem 1.5rem;
    border: 1px solid var(--accent);
    color: var(--accent);
    border-radius: 50px;
    font-size: 0.8rem; font-weight: 500;
    text-decoration: none; letter-spacing: 0.05em;
    transition: all 0.3s;
  }
  .nav-cta:hover {
    background: var(--accent); color: var(--bg);
    box-shadow: 0 0 30px rgba(0,212,255,0.4);
  }

  /* SECTIONS */
  section { position: relative; z-index: 1; }

  /* HERO */
  #hero {
    min-height: 100vh;
    display: flex; align-items: center;
    padding: 8rem 4rem 4rem;
    position: relative; overflow: hidden;
  }
  .hero-content { max-width: 700px; }
  .hero-badge {
    display: inline-flex; align-items: center; gap: 0.5rem;
    background: rgba(0,212,255,0.08);
    border: 1px solid rgba(0,212,255,0.2);
    padding: 0.4rem 1rem; border-radius: 50px;
    font-size: 0.78rem; font-weight: 500; letter-spacing: 0.1em;
    color: var(--accent); text-transform: uppercase;
    margin-bottom: 2rem;
    animation: fadeUp 0.8s ease both;
  }
  .hero-badge::before {
    content: ''; width: 6px; height: 6px;
    background: var(--accent); border-radius: 50%;
    animation: pulse 2s infinite;
  }
  @keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.5; transform: scale(1.3); }
  }
  .hero-name {
    font-family: 'Syne', sans-serif;
    font-size: clamp(3rem, 8vw, 6rem);
    font-weight: 800; line-height: 1;
    letter-spacing: -2px;
    animation: fadeUp 0.8s 0.1s ease both;
  }
  .hero-name .line1 { display: block; color: var(--text); }
  .hero-name .line2 {
    display: block;
    background: linear-gradient(135deg, var(--accent) 0%, var(--accent2) 50%, var(--accent3) 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-size: 200% auto;
    animation: fadeUp 0.8s 0.1s ease both, gradientShift 4s infinite alternate;
  }
  @keyframes gradientShift {
    0% { background-position: 0% 50%; }
    100% { background-position: 100% 50%; }
  }
  .hero-role {
    font-size: 1.1rem; color: var(--muted); font-weight: 300;
    margin: 1.5rem 0 2.5rem;
    line-height: 1.7;
    animation: fadeUp 0.8s 0.2s ease both;
  }
  .hero-role span { color: var(--accent); font-weight: 500; }
  .hero-btns {
    display: flex; gap: 1rem; flex-wrap: wrap;
    animation: fadeUp 0.8s 0.3s ease both;
  }
  .btn-primary {
    padding: 0.9rem 2.5rem;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    color: white; border: none; border-radius: 50px;
    font-size: 0.9rem; font-weight: 600; letter-spacing: 0.05em;
    cursor: none; text-decoration: none;
    transition: all 0.3s;
    position: relative; overflow: hidden;
  }
  .btn-primary::before {
    content: ''; position: absolute; inset: 0;
    background: linear-gradient(135deg, rgba(255,255,255,0.2), transparent);
    opacity: 0; transition: opacity 0.3s;
  }
  .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 20px 40px rgba(0,212,255,0.3); }
  .btn-primary:hover::before { opacity: 1; }
  .btn-outline {
    padding: 0.9rem 2.5rem;
    border: 1px solid var(--border);
    color: var(--text); border-radius: 50px;
    font-size: 0.9rem; font-weight: 500;
    cursor: none; text-decoration: none;
    transition: all 0.3s;
    backdrop-filter: blur(10px);
  }
  .btn-outline:hover {
    border-color: var(--accent); color: var(--accent);
    box-shadow: var(--glow);
  }

  .hero-stats {
    display: flex; gap: 3rem; margin-top: 5rem;
    animation: fadeUp 0.8s 0.4s ease both;
  }
  .stat-item { text-align: left; }
  .stat-num {
    font-family: 'Syne', sans-serif;
    font-size: 2.5rem; font-weight: 800;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  }
  .stat-label { font-size: 0.78rem; color: var(--muted); letter-spacing: 0.1em; text-transform: uppercase; margin-top: 0.2rem; }

  .hero-visual {
    position: absolute; right: 0; top: 50%;
    transform: translateY(-50%);
    width: 45vw; height: 100%;
    display: flex; align-items: center; justify-content: center;
  }

  /* FLOATING ORBS */
  .orb {
    position: absolute; border-radius: 50%;
    filter: blur(60px); animation: float 8s infinite ease-in-out;
  }
  .orb-1 {
    width: 400px; height: 400px;
    background: radial-gradient(circle, rgba(0,212,255,0.15) 0%, transparent 70%);
    right: -100px; top: 10%;
    animation-delay: 0s;
  }
  .orb-2 {
    width: 300px; height: 300px;
    background: radial-gradient(circle, rgba(124,58,237,0.2) 0%, transparent 70%);
    right: 20%; top: 50%;
    animation-delay: -3s;
  }
  .orb-3 {
    width: 250px; height: 250px;
    background: radial-gradient(circle, rgba(245,158,11,0.12) 0%, transparent 70%);
    left: 10%; bottom: 10%;
    animation-delay: -5s;
  }
  @keyframes float {
    0%, 100% { transform: translate(0, 0) scale(1); }
    33% { transform: translate(20px, -30px) scale(1.05); }
    66% { transform: translate(-15px, 20px) scale(0.95); }
  }

  /* SECTION COMMON */
  .section-header {
    text-align: center; margin-bottom: 5rem;
  }
  .section-tag {
    font-size: 0.75rem; font-weight: 600; letter-spacing: 0.2em;
    text-transform: uppercase; color: var(--accent);
    margin-bottom: 1rem; display: block;
  }
  .section-title {
    font-family: 'Syne', sans-serif;
    font-size: clamp(2rem, 4vw, 3.5rem);
    font-weight: 800; letter-spacing: -1px;
    line-height: 1.1;
  }
  .section-title .highlight {
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  }

  /* ABOUT */
  #about { padding: 10rem 4rem; }
  .about-grid {
    display: grid; grid-template-columns: 1fr 1fr; gap: 6rem;
    max-width: 1200px; margin: 0 auto; align-items: center;
  }
  .about-avatar-wrap {
    position: relative; display: flex; justify-content: center;
  }
  .avatar-ring {
    width: 320px; height: 320px;
    position: relative;
    animation: spinRing 20s linear infinite;
  }
  @keyframes spinRing {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }
  .avatar-ring svg { width: 100%; height: 100%; }
  .avatar-center {
    position: absolute; inset: 20px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--bg2), var(--bg3));
    display: flex; align-items: center; justify-content: center;
    border: 2px solid rgba(0,212,255,0.2);
    font-family: 'Syne', sans-serif;
    font-size: 5rem; font-weight: 800;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  }
  .about-info-chips {
    display: flex; flex-wrap: wrap; gap: 0.75rem; margin-bottom: 2rem;
  }
  .chip {
    display: flex; align-items: center; gap: 0.4rem;
    padding: 0.4rem 0.9rem;
    background: rgba(0,212,255,0.05);
    border: 1px solid rgba(0,212,255,0.15);
    border-radius: 50px; font-size: 0.82rem; color: var(--muted);
  }
  .chip .icon { font-size: 0.9rem; }
  .about-bio {
    font-size: 1rem; line-height: 1.9; color: var(--muted);
    margin-bottom: 2rem;
  }
  .about-bio strong { color: var(--text); font-weight: 500; }
  .about-tags { display: flex; flex-wrap: wrap; gap: 0.5rem; }
  .tag {
    padding: 0.3rem 0.8rem;
    background: rgba(124,58,237,0.1);
    border: 1px solid rgba(124,58,237,0.2);
    border-radius: 4px; font-size: 0.78rem;
    color: #a78bfa; font-weight: 500;
  }

  /* SKILLS */
  #skills { padding: 10rem 4rem; background: rgba(8,15,30,0.5); }
  .skills-grid {
    display: grid; grid-template-columns: repeat(3, 1fr); gap: 2rem;
    max-width: 1100px; margin: 0 auto;
  }
  .skill-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 20px; padding: 2rem;
    backdrop-filter: blur(20px);
    transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    position: relative; overflow: hidden;
  }
  .skill-card::before {
    content: ''; position: absolute;
    top: 0; left: 0; right: 0; height: 1px;
    background: linear-gradient(90deg, transparent, var(--accent), transparent);
    opacity: 0; transition: opacity 0.3s;
  }
  .skill-card:hover {
    transform: translateY(-8px);
    border-color: rgba(0,212,255,0.4);
    box-shadow: 0 30px 60px rgba(0,0,0,0.5), var(--glow);
  }
  .skill-card:hover::before { opacity: 1; }
  .skill-card-icon {
    width: 50px; height: 50px; border-radius: 14px;
    display: flex; align-items: center; justify-content: center;
    font-size: 1.5rem; margin-bottom: 1.2rem;
  }
  .skill-card h3 {
    font-family: 'Syne', sans-serif;
    font-size: 1.1rem; font-weight: 700; margin-bottom: 1.5rem;
  }
  .skill-bars { display: flex; flex-direction: column; gap: 1rem; }
  .skill-bar-item { }
  .skill-bar-label {
    display: flex; justify-content: space-between;
    font-size: 0.82rem; color: var(--muted);
    margin-bottom: 0.5rem;
  }
  .skill-bar-label span:last-child { color: var(--accent); }
  .skill-bar-track {
    height: 4px; background: rgba(255,255,255,0.06);
    border-radius: 4px; overflow: hidden;
  }
  .skill-bar-fill {
    height: 100%; border-radius: 4px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    width: 0%; transition: width 1.5s cubic-bezier(0.23, 1, 0.32, 1);
    box-shadow: 0 0 10px rgba(0,212,255,0.5);
  }

  /* PROJECTS */
  #projects { padding: 10rem 4rem; }
  .projects-grid {
    display: grid; grid-template-columns: repeat(3, 1fr); gap: 2rem;
    max-width: 1200px; margin: 0 auto;
  }
  .project-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 24px; padding: 2.5rem 2rem;
    backdrop-filter: blur(20px);
    transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    position: relative; overflow: hidden;
    display: flex; flex-direction: column;
  }
  .project-card::after {
    content: ''; position: absolute;
    bottom: 0; left: 0; right: 0; height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2), var(--accent3));
    transform: scaleX(0); transition: transform 0.4s;
    transform-origin: left;
  }
  .project-card:hover {
    transform: translateY(-10px);
    border-color: rgba(0,212,255,0.3);
    box-shadow: 0 40px 80px rgba(0,0,0,0.6), 0 0 60px rgba(0,212,255,0.1);
  }
  .project-card:hover::after { transform: scaleX(1); }
  .project-emoji {
    font-size: 2.5rem; margin-bottom: 1.5rem;
    display: block;
    animation: wobble 3s infinite ease-in-out;
  }
  @keyframes wobble {
    0%, 100% { transform: rotate(-5deg); }
    50% { transform: rotate(5deg); }
  }
  .project-label {
    font-size: 0.7rem; letter-spacing: 0.15em; text-transform: uppercase;
    color: var(--accent); font-weight: 600; margin-bottom: 0.75rem;
  }
  .project-title {
    font-family: 'Syne', sans-serif;
    font-size: 1.3rem; font-weight: 700; margin-bottom: 1rem; line-height: 1.3;
  }
  .project-desc {
    font-size: 0.88rem; color: var(--muted); line-height: 1.7;
    flex: 1; margin-bottom: 1.5rem;
  }
  .project-techs { display: flex; flex-wrap: wrap; gap: 0.4rem; }
  .tech-pill {
    padding: 0.25rem 0.65rem;
    background: rgba(0,212,255,0.06);
    border: 1px solid rgba(0,212,255,0.12);
    border-radius: 50px; font-size: 0.72rem;
    color: var(--muted); font-weight: 500;
  }

  /* CONTACT */
  #contact { padding: 10rem 4rem; background: rgba(8,15,30,0.5); }
  .contact-inner {
    max-width: 900px; margin: 0 auto;
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 32px; padding: 5rem;
    backdrop-filter: blur(30px);
    text-align: center;
    position: relative; overflow: hidden;
  }
  .contact-inner::before {
    content: ''; position: absolute;
    top: -100px; left: 50%; transform: translateX(-50%);
    width: 400px; height: 400px;
    background: radial-gradient(circle, rgba(0,212,255,0.08) 0%, transparent 70%);
    pointer-events: none;
  }
  .contact-title {
    font-family: 'Syne', sans-serif;
    font-size: clamp(2rem, 4vw, 3rem); font-weight: 800; letter-spacing: -1px;
    margin-bottom: 1rem;
  }
  .contact-sub { color: var(--muted); font-size: 1rem; line-height: 1.7; margin-bottom: 3rem; }
  .contact-links {
    display: flex; flex-wrap: wrap; justify-content: center; gap: 1rem;
    margin-bottom: 3rem;
  }
  .contact-link {
    display: flex; align-items: center; gap: 0.6rem;
    padding: 0.75rem 1.75rem;
    border: 1px solid var(--border); border-radius: 50px;
    color: var(--text); text-decoration: none;
    font-size: 0.88rem; font-weight: 500;
    transition: all 0.3s; backdrop-filter: blur(10px);
  }
  .contact-link:hover {
    border-color: var(--accent); color: var(--accent);
    transform: translateY(-3px);
    box-shadow: var(--glow);
  }
  .contact-email {
    font-family: 'Syne', sans-serif;
    font-size: 1.5rem; font-weight: 700;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    text-decoration: none; display: inline-block;
    transition: opacity 0.3s;
  }
  .contact-email:hover { opacity: 0.8; }

  /* FOOTER */
  footer {
    padding: 2rem 4rem;
    border-top: 1px solid rgba(0,212,255,0.06);
    display: flex; justify-content: space-between; align-items: center;
    position: relative; z-index: 1;
  }
  footer p { font-size: 0.8rem; color: var(--muted); }

  /* SCROLL REVEAL */
  .reveal {
    opacity: 0; transform: translateY(40px);
    transition: all 0.8s cubic-bezier(0.23, 1, 0.32, 1);
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* GLITCH NAME */
  .glitch {
    position: relative;
  }
  .glitch::before, .glitch::after {
    content: attr(data-text);
    position: absolute; top: 0; left: 0;
    width: 100%; height: 100%;
    font-family: 'Syne', sans-serif;
    font-size: inherit; font-weight: 800;
  }
  .glitch::before {
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    left: 2px; animation: glitch1 4s infinite steps(1);
    clip-path: polygon(0 0, 100% 0, 100% 45%, 0 45%);
  }
  .glitch::after {
    background: linear-gradient(135deg, var(--accent3), var(--accent));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    left: -2px; animation: glitch2 4s infinite steps(1);
    clip-path: polygon(0 55%, 100% 55%, 100% 100%, 0 100%);
  }
  @keyframes glitch1 {
    0%, 95%, 100% { transform: translate(0); opacity: 0; }
    96% { transform: translate(3px, 0); opacity: 1; }
    97% { transform: translate(-3px, 0); opacity: 1; }
    98% { transform: translate(0, 2px); opacity: 0; }
  }
  @keyframes glitch2 {
    0%, 93%, 100% { transform: translate(0); opacity: 0; }
    94% { transform: translate(-3px, 0); opacity: 1; }
    95% { transform: translate(3px, -1px); opacity: 1; }
    96% { transform: translate(0); opacity: 0; }
  }

  /* TYPEWRITER */
  .typewriter { border-right: 2px solid var(--accent); white-space: nowrap; overflow: hidden; }

  /* GRID LINES BG */
  .grid-overlay {
    position: fixed; inset: 0;
    background-image:
      linear-gradient(rgba(0,212,255,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,212,255,0.03) 1px, transparent 1px);
    background-size: 60px 60px;
    pointer-events: none; z-index: 0;
  }

  @media (max-width: 768px) {
    nav { padding: 1rem 1.5rem; }
    #hero { padding: 8rem 1.5rem 4rem; }
    .hero-stats { gap: 1.5rem; }
    #about, #skills, #projects, #contact { padding: 6rem 1.5rem; }
    .about-grid { grid-template-columns: 1fr; gap: 3rem; }
    .skills-grid { grid-template-columns: 1fr; }
    .projects-grid { grid-template-columns: 1fr; }
    .contact-inner { padding: 3rem 1.5rem; }
    footer { flex-direction: column; gap: 1rem; text-align: center; }
    .nav-links { display: none; }
    .hero-visual { display: none; }
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-trail" id="cursorTrail"></div>
<div class="grid-overlay"></div>
<canvas id="canvas-bg"></canvas>

<!-- NAV -->
<nav id="nav">
  <div class="nav-logo">SK</div>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#skills">Skills</a></li>
    <li><a href="#projects">Projects</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <a href="mailto:santhosh.sd0403@gmail.com" class="nav-cta">Hire Me</a>
</nav>

<!-- ORBS -->
<div class="orb orb-1"></div>
<div class="orb orb-2"></div>
<div class="orb orb-3"></div>

<!-- HERO -->
<section id="hero">
  <div class="hero-content">
    <div class="hero-badge">✦ Open to Opportunities · Fresher</div>
    <h1 class="hero-name">
      <span class="line1">Santhosh</span>
      <span class="line2 glitch" data-text="Kumar K">Kumar K</span>
    </h1>
    <p class="hero-role">
      <span id="typewriter"></span><br>
      B.Tech CSE Graduate · Building with purpose —
      software that <span>thinks</span>, data that <span>speaks</span>, design that <span>resonates</span>.
    </p>
    <div class="hero-btns">
      <a href="#projects" class="btn-primary">View My Work</a>
      <a href="#contact" class="btn-outline">Get In Touch</a>
    </div>
    <div class="hero-stats">
      <div class="stat-item">
        <div class="stat-num" data-target="3">0</div>
        <div class="stat-label">Tech Skills+</div>
      </div>
      <div class="stat-item">
        <div class="stat-num" data-target="3">0</div>
        <div class="stat-label">Projects</div>
      </div>
      <div class="stat-item">
        <div class="stat-num" data-target="2">0</div>
        <div class="stat-label">Roles</div>
      </div>
    </div>
  </div>
</section>

<!-- ABOUT -->
<section id="about">
  <div class="section-header reveal">
    <span class="section-tag">Who I Am</span>
    <h2 class="section-title">About <span class="highlight">Me</span></h2>
  </div>
  <div class="about-grid">
    <div class="about-avatar-wrap reveal">
      <div class="avatar-ring">
        <svg viewBox="0 0 320 320" fill="none" xmlns="http://www.w3.org/2000/svg">
          <circle cx="160" cy="160" r="155" stroke="url(#ringGrad)" stroke-width="1.5" stroke-dasharray="8 6"/>
          <circle cx="160" cy="5" r="5" fill="#00d4ff"/>
          <circle cx="315" cy="160" r="3" fill="#7c3aed"/>
          <circle cx="160" cy="315" r="4" fill="#f59e0b"/>
          <defs>
            <linearGradient id="ringGrad" x1="0" y1="0" x2="320" y2="320" gradientUnits="userSpaceOnUse">
              <stop stop-color="#00d4ff"/>
              <stop offset="0.5" stop-color="#7c3aed"/>
              <stop offset="1" stop-color="#f59e0b"/>
            </linearGradient>
          </defs>
        </svg>
        <div class="avatar-center">SK</div>
      </div>
    </div>
    <div class="reveal">
      <div class="about-info-chips">
        <div class="chip"><span class="icon">📍</span> Pondicherry, India</div>
        <div class="chip"><span class="icon">🎓</span> B.Tech CSE</div>
        <div class="chip"><span class="icon">💼</span> Open to Work</div>
        <div class="chip"><span class="icon">🌐</span> Indian</div>
      </div>
      <p class="about-bio">
        I'm a <strong>B.Tech Computer Science Engineering graduate</strong> and a passionate fresher ready to make my mark in the tech world. I bring a dual edge — <strong>software development skills</strong> paired with a <strong>creative flair for design</strong>.
      </p>
      <p class="about-bio">
        As a <strong>freelancer in logo design and content creation</strong>, I've developed a strong eye for detail. On the technical side, I enjoy building applications, working with data, and solving real-world problems with code.
      </p>
      <div class="about-tags">
        <span class="tag">Problem Solver</span>
        <span class="tag">Creative Thinker</span>
        <span class="tag">Data-Driven</span>
        <span class="tag">Logo Designer</span>
        <span class="tag">Fast Learner</span>
      </div>
    </div>
  </div>
</section>

<!-- SKILLS -->
<section id="skills">
  <div class="section-header reveal">
    <span class="section-tag">What I Know</span>
    <h2 class="section-title">Skills & <span class="highlight">Technologies</span></h2>
  </div>
  <div class="skills-grid">
    <div class="skill-card reveal">
      <div class="skill-card-icon" style="background:rgba(0,212,255,0.1)">💻</div>
      <h3>Programming</h3>
      <div class="skill-bars">
        <div class="skill-bar-item">
          <div class="skill-bar-label"><span>Java</span><span>80%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill" data-width="80"></div></div>
        </div>
        <div class="skill-bar-item">
          <div class="skill-bar-label"><span>Python</span><span>78%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill" data-width="78"></div></div>
        </div>
        <div class="skill-bar-item">
          <div class="skill-bar-label"><span>MySQL</span><span>75%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill" data-width="75"></div></div>
        </div>
      </div>
    </div>
    <div class="skill-card reveal">
      <div class="skill-card-icon" style="background:rgba(124,58,237,0.1)">🌐</div>
      <h3>Web Technologies</h3>
      <div class="skill-bars">
        <div class="skill-bar-item">
          <div class="skill-bar-label"><span>HTML</span><span>82%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill" data-width="82"></div></div>
        </div>
        <div class="skill-bar-item">
          <div class="skill-bar-label"><span>CSS</span><span>78%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill" data-width="78"></div></div>
        </div>
        <div class="skill-bar-item">
          <div class="skill-bar-label"><span>GitHub</span><span>72%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill" data-width="72"></div></div>
        </div>
      </div>
    </div>
    <div class="skill-card reveal">
      <div class="skill-card-icon" style="background:rgba(245,158,11,0.1)">🎨</div>
      <h3>Creative & Design</h3>
      <div class="skill-bars">
        <div class="skill-bar-item">
          <div class="skill-bar-label"><span>Logo Design</span><span>85%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill" data-width="85"></div></div>
        </div>
        <div class="skill-bar-item">
          <div class="skill-bar-label"><span>Content Prep</span><span>80%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill" data-width="80"></div></div>
        </div>
        <div class="skill-bar-item">
          <div class="skill-bar-label"><span>Visual Comm.</span><span>78%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill" data-width="78"></div></div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- PROJECTS -->
<section id="projects">
  <div class="section-header reveal">
    <span class="section-tag">What I've Built</span>
    <h2 class="section-title">Featured <span class="highlight">Projects</span></h2>
  </div>
  <div class="projects-grid">
    <div class="project-card reveal">
      <span class="project-emoji">🦷</span>
      <div class="project-label">Deep Learning · Final Year Project</div>
      <h3 class="project-title">Automated Dental Cavity Detection</h3>
      <p class="project-desc">Developing an automated dental cavity detection system using deep learning and image processing. Uses CNNs to analyse dental X-ray images and Word2Vec embeddings to integrate clinical text data, improving diagnostic accuracy.</p>
      <div class="project-techs">
        <span class="tech-pill">Python</span>
        <span class="tech-pill">CNN</span>
        <span class="tech-pill">Deep Learning</span>
        <span class="tech-pill">Word2Vec</span>
        <span class="tech-pill">Image Processing</span>
      </div>
    </div>
    <div class="project-card reveal">
      <span class="project-emoji" style="animation-delay:0.5s">🎨</span>
      <div class="project-label">Creative Design · Freelance</div>
      <h3 class="project-title">Freelance Logo Design</h3>
      <p class="project-desc">Creating professional logo designs and brand identities for clients as a freelancer. Delivering custom, visually compelling logos tailored to each client's brand personality and business needs.</p>
      <div class="project-techs">
        <span class="tech-pill">Logo Design</span>
        <span class="tech-pill">Branding</span>
        <span class="tech-pill">Visual Identity</span>
      </div>
    </div>
    <div class="project-card reveal">
      <span class="project-emoji" style="animation-delay:1s">📝</span>
      <div class="project-label">Content Creation · Freelance</div>
      <h3 class="project-title">Content Preparation</h3>
      <p class="project-desc">Preparing structured, engaging content for various platforms and clients — including written content, presentations, and digital material tailored to audience and purpose.</p>
      <div class="project-techs">
        <span class="tech-pill">Content Writing</span>
        <span class="tech-pill">Presentation</span>
        <span class="tech-pill">Digital Content</span>
      </div>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="contact-inner reveal">
    <h2 class="contact-title">Let's Work <span style="background:linear-gradient(135deg,#00d4ff,#7c3aed);-webkit-background-clip:text;-webkit-text-fill-color:transparent">Together</span></h2>
    <p class="contact-sub">Open to full-time roles, internships, freelance projects, and collaborative opportunities in software development, data analytics, and creative design.</p>
    <div class="contact-links">
      <a href="https://github.com/santhoshkumar0304" target="_blank" class="contact-link">🐙 GitHub</a>
      <a href="https://www.linkedin.com/in/santhosh-kumar-k-7624ab305" target="_blank" class="contact-link">💼 LinkedIn</a>
      <a href="tel:+918056492986" class="contact-link">📞 +91 8056492986</a>
      <a href="#" class="contact-link">📍 Pondicherry, India</a>
    </div>
    <a href="mailto:santhosh.sd0403@gmail.com" class="contact-email">santhosh.sd0403@gmail.com</a>
  </div>
</section>

<footer>
  <p>© 2026 Santhosh Kumar K · Pondicherry, India</p>
  <p style="color:rgba(107,127,168,0.5);font-size:0.75rem">Software Developer · Data Analyst · Designer</p>
</footer>

<script>
// CURSOR
const cursor = document.getElementById('cursor');
const trail = document.getElementById('cursorTrail');
let mx = 0, my = 0, tx = 0, ty = 0;
document.addEventListener('mousemove', e => {
  mx = e.clientX; my = e.clientY;
  cursor.style.transform = `translate(${mx-6}px, ${my-6}px)`;
});
function animateTrail() {
  tx += (mx - tx) * 0.1;
  ty += (my - ty) * 0.1;
  trail.style.transform = `translate(${tx-18}px, ${ty-18}px)`;
  requestAnimationFrame(animateTrail);
}
animateTrail();
document.querySelectorAll('a, button').forEach(el => {
  el.addEventListener('mouseenter', () => {
    cursor.style.transform += ' scale(2)';
    trail.style.width = '60px'; trail.style.height = '60px';
  });
  el.addEventListener('mouseleave', () => {
    trail.style.width = '36px'; trail.style.height = '36px';
  });
});

// PARTICLE CANVAS
const canvas = document.getElementById('canvas-bg');
const ctx = canvas.getContext('2d');
let W, H, particles = [];
function resize() {
  W = canvas.width = window.innerWidth;
  H = canvas.height = window.innerHeight;
}
resize(); window.addEventListener('resize', resize);
for (let i = 0; i < 120; i++) {
  particles.push({
    x: Math.random() * W, y: Math.random() * H,
    vx: (Math.random()-0.5)*0.3, vy: (Math.random()-0.5)*0.3,
    r: Math.random() * 1.5 + 0.5,
    alpha: Math.random() * 0.5 + 0.1,
    color: ['#00d4ff','#7c3aed','#f59e0b'][Math.floor(Math.random()*3)]
  });
}
function drawParticles() {
  ctx.clearRect(0, 0, W, H);
  particles.forEach(p => {
    p.x += p.vx; p.y += p.vy;
    if (p.x < 0) p.x = W; if (p.x > W) p.x = 0;
    if (p.y < 0) p.y = H; if (p.y > H) p.y = 0;
    ctx.beginPath();
    ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
    ctx.fillStyle = p.color;
    ctx.globalAlpha = p.alpha;
    ctx.fill();
  });
  // Draw connections
  ctx.globalAlpha = 1;
  for (let i = 0; i < particles.length; i++) {
    for (let j = i+1; j < particles.length; j++) {
      const dx = particles[i].x - particles[j].x;
      const dy = particles[i].y - particles[j].y;
      const dist = Math.sqrt(dx*dx+dy*dy);
      if (dist < 100) {
        ctx.beginPath();
        ctx.moveTo(particles[i].x, particles[i].y);
        ctx.lineTo(particles[j].x, particles[j].y);
        ctx.strokeStyle = '#00d4ff';
        ctx.globalAlpha = (1 - dist/100) * 0.08;
        ctx.lineWidth = 0.5;
        ctx.stroke();
      }
    }
  }
  requestAnimationFrame(drawParticles);
}
drawParticles();

// TYPEWRITER
const roles = ['Developer & Data Analyst', 'Creative Designer', 'Problem Solver', 'Fresher · Open to Work'];
let ri = 0, ci = 0, deleting = false;
const tw = document.getElementById('typewriter');
function typewrite() {
  const cur = roles[ri];
  if (!deleting) {
    tw.textContent = cur.slice(0, ++ci);
    if (ci === cur.length) { deleting = true; setTimeout(typewrite, 2000); return; }
  } else {
    tw.textContent = cur.slice(0, --ci);
    if (ci === 0) { deleting = false; ri = (ri+1) % roles.length; }
  }
  setTimeout(typewrite, deleting ? 50 : 100);
}
typewrite();

// SCROLL REVEAL
const revealEls = document.querySelectorAll('.reveal');
const observer = new IntersectionObserver(entries => {
  entries.forEach((e, i) => {
    if (e.isIntersecting) {
      setTimeout(() => e.target.classList.add('visible'), 100);
    }
  });
}, { threshold: 0.1 });
revealEls.forEach(el => observer.observe(el));

// SKILL BARS
const barObserver = new IntersectionObserver(entries => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.querySelectorAll('.skill-bar-fill').forEach(bar => {
        bar.style.width = bar.dataset.width + '%';
      });
    }
  });
}, { threshold: 0.3 });
document.querySelectorAll('.skill-card').forEach(card => barObserver.observe(card));

// COUNTER
const counters = document.querySelectorAll('.stat-num[data-target]');
const countObserver = new IntersectionObserver(entries => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const el = entry.target;
      const target = +el.dataset.target;
      let count = 0;
      const step = target / 40;
      const interval = setInterval(() => {
        count += step;
        if (count >= target) { el.textContent = target + '+'; clearInterval(interval); }
        else { el.textContent = Math.floor(count); }
      }, 40);
      countObserver.unobserve(el);
    }
  });
}, { threshold: 0.5 });
counters.forEach(c => countObserver.observe(c));

// NAV SCROLL
window.addEventListener('scroll', () => {
  const nav = document.getElementById('nav');
  nav.style.padding = window.scrollY > 50 ? '1rem 4rem' : '1.5rem 4rem';
});
</script>
</body>
</html>
