<!DOCTYPE html>
<html>
<head>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body { font-family: 'Inter', sans-serif; background: #050510; color: #e0e0ff; overflow-x: hidden; }

  ::-webkit-scrollbar { width: 6px; }
  ::-webkit-scrollbar-track { background: #0a0a20; }
  ::-webkit-scrollbar-thumb { background: linear-gradient(#7c3aed, #2563eb); border-radius: 3px; }

  .bg-glow { position: fixed; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 0; overflow: hidden; }
  .blob { position: absolute; border-radius: 50%; filter: blur(80px); opacity: 0.18; animation: blobFloat 8s ease-in-out infinite; }
  .blob1 { width: 500px; height: 500px; background: #7c3aed; top: -100px; left: -100px; animation-delay: 0s; }
  .blob2 { width: 400px; height: 400px; background: #2563eb; top: 40%; right: -100px; animation-delay: 3s; }
  .blob3 { width: 350px; height: 350px; background: #9333ea; bottom: 10%; left: 30%; animation-delay: 6s; }
  @keyframes blobFloat { 0%,100%{transform:translate(0,0) scale(1);} 33%{transform:translate(20px,-30px) scale(1.05);} 66%{transform:translate(-15px,20px) scale(0.97);} }

  .particles { position: fixed; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 0; }
  .particle { position: absolute; width: 2px; height: 2px; border-radius: 50%; background: #818cf8; animation: particleFloat linear infinite; opacity: 0; }
  @keyframes particleFloat { 0%{transform:translateY(100vh) translateX(0);opacity:0;} 10%{opacity:1;} 90%{opacity:1;} 100%{transform:translateY(-100px) translateX(var(--drift));opacity:0;} }

  .content { position: relative; z-index: 1; max-width: 900px; margin: 0 auto; padding: 0 20px; }

  .grid-bg { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background-image: linear-gradient(rgba(99,102,241,0.04) 1px, transparent 1px), linear-gradient(90deg, rgba(99,102,241,0.04) 1px, transparent 1px); background-size: 50px 50px; pointer-events: none; z-index: 0; }

  .hero { min-height: 100vh; display: flex; align-items: center; justify-content: center; text-align: center; padding: 60px 20px; }
  .hero-inner { max-width: 750px; }

  .avatar-wrap { position: relative; display: inline-block; margin-bottom: 32px; }
  .avatar { width: 130px; height: 130px; border-radius: 50%; background: linear-gradient(135deg, #1e1b4b, #312e81); border: 3px solid transparent; background-clip: padding-box; position: relative; display: flex; align-items: center; justify-content: center; font-size: 52px; animation: avatarPulse 3s ease-in-out infinite; }
  @keyframes avatarPulse { 0%,100%{box-shadow:0 0 20px rgba(124,58,237,0.4),0 0 60px rgba(37,99,235,0.2);} 50%{box-shadow:0 0 40px rgba(124,58,237,0.7),0 0 100px rgba(37,99,235,0.35);} }
  .avatar-ring { position: absolute; inset: -8px; border-radius: 50%; border: 2px solid transparent; background: linear-gradient(135deg, #7c3aed, #2563eb, #9333ea) border-box; -webkit-mask: linear-gradient(#fff 0 0) padding-box, linear-gradient(#fff 0 0); -webkit-mask-composite: destination-out; mask-composite: exclude; animation: ringRotate 4s linear infinite; }
  @keyframes ringRotate { from{transform:rotate(0deg);} to{transform:rotate(360deg);} }
  .status-dot { position: absolute; bottom: 8px; right: 8px; width: 18px; height: 18px; background: #22c55e; border-radius: 50%; border: 3px solid #050510; animation: statusPulse 2s ease-in-out infinite; }
  @keyframes statusPulse { 0%,100%{box-shadow:0 0 0 0 rgba(34,197,94,0.6);} 70%{box-shadow:0 0 0 10px rgba(34,197,94,0);} }

  .hero h1 { font-size: clamp(36px, 6vw, 62px); font-weight: 900; background: linear-gradient(135deg, #e0e7ff 0%, #a78bfa 40%, #60a5fa 100%); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; margin-bottom: 16px; letter-spacing: -2px; animation: fadeInUp 0.8s ease both; }
  .hero-sub { font-size: clamp(14px, 2vw, 18px); color: #94a3b8; margin-bottom: 28px; letter-spacing: 0.5px; animation: fadeInUp 0.8s 0.2s ease both; }
  .typing-wrap { font-size: clamp(16px, 2.5vw, 22px); font-weight: 600; color: #a78bfa; min-height: 40px; animation: fadeInUp 0.8s 0.4s ease both; margin-bottom: 36px; }
  .typing-cursor { border-right: 3px solid #7c3aed; animation: blink 0.7s infinite; display: inline; }
  @keyframes blink { 0%,100%{opacity:1;} 50%{opacity:0;} }

  .hero-badges { display: flex; gap: 12px; justify-content: center; flex-wrap: wrap; animation: fadeInUp 0.8s 0.6s ease both; margin-bottom: 40px; }
  .badge { padding: 8px 18px; border-radius: 50px; font-size: 13px; font-weight: 500; border: 1px solid; backdrop-filter: blur(8px); }
  .badge-purple { background: rgba(124,58,237,0.15); border-color: rgba(124,58,237,0.4); color: #c4b5fd; }
  .badge-blue { background: rgba(37,99,235,0.15); border-color: rgba(37,99,235,0.4); color: #93c5fd; }
  .badge-pink { background: rgba(147,51,234,0.15); border-color: rgba(147,51,234,0.4); color: #d8b4fe; }

  .cta-row { display: flex; gap: 16px; justify-content: center; flex-wrap: wrap; animation: fadeInUp 0.8s 0.8s ease both; }
  .btn { padding: 12px 28px; border-radius: 50px; font-size: 14px; font-weight: 600; cursor: pointer; transition: all 0.3s; border: none; letter-spacing: 0.3px; }
  .btn-primary { background: linear-gradient(135deg, #7c3aed, #2563eb); color: #fff; box-shadow: 0 0 30px rgba(124,58,237,0.4); }
  .btn-primary:hover { box-shadow: 0 0 50px rgba(124,58,237,0.7); transform: translateY(-2px); }
  .btn-outline { background: transparent; color: #a78bfa; border: 1px solid rgba(124,58,237,0.5); }
  .btn-outline:hover { background: rgba(124,58,237,0.1); transform: translateY(-2px); }

  @keyframes fadeInUp { from{opacity:0;transform:translateY(20px);} to{opacity:1;transform:translateY(0);} }

  .section { padding: 80px 0; }
  .section-label { font-size: 12px; font-weight: 600; letter-spacing: 3px; text-transform: uppercase; color: #7c3aed; margin-bottom: 12px; }
  .section-title { font-size: clamp(26px, 4vw, 38px); font-weight: 800; background: linear-gradient(135deg, #e0e7ff, #a78bfa); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; margin-bottom: 48px; letter-spacing: -1px; }

  .glass { background: rgba(255,255,255,0.03); backdrop-filter: blur(20px); border: 1px solid rgba(255,255,255,0.08); border-radius: 20px; }
  .glass:hover { border-color: rgba(124,58,237,0.3); box-shadow: 0 0 30px rgba(124,58,237,0.1); }

  .about-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 20px; }
  .about-card { padding: 28px 24px; border-radius: 18px; background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.07); transition: all 0.3s; position: relative; overflow: hidden; }
  .about-card::before { content: ''; position: absolute; inset: 0; border-radius: 18px; opacity: 0; transition: opacity 0.3s; }
  .about-card.c1::before { background: linear-gradient(135deg, rgba(124,58,237,0.08),transparent); }
  .about-card.c2::before { background: linear-gradient(135deg, rgba(37,99,235,0.08),transparent); }
  .about-card.c3::before { background: linear-gradient(135deg, rgba(147,51,234,0.08),transparent); }
  .about-card.c4::before { background: linear-gradient(135deg, rgba(99,102,241,0.08),transparent); }
  .about-card.c5::before { background: linear-gradient(135deg, rgba(168,85,247,0.08),transparent); }
  .about-card:hover { transform: translateY(-4px); border-color: rgba(124,58,237,0.3); box-shadow: 0 8px 40px rgba(124,58,237,0.12); }
  .about-card:hover::before { opacity: 1; }
  .about-icon { font-size: 32px; margin-bottom: 14px; display: block; }
  .about-card h3 { font-size: 15px; font-weight: 700; color: #e0e7ff; margin-bottom: 8px; }
  .about-card p { font-size: 13px; color: #64748b; line-height: 1.6; }

  .tech-category { margin-bottom: 40px; }
  .cat-title { font-size: 13px; font-weight: 600; letter-spacing: 2px; text-transform: uppercase; color: #7c3aed; margin-bottom: 18px; }
  .tech-grid { display: flex; flex-wrap: wrap; gap: 12px; }
  .tech-chip { display: flex; align-items: center; gap: 8px; padding: 10px 18px; border-radius: 50px; border: 1px solid; font-size: 13px; font-weight: 500; cursor: default; transition: all 0.3s; }
  .tc-purple { background: rgba(124,58,237,0.1); border-color: rgba(124,58,237,0.3); color: #c4b5fd; }
  .tc-purple:hover { background: rgba(124,58,237,0.2); box-shadow: 0 0 20px rgba(124,58,237,0.3); transform: translateY(-2px); }
  .tc-blue { background: rgba(37,99,235,0.1); border-color: rgba(37,99,235,0.3); color: #93c5fd; }
  .tc-blue:hover { background: rgba(37,99,235,0.2); box-shadow: 0 0 20px rgba(37,99,235,0.3); transform: translateY(-2px); }
  .tc-pink { background: rgba(236,72,153,0.1); border-color: rgba(236,72,153,0.3); color: #f9a8d4; }
  .tc-pink:hover { background: rgba(236,72,153,0.2); box-shadow: 0 0 20px rgba(236,72,153,0.3); transform: translateY(-2px); }
  .tech-dot { width: 8px; height: 8px; border-radius: 50%; }
  .dot-purple { background: #7c3aed; box-shadow: 0 0 6px #7c3aed; }
  .dot-blue { background: #2563eb; box-shadow: 0 0 6px #2563eb; }
  .dot-pink { background: #ec4899; box-shadow: 0 0 6px #ec4899; }

  .projects-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 24px; }
  .project-card { padding: 28px; border-radius: 20px; background: rgba(255,255,255,0.02); border: 1px solid rgba(255,255,255,0.07); transition: all 0.4s; cursor: pointer; position: relative; overflow: hidden; }
  .project-card::after { content: ''; position: absolute; inset: 0; border-radius: 20px; opacity: 0; transition: opacity 0.4s; }
  .pc1::after { background: linear-gradient(135deg, rgba(124,58,237,0.06), rgba(37,99,235,0.06)); }
  .pc2::after { background: linear-gradient(135deg, rgba(99,102,241,0.06), rgba(147,51,234,0.06)); }
  .pc3::after { background: linear-gradient(135deg, rgba(37,99,235,0.06), rgba(99,102,241,0.06)); }
  .pc4::after { background: linear-gradient(135deg, rgba(168,85,247,0.06), rgba(124,58,237,0.06)); }
  .project-card:hover { transform: translateY(-6px); border-color: rgba(124,58,237,0.4); box-shadow: 0 0 0 1px rgba(124,58,237,0.2), 0 20px 60px rgba(124,58,237,0.15); }
  .project-card:hover::after { opacity: 1; }
  .proj-icon { font-size: 36px; margin-bottom: 16px; }
  .proj-title { font-size: 17px; font-weight: 700; color: #e0e7ff; margin-bottom: 10px; }
  .proj-desc { font-size: 13px; color: #64748b; line-height: 1.6; margin-bottom: 18px; }
  .proj-tags { display: flex; flex-wrap: wrap; gap: 8px; }
  .proj-tag { padding: 4px 12px; border-radius: 50px; font-size: 11px; font-weight: 500; background: rgba(124,58,237,0.12); border: 1px solid rgba(124,58,237,0.25); color: #a78bfa; }

  .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 20px; }
  .stat-card { padding: 28px 24px; border-radius: 20px; background: rgba(255,255,255,0.02); border: 1px solid rgba(255,255,255,0.07); text-align: center; transition: all 0.3s; }
  .stat-card:hover { border-color: rgba(124,58,237,0.4); box-shadow: 0 0 40px rgba(124,58,237,0.12); transform: translateY(-3px); }
  .stat-num { font-size: 42px; font-weight: 900; background: linear-gradient(135deg, #a78bfa, #60a5fa); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
  .stat-label { font-size: 13px; color: #64748b; margin-top: 6px; font-weight: 500; letter-spacing: 0.5px; }
  .stat-icon { font-size: 28px; margin-bottom: 12px; }

  .timeline { position: relative; padding-left: 40px; }
  .timeline::before { content: ''; position: absolute; left: 12px; top: 0; bottom: 0; width: 2px; background: linear-gradient(to bottom, #7c3aed, #2563eb, transparent); }
  .tl-item { position: relative; margin-bottom: 32px; }
  .tl-dot { position: absolute; left: -34px; top: 4px; width: 14px; height: 14px; border-radius: 50%; background: linear-gradient(135deg, #7c3aed, #2563eb); box-shadow: 0 0 15px rgba(124,58,237,0.6); border: 2px solid #050510; }
  .tl-card { padding: 22px 24px; border-radius: 16px; background: rgba(255,255,255,0.02); border: 1px solid rgba(255,255,255,0.07); transition: all 0.3s; }
  .tl-card:hover { border-color: rgba(124,58,237,0.3); transform: translateX(4px); box-shadow: 0 0 30px rgba(124,58,237,0.08); }
  .tl-title { font-size: 15px; font-weight: 700; color: #e0e7ff; margin-bottom: 6px; }
  .tl-text { font-size: 13px; color: #64748b; line-height: 1.6; }
  .tl-year { font-size: 11px; font-weight: 600; color: #7c3aed; letter-spacing: 1px; margin-bottom: 6px; }

  .contact-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 16px; }
  .contact-btn { display: flex; align-items: center; justify-content: center; gap: 10px; padding: 18px 24px; border-radius: 16px; font-size: 14px; font-weight: 600; cursor: pointer; transition: all 0.3s; border: 1px solid; text-decoration: none; }
  .cb-github { background: rgba(255,255,255,0.03); border-color: rgba(255,255,255,0.1); color: #e0e7ff; }
  .cb-github:hover { background: rgba(255,255,255,0.08); border-color: rgba(255,255,255,0.25); transform: translateY(-3px); box-shadow: 0 10px 30px rgba(0,0,0,0.3); }
  .cb-linkedin { background: rgba(14,118,168,0.1); border-color: rgba(14,118,168,0.3); color: #7dd3fc; }
  .cb-linkedin:hover { background: rgba(14,118,168,0.2); box-shadow: 0 10px 30px rgba(14,118,168,0.2); transform: translateY(-3px); }
  .cb-instagram { background: rgba(225,48,108,0.1); border-color: rgba(225,48,108,0.3); color: #fda4af; }
  .cb-instagram:hover { background: rgba(225,48,108,0.2); box-shadow: 0 10px 30px rgba(225,48,108,0.2); transform: translateY(-3px); }
  .cb-email { background: rgba(124,58,237,0.1); border-color: rgba(124,58,237,0.3); color: #c4b5fd; }
  .cb-email:hover { background: rgba(124,58,237,0.2); box-shadow: 0 10px 30px rgba(124,58,237,0.2); transform: translateY(-3px); }

  .divider { height: 1px; background: linear-gradient(to right, transparent, rgba(124,58,237,0.3), rgba(37,99,235,0.3), transparent); margin: 0 0 80px; }

  .footer { text-align: center; padding: 60px 20px 40px; }
  .footer-text { font-size: clamp(18px, 3vw, 28px); font-weight: 800; background: linear-gradient(135deg, #a78bfa, #60a5fa, #c084fc); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; margin-bottom: 16px; letter-spacing: -0.5px; animation: glowPulse 3s ease-in-out infinite; }
  @keyframes glowPulse { 0%,100%{filter:brightness(1);} 50%{filter:brightness(1.2);} }
  .footer-sub { font-size: 13px; color: #334155; }

  .reveal { opacity: 0; transform: translateY(30px); transition: opacity 0.7s ease, transform 0.7s ease; }
  .reveal.visible { opacity: 1; transform: translateY(0); }

  .lang-bar-wrap { margin-top: 24px; }
  .lang-row { display: flex; align-items: center; gap: 12px; margin-bottom: 12px; }
  .lang-name { font-size: 12px; font-weight: 600; color: #94a3b8; width: 90px; flex-shrink: 0; }
  .lang-bar { flex: 1; height: 6px; border-radius: 3px; background: rgba(255,255,255,0.05); overflow: hidden; }
  .lang-fill { height: 100%; border-radius: 3px; transition: width 1.5s cubic-bezier(0.23,1,0.32,1); }
  .lang-pct { font-size: 12px; color: #64748b; width: 36px; text-align: right; }

  .streak-card { padding: 28px; border-radius: 20px; background: rgba(255,255,255,0.02); border: 1px solid rgba(255,255,255,0.07); display: flex; align-items: center; gap: 24px; flex-wrap: wrap; }
  .streak-num { font-size: 56px; font-weight: 900; background: linear-gradient(135deg, #f59e0b, #ef4444); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; line-height: 1; }
  .streak-label { font-size: 14px; color: #94a3b8; font-weight: 500; margin-top: 4px; }
  .streak-divider { width: 1px; height: 60px; background: rgba(255,255,255,0.08); }
  .contrib-grid { display: flex; flex-wrap: wrap; gap: 3px; flex: 1; min-width: 200px; }
  .contrib-cell { width: 12px; height: 12px; border-radius: 2px; }
  .cl0 { background: rgba(255,255,255,0.04); }
  .cl1 { background: rgba(124,58,237,0.3); }
  .cl2 { background: rgba(124,58,237,0.55); }
  .cl3 { background: rgba(124,58,237,0.8); }
  .cl4 { background: #7c3aed; box-shadow: 0 0 4px rgba(124,58,237,0.6); }

  @media(max-width: 600px) {
    .hero { padding: 40px 16px; }
    .about-grid { grid-template-columns: 1fr; }
    .projects-grid { grid-template-columns: 1fr; }
    .stats-grid { grid-template-columns: repeat(2, 1fr); }
    .contact-grid { grid-template-columns: repeat(2, 1fr); }
  }
</style>
</head>
<body>

<div class="bg-glow">
  <div class="blob blob1"></div>
  <div class="blob blob2"></div>
  <div class="blob blob3"></div>
</div>
<div class="grid-bg"></div>
<div class="particles" id="particles"></div>

<!-- HERO -->
<section class="hero">
  <div class="hero-inner">
    <div class="avatar-wrap">
      <div class="avatar">
        <div class="avatar-ring"></div>
        <span>S</span>
        <div class="status-dot"></div>
      </div>
    </div>
    <h1>Hi 👋, I'm Suriya</h1>
    <p class="hero-sub">Creative UI/UX Designer &nbsp;•&nbsp; Frontend Developer &nbsp;•&nbsp; AI Enthusiast</p>
    <div class="typing-wrap">
      <span id="typed-text"></span><span class="typing-cursor"></span>
    </div>
    <div class="hero-badges">
      <span class="badge badge-purple">🎨 UI/UX Designer</span>
      <span class="badge badge-blue">⚡ Frontend Dev</span>
      <span class="badge badge-pink">🤖 AI Explorer</span>
    </div>
    <div class="cta-row">
      <button class="btn btn-primary">View My Work ↓</button>
      <button class="btn btn-outline">Connect with Me</button>
    </div>
  </div>
</section>

<div class="content">

  <!-- ABOUT -->
  <section class="section reveal">
    <div class="section-label">// about.me</div>
    <div class="section-title">What I Do</div>
    <div class="about-grid">
      <div class="about-card c1">
        <span class="about-icon">🎨</span>
        <h3>UI/UX Design</h3>
        <p>Crafting intuitive and visually stunning interfaces with a focus on clean UI and smooth UX experiences.</p>
      </div>
      <div class="about-card c2">
        <span class="about-icon">⚡</span>
        <h3>Frontend Dev</h3>
        <p>Building responsive, performant web applications using modern frameworks and cutting-edge technologies.</p>
      </div>
      <div class="about-card c3">
        <span class="about-icon">🤖</span>
        <h3>AI / ML</h3>
        <p>Exploring intelligent systems, machine learning models, and AI-powered digital experiences.</p>
      </div>
      <div class="about-card c4">
        <span class="about-icon">🚀</span>
        <h3>Digital Products</h3>
        <p>Building creative, end-to-end digital products that solve real-world problems with elegant solutions.</p>
      </div>
      <div class="about-card c5">
        <span class="about-icon">💡</span>
        <h3>Innovation</h3>
        <p>Always learning, experimenting, and pushing the boundaries of what's possible with technology.</p>
      </div>
    </div>
  </section>

  <div class="divider"></div>

  <!-- TECH STACK -->
  <section class="section reveal">
    <div class="section-label">// tech.stack</div>
    <div class="section-title">Technologies</div>

    <div class="tech-category">
      <div class="cat-title">⚡ Frontend</div>
      <div class="tech-grid">
        <div class="tech-chip tc-purple"><span class="tech-dot dot-purple"></span>HTML5</div>
        <div class="tech-chip tc-purple"><span class="tech-dot dot-purple"></span>CSS3</div>
        <div class="tech-chip tc-purple"><span class="tech-dot dot-purple"></span>JavaScript</div>
        <div class="tech-chip tc-purple"><span class="tech-dot dot-purple"></span>React</div>
        <div class="tech-chip tc-purple"><span class="tech-dot dot-purple"></span>Tailwind CSS</div>
      </div>
    </div>

    <div class="tech-category">
      <div class="cat-title">🎨 Design</div>
      <div class="tech-grid">
        <div class="tech-chip tc-pink"><span class="tech-dot dot-pink"></span>Figma</div>
        <div class="tech-chip tc-pink"><span class="tech-dot dot-pink"></span>Canva</div>
        <div class="tech-chip tc-pink"><span class="tech-dot dot-pink"></span>Photoshop</div>
      </div>
    </div>

    <div class="tech-category">
      <div class="cat-title">🤖 AI & Programming</div>
      <div class="tech-grid">
        <div class="tech-chip tc-blue"><span class="tech-dot dot-blue"></span>Python</div>
        <div class="tech-chip tc-blue"><span class="tech-dot dot-blue"></span>OpenCV</div>
        <div class="tech-chip tc-blue"><span class="tech-dot dot-blue"></span>Machine Learning</div>
        <div class="tech-chip tc-blue"><span class="tech-dot dot-blue"></span>SQL</div>
        <div class="tech-chip tc-blue"><span class="tech-dot dot-blue"></span>C</div>
      </div>
    </div>
  </section>

  <div class="divider"></div>

  <!-- PROJECTS -->
  <section class="section reveal">
    <div class="section-label">// featured.projects</div>
    <div class="section-title">What I've Built</div>
    <div class="projects-grid">

      <div class="project-card pc1">
        <div class="proj-icon">🔍</div>
        <div class="proj-title">Image Forgery Detection</div>
        <p class="proj-desc">AI-powered system that detects tampered or forged images using deep learning and computer vision techniques.</p>
        <div class="proj-tags">
          <span class="proj-tag">Python</span>
          <span class="proj-tag">OpenCV</span>
          <span class="proj-tag">ML</span>
          <span class="proj-tag">CNN</span>
        </div>
      </div>

      <div class="project-card pc2">
        <div class="proj-icon">🧠</div>
        <div class="proj-title">Graph Intelligence Agent</div>
        <p class="proj-desc">Intelligent agent leveraging graph algorithms and AI reasoning for complex data relationship analysis.</p>
        <div class="proj-tags">
          <span class="proj-tag">Python</span>
          <span class="proj-tag">AI</span>
          <span class="proj-tag">Graph</span>
          <span class="proj-tag">NLP</span>
        </div>
      </div>

      <div class="project-card pc3">
        <div class="proj-icon">🎓</div>
        <div class="proj-title">Course Finder Website</div>
        <p class="proj-desc">Modern web app helping students discover and filter courses with a clean, intuitive interface and smart search.</p>
        <div class="proj-tags">
          <span class="proj-tag">React</span>
          <span class="proj-tag">JavaScript</span>
          <span class="proj-tag">CSS</span>
          <span class="proj-tag">API</span>
        </div>
      </div>

      <div class="project-card pc4">
        <div class="proj-icon">💧</div>
        <div class="proj-title">Water Contamination ML</div>
        <p class="proj-desc">Machine learning model to predict and classify water contamination levels from environmental sensor data.</p>
        <div class="proj-tags">
          <span class="proj-tag">Python</span>
          <span class="proj-tag">ML</span>
          <span class="proj-tag">Data</span>
          <span class="proj-tag">SQL</span>
        </div>
      </div>

    </div>
  </section>

  <div class="divider"></div>

  <!-- STATS -->
  <section class="section reveal">
    <div class="section-label">// github.stats</div>
    <div class="section-title">By The Numbers</div>
    <div class="stats-grid">
      <div class="stat-card">
        <div class="stat-icon">📦</div>
        <div class="stat-num" data-target="24">0</div>
        <div class="stat-label">Repositories</div>
      </div>
      <div class="stat-card">
        <div class="stat-icon">⭐</div>
        <div class="stat-num" data-target="87">0</div>
        <div class="stat-label">Stars Earned</div>
      </div>
      <div class="stat-card">
        <div class="stat-icon">🔥</div>
        <div class="stat-num" data-target="42">0</div>
        <div class="stat-label">Day Streak</div>
      </div>
      <div class="stat-card">
        <div class="stat-icon">💻</div>
        <div class="stat-num" data-target="312">0</div>
        <div class="stat-label">Contributions</div>
      </div>
    </div>

    <div style="margin-top:32px;">
      <div class="streak-card">
        <div>
          <div class="streak-num">🔥 42</div>
          <div class="streak-label">Day Streak</div>
        </div>
        <div class="streak-divider"></div>
        <div class="contrib-grid" id="contrib-grid"></div>
      </div>
    </div>

    <div style="margin-top:24px; padding:28px; border-radius:20px; background:rgba(255,255,255,0.02); border:1px solid rgba(255,255,255,0.07);">
      <div style="font-size:13px;font-weight:600;color:#7c3aed;letter-spacing:2px;margin-bottom:20px;">TOP LANGUAGES</div>
      <div class="lang-bar-wrap" id="lang-bars"></div>
    </div>
  </section>

  <div class="divider"></div>

  <!-- ACHIEVEMENTS -->
  <section class="section reveal">
    <div class="section-label">// achievements</div>
    <div class="section-title">Journey So Far</div>
    <div class="timeline">
      <div class="tl-item">
        <div class="tl-dot"></div>
        <div class="tl-card">
          <div class="tl-year">ONGOING</div>
          <div class="tl-title">🎨 Mastering Modern UI Experiences</div>
          <p class="tl-text">Building premium, accessible interfaces with Figma and React — focused on pixel-perfect design and delightful micro-interactions.</p>
        </div>
      </div>
      <div class="tl-item">
        <div class="tl-dot"></div>
        <div class="tl-card">
          <div class="tl-year">2024</div>
          <div class="tl-title">🤖 Diving Deep into AI/ML Technologies</div>
          <p class="tl-text">Exploring machine learning, computer vision, and intelligent systems to build next-generation AI-powered applications.</p>
        </div>
      </div>
      <div class="tl-item">
        <div class="tl-dot"></div>
        <div class="tl-card">
          <div class="tl-year">2023</div>
          <div class="tl-title">⚡ Frontend Development Foundations</div>
          <p class="tl-text">Mastered React, JavaScript ES6+, and Tailwind CSS — building responsive, performant applications from scratch.</p>
        </div>
      </div>
      <div class="tl-item">
        <div class="tl-dot"></div>
        <div class="tl-card">
          <div class="tl-year">2022</div>
          <div class="tl-title">💡 Problem Solving & CS Fundamentals</div>
          <p class="tl-text">Built a strong foundation in algorithms, data structures, and programming with C, Python, and SQL.</p>
        </div>
      </div>
    </div>
  </section>

  <div class="divider"></div>

  <!-- CONTACT -->
  <section class="section reveal">
    <div class="section-label">// let's.connect</div>
    <div class="section-title">Get In Touch</div>
    <p style="font-size:15px;color:#64748b;margin-bottom:36px;max-width:500px;">Always open to exciting opportunities, collaborations, and conversations about design and technology.</p>
    <div class="contact-grid">
      <a class="contact-btn cb-github" href="#">
        <span style="font-size:20px;">🐱</span> GitHub
      </a>
      <a class="contact-btn cb-linkedin" href="#">
        <span style="font-size:20px;">💼</span> LinkedIn
      </a>
      <a class="contact-btn cb-instagram" href="#">
        <span style="font-size:20px;">📸</span> Instagram
      </a>
      <a class="contact-btn cb-email" href="#">
        <span style="font-size:20px;">✉️</span> Email Me
      </a>
    </div>
  </section>

</div>

<!-- FOOTER -->
<footer class="footer reveal">
  <div style="width:200px;height:1px;background:linear-gradient(to right,transparent,rgba(124,58,237,0.5),transparent);margin:0 auto 32px;"></div>
  <div class="footer-text">✦ Designing Intelligent Digital Experiences ✦</div>
  <p class="footer-sub">Built with passion by Suriya &nbsp;•&nbsp; 2025</p>
  <div style="margin-top:20px;display:flex;gap:8px;justify-content:center;">
    <span style="width:8px;height:8px;border-radius:50%;background:#7c3aed;box-shadow:0 0 8px #7c3aed;display:inline-block;"></span>
    <span style="width:8px;height:8px;border-radius:50%;background:#2563eb;box-shadow:0 0 8px #2563eb;display:inline-block;"></span>
    <span style="width:8px;height:8px;border-radius:50%;background:#9333ea;box-shadow:0 0 8px #9333ea;display:inline-block;"></span>
  </div>
</footer>

<script>
  const pc = document.getElementById('particles');
  for(let i=0;i<30;i++){
    const p = document.createElement('div');
    p.className='particle';
    p.style.cssText=`left:${Math.random()*100}%;--drift:${(Math.random()-0.5)*100}px;animation-duration:${8+Math.random()*12}s;animation-delay:${Math.random()*10}s;`;
    pc.appendChild(p);
  }

  const words=['UI/UX Designer','Frontend Developer','AI Innovator','Building Modern Digital Experiences'];
  let wi=0,ci=0,del=false;
  const el=document.getElementById('typed-text');
  function type(){
    const w=words[wi];
    if(!del){
      el.textContent=w.slice(0,++ci);
      if(ci===w.length){del=true;setTimeout(type,1800);return;}
    } else {
      el.textContent=w.slice(0,--ci);
      if(ci===0){del=false;wi=(wi+1)%words.length;setTimeout(type,400);return;}
    }
    setTimeout(type,del?50:80);
  }
  setTimeout(type,800);

  const cg=document.getElementById('contrib-grid');
  const lvls=['cl0','cl0','cl0','cl1','cl1','cl2','cl3','cl4'];
  for(let i=0;i<140;i++){
    const c=document.createElement('div');
    c.className='contrib-cell '+lvls[Math.floor(Math.random()*lvls.length)];
    cg.appendChild(c);
  }

  const langs=[
    {name:'JavaScript',pct:40,color:'linear-gradient(90deg,#f59e0b,#ef4444)'},
    {name:'Python',pct:25,color:'linear-gradient(90deg,#3b82f6,#8b5cf6)'},
    {name:'React',pct:20,color:'linear-gradient(90deg,#06b6d4,#3b82f6)'},
    {name:'CSS',pct:10,color:'linear-gradient(90deg,#8b5cf6,#ec4899)'},
    {name:'C',pct:5,color:'linear-gradient(90deg,#64748b,#94a3b8)'},
  ];
  const lb=document.getElementById('lang-bars');
  langs.forEach(l=>{
    lb.innerHTML+=`<div class="lang-row">
      <span class="lang-name">${l.name}</span>
      <div class="lang-bar"><div class="lang-fill" data-w="${l.pct}" style="width:0;background:${l.color}"></div></div>
      <span class="lang-pct">${l.pct}%</span>
    </div>`;
  });

  const observer=new IntersectionObserver((entries)=>{
    entries.forEach(e=>{
      if(e.isIntersecting){
        e.target.classList.add('visible');
        e.target.querySelectorAll('[data-target]').forEach(el=>{
          const target=+el.dataset.target;
          let cur=0,step=Math.ceil(target/40);
          const t=setInterval(()=>{cur=Math.min(cur+step,target);el.textContent=cur;if(cur>=target)clearInterval(t);},30);
        });
        e.target.querySelectorAll('.lang-fill').forEach(el=>{
          el.style.width=el.dataset.w+'%';
        });
        observer.unobserve(e.target);
      }
    });
  },{threshold:0.1});
  document.querySelectorAll('.reveal').forEach(el=>observer.observe(el));
</script>
</body>
</html>
