# syedzakir.com
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>syd.zkir</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#0A1420;
    --surface:#101D2E;
    --text:#E7EEF5;
    --text-dim:#7C93A8;
    --line:#2A3F55;
    --cyan:#6EC1E4;
    --rust:#E0794F;
    --green:#7FB88F;
    --font-display:'Space Grotesk', sans-serif;
    --font-body:'Inter', sans-serif;
    --font-mono:'JetBrains Mono', monospace;
  }
  *{margin:0;padding:0;box-sizing:border-box;}
  html{scroll-behavior:smooth;}
  body{
    position:relative;
    min-height:100vh;
    overflow-x:hidden;
    isolation:isolate;
    background:var(--bg);
    color:var(--text);font-family:var(--font-body);line-height:1.5;
    -webkit-font-smoothing:antialiased;
  }
  body::before,
  body::after{
    content:'';
    position:fixed;
    inset:0;
    pointer-events:none;
    z-index:-1;
  }
  body::before{
    background:
      radial-gradient(circle at 20% 20%, rgba(110,193,228,0.24), transparent 18%),
      radial-gradient(circle at 80% 10%, rgba(224,121,79,0.18), transparent 22%),
      radial-gradient(circle at 60% 70%, rgba(127,184,143,0.12), transparent 24%),
      radial-gradient(circle at 10% 80%, rgba(110,193,228,0.1), transparent 16%);
    filter:blur(20px);
    animation:ambientDrift 18s ease-in-out infinite alternate;
  }
  body::after{
    background:
      repeating-linear-gradient(0deg, rgba(110,193,228,0.035) 0px, rgba(110,193,228,0.035) 1px, transparent 1px, transparent 40px),
      repeating-linear-gradient(90deg, rgba(110,193,228,0.035) 0px, rgba(110,193,228,0.035) 1px, transparent 1px, transparent 40px);
    opacity:.9;
    animation:gridPulse 12s linear infinite;
  }
  a{color:inherit;text-decoration:none;}
  ::selection{background:var(--rust);color:#0A1420;}
  .wrap{max-width:960px;margin:0 auto;padding:0 32px;position:relative;}

  /* reticle cursor */
  #reticle{
    position:fixed;top:0;left:0;width:22px;height:22px;pointer-events:none;z-index:9999;
    transform:translate(-50%,-50%);transition:opacity .15s ease;
  }
  #reticle::before, #reticle::after{content:'';position:absolute;background:var(--cyan);}
  #reticle::before{top:50%;left:0;width:100%;height:1px;transform:translateY(-50%);}
  #reticle::after{left:50%;top:0;width:1px;height:100%;transform:translateX(-50%);}
  #coord{
    position:fixed;top:0;left:0;pointer-events:none;z-index:9999;
    font-family:var(--font-mono);font-size:10px;color:var(--cyan);
    transform:translate(14px, -22px);opacity:.75;white-space:nowrap;
  }
  @media (pointer:coarse){ #reticle, #coord{display:none;} }
  body{cursor:none;}
  @media (pointer:coarse){ body{cursor:auto;} }
  @media (prefers-reduced-motion: reduce){
    *{animation:none !important;transition:none !important;}
    #reticle,#coord{display:none;} body{cursor:auto;}
  }

  /* corner bracket component — the recurring signature shape */
  .bracket{position:relative;}
  .bracket::before, .bracket::after,
  .bracket .bl, .bracket .br{
    content:'';position:absolute;width:12px;height:12px;
    border-color:var(--line);border-style:solid;border-width:0;
    transition:border-color .25s ease, width .25s ease, height .25s ease;
  }
  .bracket::before{top:-1px;left:-1px;border-top-width:2px;border-left-width:2px;}
  .bracket::after{top:-1px;right:-1px;border-top-width:2px;border-right-width:2px;}
  .bracket .bl{bottom:-1px;left:-1px;border-bottom-width:2px;border-left-width:2px;}
  .bracket .br{bottom:-1px;right:-1px;border-bottom-width:2px;border-right-width:2px;}
  .bracket:hover::before, .bracket:hover::after, .bracket:hover .bl, .bracket:hover .br{
    border-color:var(--cyan);width:18px;height:18px;
  }

  @keyframes riseIn{from{opacity:0;transform:translateY(18px);} to{opacity:1;transform:translateY(0);}}
  @keyframes ambientDrift{
    0%{transform:translate3d(-2%, -1%, 0) scale(1);} 
    50%{transform:translate3d(2%, 1.5%, 0) scale(1.06);} 
    100%{transform:translate3d(-1%, 2%, 0) scale(1.02);} 
  }
  @keyframes gridPulse{
    0%{transform:translateY(0) scale(1); opacity:.75;}
    50%{transform:translateY(10px) scale(1.01); opacity:.9;}
    100%{transform:translateY(0) scale(1); opacity:.75;}
  }
  .rise{animation:riseIn .7s ease both;}
  .d1{animation-delay:.05s;} .d2{animation-delay:.18s;} .d3{animation-delay:.32s;} .d4{animation-delay:.46s;}

  nav{position:sticky;top:0;z-index:10;background:rgba(10,20,32,0.88);backdrop-filter:blur(8px);border-bottom:1px solid var(--line);}
  nav .wrap{display:flex;align-items:center;justify-content:space-between;height:64px;}
  .logo{font-family:var(--font-mono);font-size:13px;color:var(--cyan);display:flex;align-items:center;gap:8px;}
  .logo svg{width:16px;height:16px;}
  .navlinks{display:flex;gap:32px;font-family:var(--font-mono);font-size:12px;text-transform:uppercase;letter-spacing:0.08em;color:var(--text-dim);}
  .navlinks a{position:relative;padding-bottom:4px;transition:color .2s;}
  .navlinks a::after{content:'';position:absolute;left:0;bottom:0;width:100%;height:1px;background:var(--rust);transform:scaleX(0);transform-origin:left;transition:transform .25s ease;}
  .navlinks a:hover{color:var(--text);}
  .navlinks a:hover::after{transform:scaleX(1);}

  header.hero{padding:110px 0 90px;border-bottom:1px solid var(--line);}
  .spec-label{font-family:var(--font-mono);font-size:12px;color:var(--text-dim);letter-spacing:0.1em;margin-bottom:20px;}
  .spec-label span{color:var(--cyan);}
  h1{font-family:var(--font-display);font-weight:700;font-size:clamp(46px,7vw,80px);line-height:1.02;letter-spacing:-0.01em;}
  .role-tags{display:flex;gap:10px;flex-wrap:wrap;margin-top:22px;}
  .role-tag{font-family:var(--font-mono);font-size:12px;color:var(--cyan);border:1px solid var(--line);padding:5px 12px;border-radius:2px;}
  .tagline{margin-top:26px;max-width:480px;color:var(--text-dim);font-size:17px;}
  .hero-cta{margin-top:38px;display:flex;gap:20px;align-items:center;}

  .btn-primary{
    font-family:var(--font-mono);font-size:13px;color:var(--rust);
    padding:14px 26px;letter-spacing:0.03em;display:inline-block;
    transition:color .2s ease, background .2s ease;
  }
  .btn-primary:hover{background:rgba(224,121,79,0.1);}
  .btn-primary:active{transform:scale(0.98);}
  .btn-ghost{font-family:var(--font-mono);font-size:13px;color:var(--text-dim);border-bottom:1px solid var(--line);padding-bottom:2px;transition:color .2s,border-color .2s;}
  .btn-ghost:hover{color:var(--text);border-color:var(--text);}

  section{padding:96px 0;border-bottom:1px solid var(--line);}
  .eyebrow{font-family:var(--font-mono);font-size:12px;color:var(--text-dim);letter-spacing:0.1em;margin-bottom:36px;display:flex;align-items:center;gap:10px;}
  .status-dot{width:6px;height:6px;border-radius:50%;background:var(--rust);box-shadow:0 0 0 0 rgba(224,121,79,.6);animation:pulse 2.4s infinite;}
  @keyframes pulse{0%{box-shadow:0 0 0 0 rgba(224,121,79,.5);}70%{box-shadow:0 0 0 6px rgba(224,121,79,0);}100%{box-shadow:0 0 0 0 rgba(224,121,79,0);}}

  .projects{display:flex;flex-direction:column;gap:24px;}
  .project{padding:30px;border:1px solid var(--line);transition:background .25s ease, transform .25s ease;}
  .project:hover{background:var(--surface);transform:translateY(-3px);}
  .project-meta{display:flex;justify-content:space-between;align-items:center;font-family:var(--font-mono);font-size:11px;color:var(--text-dim);letter-spacing:0.05em;margin-bottom:18px;flex-wrap:wrap;gap:8px;}
  .project-meta .id{color:var(--cyan);}
  .project-title{font-family:var(--font-display);font-size:28px;font-weight:600;transition:color .2s;}
  .project:hover .project-title{color:var(--cyan);}
  .project-desc{color:var(--text-dim);font-size:15px;max-width:560px;margin-top:12px;}
  .spec-table{display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:16px;margin-top:22px;padding-top:20px;border-top:1px dashed var(--line);}
  .spec-item dt{font-family:var(--font-mono);font-size:10px;color:var(--text-dim);letter-spacing:0.08em;margin-bottom:4px;}
  .spec-item dd{font-family:var(--font-mono);font-size:12px;color:var(--text);}

  .about-grid{display:grid;grid-template-columns:220px 1fr;gap:48px;}
  .about-text{max-width:520px;font-size:16px;color:var(--text-dim);}
  .about-text p+p{margin-top:16px;}
  .about-text strong{color:var(--text);font-weight:500;}
  .profile-specs{margin-top:28px;display:grid;grid-template-columns:1fr 1fr;gap:18px 28px;}
  .profile-specs dt{font-family:var(--font-mono);font-size:10px;color:var(--cyan);letter-spacing:0.08em;margin-bottom:4px;}
  .profile-specs dd{font-family:var(--font-mono);font-size:13px;color:var(--text);}

  .milestones{display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));gap:20px;}
  .milestone{padding:22px;border:1px solid var(--line);background:rgba(16,29,46,0.65);transition:background .25s ease, transform .25s ease;}
  .milestone:hover{background:var(--surface);transform:translateY(-3px);}
  .milestone-year{font-family:var(--font-mono);font-size:11px;color:var(--cyan);letter-spacing:0.08em;margin-bottom:12px;}
  .milestone-title{font-family:var(--font-display);font-size:22px;font-weight:600;margin-bottom:8px;}
  .milestone-copy{color:var(--text-dim);font-size:14px;}

  @media (max-width:640px){
    .about-grid{grid-template-columns:1fr;gap:20px;}
    .profile-specs{grid-template-columns:1fr;}
  }

  footer{padding:96px 0 60px;}
  .transmit-box{border:1px solid var(--line);padding:36px;}
  .contact-line{font-family:var(--font-mono);font-size:15px;color:var(--text-dim);margin-bottom:28px;}
  .contact-line .rust{color:var(--rust);}
  .socials{display:flex;gap:24px;font-family:var(--font-mono);font-size:13px;}
  .socials a{color:var(--text-dim);transition:color .2s;}
  .socials a:hover{color:var(--cyan);}
  .foot-note{margin-top:64px;font-family:var(--font-mono);font-size:11px;color:#3E5066;text-align:center;}

  a:focus-visible, button:focus-visible{outline:1px solid var(--cyan);outline-offset:3px;}
</style>
</head>
<body>

<div id="reticle"></div>
<div id="coord">X:000 Y:000</div>

<nav>
  <div class="wrap">
    <div class="logo">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><circle cx="12" cy="12" r="9"/><line x1="12" y1="3" x2="12" y2="6"/><line x1="12" y1="18" x2="12" y2="21"/><line x1="3" y1="12" x2="6" y2="12"/><line x1="18" y1="12" x2="21" y2="12"/></svg>
      syd.zkir
    </div>
    <div class="navlinks">
      <a href="#work">Work</a>
      <a href="#about">About</a>
      <a href="#milestones">Milestones</a>
      <a href="#contact">Contact</a>
    </div>
  </div>
</nav>

<header class="hero">
  <div class="wrap">
    <div class="spec-label rise d1">SHEET <span>001</span> / OPERATOR PROFILE</div>
    <h1 class="rise d2">Syed Zakir Hasan</h1>
    <div class="role-tags rise d2">
      <span class="role-tag">FULL-STACK</span>
      <span class="role-tag">WEB DEV</span>
      <span class="role-tag">CYBERSECURITY</span>
      <span class="role-tag">GAME DEV</span>
    </div>
    <p class="tagline rise d3">Self-taught and endlessly curious — building across web, cybersecurity, and games because staying in one lane never worked out for me.</p>
    <div class="hero-cta rise d4">
      <a href="#work" class="btn-primary bracket">MY WORK<span class="bl"></span><span class="br"></span></a>
      <a href="#contact" class="btn-ghost">CONTACT ME HERE →</a>
    </div>
  </div>
</header>

<section id="work">
  <div class="wrap">
    <div class="eyebrow">DATASHEET // SELECTED WORK</div>
    <!-- Projects will be placed here automatically from projects.js -->
    <div class="projects" id="projects-container"></div>
  </div>
</section>

<section id="about">
  <div class="wrap">
    <div class="about-grid">
      <div class="eyebrow" style="margin-bottom:0;">OPERATOR PROFILE</div>
      <div class="about-text">
        <p>Mostly self-taught, mostly curious. I move between web development, cybersecurity, and game dev depending on whatever's pulling my attention that month — less a career plan, more a habit of picking things apart to see how they work.</p>
      </div>
    </div>
  </div>
</section>

<section id="milestones">
  <div class="wrap">
    <div class="eyebrow">MILESTONES // LEARNING TRACK</div>
    <div class="milestones">
      <div class="milestone bracket"><span class="bl"></span><span class="br"></span>
        <div class="milestone-year">2026</div>
        <div class="milestone-title">Add your first milestone</div>
        <div class="milestone-copy">This section is for documenting skills, tools, and concepts you learn over time.</div>
      </div>
    </div>
  </div>
</section>

<footer id="contact">
  <div class="wrap">
    <div class="eyebrow"><span class="status-dot"></span> SIGNAL: HEADS DOWN — LEARNING, NOT TAKING WORK</div>
    <div class="transmit-box bracket"><span class="bl"></span><span class="br"></span>
      <div class="contact-line">TRANSMIT // <span class="rust">syedzakirhasanamroha1@gmail.com</span></div>
      <div class="socials">
        <a href="https://github.com/SyedZakirHasan" target="_blank" rel="noreferrer">GitHub</a>
      </div>
    </div>
    <div class="foot-note">SHEET 001 — REV E — VER 2.4, 1 PROJECT, 0 MILESTONES.</div>
  </div>
</footer>

<script>
  /* Reticle Cursor Script */
  const reticle = document.getElementById('reticle');
  const coord = document.getElementById('coord');
  const reduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  const coarse = window.matchMedia('(pointer: coarse)').matches;

  if(!reduced && !coarse){
    window.addEventListener('mousemove', e=>{
      reticle.style.transform = `translate(${e.clientX}px, ${e.clientY}px) translate(-50%,-50%)`;
      coord.style.transform = `translate(${e.clientX + 14}px, ${e.clientY - 22}px)`;
      coord.textContent = `X:${String(e.clientX).padStart(3,'0')} Y:${String(e.clientY).padStart(3,'0')}`;
    });
  }
</script>

<!-- Load project data and automatically create project cards -->
<script src="projects.js"></script>
<script>
  const container = document.getElementById('projects-container');
  
  projectsData.forEach(proj => {
    const projectHTML = `
      <div class="project bracket"><span class="bl"></span><span class="br"></span>
        <div class="project-meta">
          <span class="id">${proj.id}</span>
          <span>${proj.status}</span>
        </div>
        <div class="project-title">${proj.title}</div>
        <div class="project-desc">${proj.description}</div>
        <dl class="spec-table">
          <div class="spec-item"><dt>STACK</dt><dd>${proj.stack}</dd></div>
          <div class="spec-item"><dt>ROLE</dt><dd>${proj.role}</dd></div>
          <div class="spec-item"><dt>YEAR</dt><dd>${proj.year}</dd></div>
        </dl>
      </div>
    `;
    container.innerHTML += projectHTML;
  });
</script>

</body>
</html>

