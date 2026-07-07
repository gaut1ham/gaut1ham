<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Gautham K.B. — Case File</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:ital,wght@0,400;0,500;0,600;0,700;1,400&family=Inter:wght@400;500;600;800&display=swap" rel="stylesheet">
<style>
  :root{
    --bg: #0c0d0a;
    --panel: #14160f;
    --panel-2: #191b13;
    --line: #2b2d22;
    --paper: #e7e2d3;
    --paper-dim: #9a9686;
    --amber: #d99a3d;
    --amber-bright: #f0b354;
    --red: #b8452f;
    --olive: #5c6248;
    --shadow: rgba(0,0,0,0.5);
  }

  *{ margin:0; padding:0; box-sizing:border-box; }

  html{ scroll-behavior: smooth; }

  body{
    background: var(--bg);
    color: var(--paper);
    font-family: 'Inter', sans-serif;
    overflow-x: hidden;
    position: relative;
  }

  /* ambient scanline / grain overlay */
  body::before{
    content:"";
    position: fixed; inset:0;
    background-image: repeating-linear-gradient(
      0deg, rgba(255,255,255,0.015) 0px, rgba(255,255,255,0.015) 1px,
      transparent 1px, transparent 3px
    );
    pointer-events:none;
    z-index: 999;
    opacity: 0.5;
  }

  body::after{
    content:"";
    position: fixed; inset:0;
    background: radial-gradient(ellipse at 50% 0%, transparent 0%, rgba(0,0,0,0.55) 100%);
    pointer-events:none;
    z-index: 998;
  }

  .mono{ font-family: 'IBM Plex Mono', monospace; }

  ::selection{ background: var(--amber); color: #0c0d0a; }

  a{ color: inherit; text-decoration:none; }

  /* ---------- layout wrapper ---------- */
  .wrap{
    max-width: 920px;
    margin: 0 auto;
    padding: 0 28px;
  }

  /* ---------- top classification bar ---------- */
  .topbar{
    border-bottom: 1px solid var(--line);
    padding: 14px 0;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.12em;
    color: var(--paper-dim);
  }
  .topbar .wrap{
    display:flex; justify-content:space-between; align-items:center;
    flex-wrap: wrap; gap: 8px;
  }
  .topbar .blink{
    color: var(--amber);
    animation: blink 1.6s steps(1) infinite;
  }
  @keyframes blink{ 50%{ opacity: 0.25; } }

  /* ---------- hero ---------- */
  .hero{
    padding: 110px 0 90px;
    position: relative;
  }

  .eyebrow{
    font-family:'IBM Plex Mono', monospace;
    font-size: 12px;
    letter-spacing: 0.18em;
    color: var(--olive);
    text-transform: uppercase;
    margin-bottom: 22px;
    display:flex;
    align-items:center;
    gap: 10px;
  }
  .eyebrow::before{
    content:"";
    width:18px; height:1px; background: var(--olive);
    display:inline-block;
  }

  h1.title{
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: clamp(38px, 7vw, 74px);
    line-height: 1.02;
    letter-spacing: -0.01em;
    color: var(--paper);
    text-transform: uppercase;
  }
  h1.title .sub{
    display:block;
    font-size: 0.34em;
    font-weight: 500;
    color: var(--paper-dim);
    text-transform: none;
    letter-spacing: 0.01em;
    margin-top: 14px;
    font-family: 'Inter', sans-serif;
  }

  /* the stamp */
  .stamp{
    position: absolute;
    top: 72px;
    right: 24px;
    width: 148px;
    height: 148px;
    border: 3px solid var(--amber);
    border-radius: 50%;
    color: var(--amber);
    font-family: 'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: 15px;
    text-transform: uppercase;
    display:flex;
    align-items:center;
    justify-content:center;
    text-align:center;
    letter-spacing: 0.06em;
    transform: rotate(-14deg) scale(2.4);
    opacity: 0;
    mix-blend-mode: screen;
    animation: stamp-in 0.5s cubic-bezier(.2,1.4,.4,1) 0.9s forwards;
    pointer-events:none;
  }
  .stamp::before{
    content:"";
    position:absolute; inset: 8px;
    border: 1px solid var(--amber);
    border-radius: 50%;
  }
  @keyframes stamp-in{
    0%{ opacity:0; transform: rotate(-14deg) scale(2.6); }
    60%{ opacity: 0.9; transform: rotate(-14deg) scale(0.94); }
    80%{ opacity: 0.65; }
    100%{ opacity: 0.85; transform: rotate(-14deg) scale(1); }
  }

  @media (max-width: 640px){
    .stamp{ display:none; }
  }

  /* terminal block */
  .terminal{
    margin-top: 54px;
    background: var(--panel);
    border: 1px solid var(--line);
    border-radius: 4px;
    max-width: 560px;
    box-shadow: 0 20px 60px var(--shadow);
  }
  .terminal .bar{
    display:flex; gap:6px;
    padding: 10px 14px;
    border-bottom: 1px solid var(--line);
  }
  .terminal .bar span{
    width:9px; height:9px; border-radius:50%;
    background: var(--line);
  }
  .terminal .body{
    padding: 18px 20px 22px;
    font-family:'IBM Plex Mono', monospace;
    font-size: 13.5px;
    line-height: 1.9;
    color: #cfcabb;
    min-height: 128px;
  }
  .terminal .prompt{ color: var(--amber); }
  .terminal .cursor{
    display:inline-block;
    width: 8px; height: 15px;
    background: var(--amber);
    vertical-align: -2px;
    animation: blink 1s steps(1) infinite;
  }

  /* ---------- section shell ---------- */
  section{
    padding: 90px 0;
    border-top: 1px solid var(--line);
  }

  .reveal{
    opacity: 0;
    transform: translateY(28px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .reveal.in{
    opacity: 1;
    transform: translateY(0);
  }

  .tag{
    font-family:'IBM Plex Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.16em;
    text-transform: uppercase;
    color: var(--amber);
    display:flex;
    align-items:center;
    gap: 10px;
    margin-bottom: 18px;
  }
  .tag .n{
    color: var(--olive);
  }

  h2.h{
    font-family:'IBM Plex Mono', monospace;
    font-weight: 600;
    font-size: clamp(24px, 4vw, 34px);
    text-transform: uppercase;
    letter-spacing: -0.01em;
    margin-bottom: 34px;
  }

  p.lead{
    font-size: 16px;
    line-height: 1.75;
    color: #cfcabb;
    max-width: 62ch;
  }

  /* ---------- case file / EVM timeline ---------- */
  .case{
    background: var(--panel);
    border: 1px solid var(--line);
    border-radius: 4px;
    padding: 34px 32px 36px;
    position: relative;
    overflow: hidden;
  }
  .case::before{
    content: "CASE FILE // EVM-6.0";
    position: absolute;
    top: 16px; right: -46px;
    background: var(--red);
    color: #f4ede0;
    font-family:'IBM Plex Mono', monospace;
    font-size: 10.5px;
    letter-spacing: 0.1em;
    padding: 4px 50px;
    transform: rotate(38deg);
    box-shadow: 0 2px 6px var(--shadow);
  }

  .case h3{
    font-family:'IBM Plex Mono', monospace;
    font-size: 20px;
    margin-bottom: 8px;
    text-transform: uppercase;
  }
  .case .status{
    font-family:'IBM Plex Mono', monospace;
    font-size: 12px;
    color: var(--amber-bright);
    margin-bottom: 26px;
    letter-spacing: 0.04em;
  }

  .timeline{
    display:flex;
    flex-direction:column;
    gap: 0;
    margin-top: 10px;
  }
  .tl-item{
    display:grid;
    grid-template-columns: 92px 22px 1fr;
    gap: 0;
  }
  .tl-item .t{
    font-family:'IBM Plex Mono', monospace;
    font-size: 12px;
    color: var(--olive);
    padding-top: 2px;
  }
  .tl-item .mid{
    display:flex; flex-direction:column; align-items:center;
  }
  .tl-item .dot{
    width: 9px; height:9px; border-radius:50%;
    background: var(--amber);
    margin-top: 4px;
    flex-shrink:0;
  }
  .tl-item .stem{
    flex:1;
    width: 1px;
    background: var(--line);
    margin-top: 4px;
  }
  .tl-item:last-child .stem{ display:none; }
  .tl-item .content{
    padding-bottom: 30px;
  }
  .tl-item .content h4{
    font-size: 15.5px;
    font-weight: 600;
    margin-bottom: 6px;
  }
  .tl-item .content p{
    font-size: 14px;
    color: var(--paper-dim);
    line-height: 1.65;
    max-width: 52ch;
  }

  /* ---------- clearance badges (skills) ---------- */
  .grid{
    display:grid;
    grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
    gap: 14px;
    margin-top: 8px;
  }
  .badge{
    border: 1px solid var(--line);
    background: var(--panel);
    border-radius: 4px;
    padding: 18px 16px;
    transition: transform 0.25s ease, border-color 0.25s ease, background 0.25s ease;
  }
  .badge:hover{
    transform: translateY(-4px);
    border-color: var(--amber);
    background: var(--panel-2);
  }
  .badge .name{
    font-family:'IBM Plex Mono', monospace;
    font-weight: 600;
    font-size: 14px;
    margin-bottom: 8px;
  }
  .badge .lvl{
    font-family:'IBM Plex Mono', monospace;
    font-size: 10.5px;
    color: var(--olive);
    letter-spacing: 0.08em;
    text-transform: uppercase;
  }
  .badge .bar{
    margin-top: 10px;
    height: 3px;
    background: var(--line);
    border-radius: 2px;
    overflow: hidden;
  }
  .badge .bar span{
    display:block;
    height:100%;
    background: var(--amber);
    width: 0%;
    transition: width 1.1s cubic-bezier(.2,.8,.2,1);
  }
  .badge.in .bar span{ width: var(--w); }

  /* ---------- open lines / learning ---------- */
  .two-col{
    display:grid;
    grid-template-columns: 1fr 1fr;
    gap: 40px;
  }
  @media (max-width: 700px){ .two-col{ grid-template-columns: 1fr; } }

  .list-block .k{
    font-family:'IBM Plex Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--amber);
    margin-bottom: 14px;
  }
  .list-block ul{ list-style:none; }
  .list-block li{
    font-size: 14.5px;
    color: #cfcabb;
    padding: 10px 0;
    border-bottom: 1px dashed var(--line);
  }
  .list-block li:last-child{ border-bottom:none; }

  /* ---------- footer / contact ---------- */
  footer{
    padding: 70px 0 50px;
    border-top: 1px solid var(--line);
  }
  .contact-title{
    font-family:'IBM Plex Mono', monospace;
    font-weight: 700;
    font-size: clamp(28px, 5vw, 46px);
    text-transform: uppercase;
    margin-bottom: 30px;
    line-height: 1.1;
  }
  .contact-title span{ color: var(--amber); }

  .links{
    display:flex;
    flex-wrap: wrap;
    gap: 12px;
    margin-bottom: 50px;
  }
  .links a{
    font-family:'IBM Plex Mono', monospace;
    font-size: 13px;
    border: 1px solid var(--line);
    padding: 12px 18px;
    border-radius: 3px;
    letter-spacing: 0.02em;
    transition: all 0.2s ease;
    display:inline-flex;
    align-items:center;
    gap: 8px;
  }
  .links a:hover{
    border-color: var(--amber);
    background: var(--panel);
    color: var(--amber-bright);
  }

  .fine-print{
    font-family:'IBM Plex Mono', monospace;
    font-size: 11px;
    color: #565349;
    display:flex;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 10px;
    padding-top: 24px;
    border-top: 1px solid var(--line);
  }

  @media (prefers-reduced-motion: reduce){
    *{ animation: none !important; transition: none !important; }
    .reveal{ opacity:1; transform:none; }
  }
</style>
</head>
<body>

  <div class="topbar">
    <div class="wrap">
      <span>FILE REF: GKB-2026-CS-001</span>
      <span><span class="blink">●</span> STATUS: ACTIVELY DEPLOYED</span>
    </div>
  </div>

  <header class="hero">
    <div class="wrap" style="position:relative;">
      <div class="stamp">CLEARANCE<br>GRANTED</div>
      <p class="eyebrow mono">Subject profile — Trivandrum, Kerala</p>
      <h1 class="title">
        Gautham K.B.
        <span class="sub">Cybersecurity-focused developer. Class 12 graduate, PCM + Computer Science. Known on campus for building the tools other people just complain about.</span>
      </h1>

      <div class="terminal">
        <div class="bar"><span></span><span></span><span></span></div>
        <div class="body" id="termBody"></div>
      </div>
    </div>
  </header>

  <section id="case">
    <div class="wrap reveal">
      <div class="tag"><span class="n">01</span> Field report</div>
      <h2 class="h">The nine-hour build</h2>
      <p class="lead" style="margin-bottom: 34px;">
        The clearest evidence of how I work: given a real deadline and a broken system, here's what happened.
      </p>

      <div class="case">
        <h3>EVM 6.0 — School Election Voting System</h3>
        <div class="status">RESULT: DEPLOYED FOR LIVE HEAD BOY / HEAD GIRL &amp; HOUSE LEADER ELECTIONS</div>

        <div class="timeline">
          <div class="tl-item">
            <div class="t mono">HOUR 0</div>
            <div class="mid"><div class="dot"></div><div class="stem"></div></div>
            <div class="content">
              <h4>The existing system wasn't going to hold up</h4>
              <p>The school's election interface had gaps that made it unfit for a real vote. Instead of flagging it and waiting, I decided to rebuild it myself.</p>
            </div>
          </div>
          <div class="tl-item">
            <div class="t mono">HOUR 9</div>
            <div class="mid"><div class="dot"></div><div class="stem"></div></div>
            <div class="content">
              <h4>EVM 6.0 shipped, solo</h4>
              <p>Built end-to-end in a single sitting — no team, no second pass. It needed to just work, so it did.</p>
            </div>
          </div>
          <div class="tl-item">
            <div class="t mono">DAY 1</div>
            <div class="mid"><div class="dot"></div><div class="stem"></div></div>
            <div class="content">
              <h4>Ran the real elections</h4>
              <p>Deployed live for Head Boy, Head Girl, and house leader elections — actual votes, actual results, no dry run.</p>
            </div>
          </div>
          <div class="tl-item">
            <div class="t mono">ONGOING</div>
            <div class="mid"><div class="dot"></div></div>
            <div class="content">
              <h4>The name stuck</h4>
              <p>Publicly recognized by the principal, Fr. Chacko Puthukulam. The nickname "Software Engineer GKB" followed shortly after — it hasn't gone away since.</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <section id="skills">
    <div class="wrap reveal">
      <div class="tag"><span class="n">02</span> Capabilities on file</div>
      <h2 class="h">Working stack</h2>
      <div class="grid" id="badgeGrid">
        <div class="badge" style="--w:92%"><div class="name mono">Python</div><div class="lvl">Daily driver</div><div class="bar"><span></span></div></div>
        <div class="badge" style="--w:80%"><div class="name mono">Linux</div><div class="lvl">Comfortable</div><div class="bar"><span></span></div></div>
        <div class="badge" style="--w:74%"><div class="name mono">Networking</div><div class="lvl">Building fluency</div><div class="bar"><span></span></div></div>
        <div class="badge" style="--w:70%"><div class="name mono">JavaScript</div><div class="lvl">Working knowledge</div><div class="bar"><span></span></div></div>
        <div class="badge" style="--w:65%"><div class="name mono">Flask</div><div class="lvl">Working knowledge</div><div class="bar"><span></span></div></div>
        <div class="badge" style="--w:60%"><div class="name mono">MySQL</div><div class="lvl">Working knowledge</div><div class="bar"><span></span></div></div>
        <div class="badge" style="--w:78%"><div class="name mono">Secure coding</div><div class="lvl">Actively studying</div><div class="bar"><span></span></div></div>
        <div class="badge" style="--w:55%"><div class="name mono">Git</div><div class="lvl">Working knowledge</div><div class="bar"><span></span></div></div>
      </div>
    </div>
  </section>

  <section id="learning">
    <div class="wrap reveal">
      <div class="tag"><span class="n">03</span> Current activity</div>
      <h2 class="h">What's in progress</h2>
      <div class="two-col">
        <div class="list-block">
          <div class="k">Currently learning</div>
          <ul>
            <li>Cybersecurity fundamentals &amp; defensive practices</li>
            <li>Python for security automation</li>
            <li>Linux internals &amp; core networking</li>
          </ul>
        </div>
        <div class="list-block">
          <div class="k">Open to</div>
          <ul>
            <li>Beginner-friendly security &amp; automation projects</li>
            <li>Collaborating with people learning system security</li>
            <li>Feedback from anyone further along than me</li>
          </ul>
        </div>
      </div>
    </div>
  </section>

  <footer>
    <div class="wrap reveal">
      <div class="contact-title">Case open.<br>Reach out <span>anytime.</span></div>
      <div class="links">
        <a href="https://gaut1ham.github.io/GK-Portfolio/" target="_blank">→ Portfolio</a>
        <a href="https://github.com/gaut1ham" target="_blank">→ GitHub</a>
        <a href="mailto:gkb8097@gmail.com">→ Email</a>
        <a href="https://instagram.com/gaut1ham" target="_blank">→ Instagram</a>
      </div>
      <div class="fine-print">
        <span>© 2026 Gautham K.B. — Trivandrum, Kerala</span>
        <span>Document ends here.</span>
      </div>
    </div>
  </footer>

<script>
  // typing terminal effect
  const lines = [
    { prompt: '$ whoami', out: 'gautham — class 12 graduate, PCM + Computer Science' },
    { prompt: '$ cat status.txt', out: 'building things, then trying to break them to see how they hold up' },
    { prompt: '$ ./run_evm.sh', out: 'EVM 6.0 — deployed. election complete. no incidents reported.' }
  ];
  const termBody = document.getElementById('termBody');
  let li = 0;

  function typeLine(){
    if(li >= lines.length){
      const cur = document.createElement('span');
      cur.className = 'cursor';
      termBody.appendChild(cur);
      return;
    }
    const row = document.createElement('div');
    const promptSpan = document.createElement('span');
    promptSpan.className = 'prompt';
    row.appendChild(promptSpan);
    termBody.appendChild(row);

    const full = lines[li].prompt;
    let i = 0;
    const typer = setInterval(() => {
      promptSpan.textContent = full.slice(0, i+1);
      i++;
      if(i >= full.length){
        clearInterval(typer);
        const outRow = document.createElement('div');
        outRow.style.color = '#9a9686';
        outRow.style.marginBottom = '10px';
        outRow.textContent = lines[li].out;
        termBody.appendChild(outRow);
        li++;
        setTimeout(typeLine, 320);
      }
    }, 26);
  }
  setTimeout(typeLine, 500);

  // scroll reveal
  const revealEls = document.querySelectorAll('.reveal');
  const io = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if(e.isIntersecting){
        e.target.classList.add('in');
        io.unobserve(e.target);
      }
    });
  }, { threshold: 0.12 });
  revealEls.forEach(el => io.observe(el));

  // badge bars fill on view
  const badges = document.querySelectorAll('.badge');
  const io2 = new IntersectionObserver((entries) => {
    entries.forEach((e, idx) => {
      if(e.isIntersecting){
        setTimeout(() => e.target.classList.add('in'), idx * 70);
        io2.unobserve(e.target);
      }
    });
  }, { threshold: 0.2 });
  badges.forEach(b => io2.observe(b));
</script>

</body>
</html>
