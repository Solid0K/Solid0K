<style>
  @import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=VT323&display=swap');

  .pip {
    background: #0a0a0a;
    color: #00ff41;
    font-family: 'Share Tech Mono', 'Courier New', monospace;
    min-height: 100vh;
    padding: 0;
    margin: 0;
    position: relative;
    overflow: hidden;
  }

  .pip * { box-sizing: border-box; }

  .scanlines {
    position: fixed;
    top: 0; left: 0; right: 0; bottom: 0;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 2px,
      rgba(0,0,0,0.15) 2px,
      rgba(0,0,0,0.15) 4px
    );
    pointer-events: none;
    z-index: 9999;
  }

  .crt-flicker {
    animation: flicker 8s infinite;
  }

  @keyframes flicker {
    0%,100%{opacity:1} 92%{opacity:1} 93%{opacity:0.97} 94%{opacity:1} 96%{opacity:0.95} 97%{opacity:1}
  }

  .glow { text-shadow: 0 0 8px #00ff41, 0 0 2px #00ff41; }
  .glow-dim { text-shadow: 0 0 4px #00cc33; }

  .border-pip { border: 1px solid #00ff41; box-shadow: 0 0 8px rgba(0,255,65,0.3), inset 0 0 8px rgba(0,255,65,0.05); }

  .section { border: 1px solid #00ff41; margin: 12px 0; padding: 12px 16px; box-shadow: 0 0 10px rgba(0,255,65,0.2); }

  .section-title {
    font-family: 'VT323', monospace;
    font-size: 22px;
    color: #00ff41;
    text-shadow: 0 0 10px #00ff41;
    border-bottom: 1px solid #00ff41;
    padding-bottom: 6px;
    margin-bottom: 12px;
    letter-spacing: 2px;
  }

  .progress-bar { display: flex; align-items: center; gap: 8px; margin: 4px 0; font-size: 12px; }
  .bar-track { flex: 1; height: 10px; background: #001a00; border: 1px solid #00aa2a; }
  .bar-fill { height: 100%; background: #00ff41; box-shadow: 0 0 4px #00ff41; transition: width 1s ease; }

  .cursor { display: inline-block; width: 9px; height: 14px; background: #00ff41; animation: blink 1s step-end infinite; vertical-align: -2px; }
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

  .typing { overflow: hidden; white-space: nowrap; border-right: 2px solid #00ff41; animation: type 2.5s steps(40) forwards, blink-border 0.75s step-end infinite; }
  @keyframes type { from{width:0} to{width:100%} }
  @keyframes blink-border { 50%{border-color:transparent} }

  .boot-done { display: none; }

  .status-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 6px; }
  .status-item { font-size: 12px; padding: 4px 0; border-bottom: 1px solid #003300; }
  .status-label { color: #00aa2a; }
  .status-val { color: #00ff41; }

  .special-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 8px; }
  .special-item { padding: 6px 8px; border: 1px solid #003300; }
  .special-letter { font-family: 'VT323', monospace; font-size: 28px; color: #00ff41; text-shadow: 0 0 8px #00ff41; }
  .special-name { font-size: 10px; color: #00aa2a; margin-bottom: 4px; }

  .project-card { border: 1px solid #00aa2a; padding: 10px 12px; margin: 8px 0; }
  .project-name { font-size: 14px; color: #00ff41; font-weight: bold; }
  .project-desc { font-size: 11px; color: #00cc33; margin: 4px 0; }
  .project-tags { display: flex; flex-wrap: wrap; gap: 4px; margin-top: 6px; }
  .tag { font-size: 10px; border: 1px solid #00aa2a; padding: 1px 5px; color: #00aa2a; }
  .status-dot { display: inline-block; width: 8px; height: 8px; border-radius: 50%; margin-right: 4px; }
  .dot-green { background: #00ff41; box-shadow: 0 0 4px #00ff41; }
  .dot-amber { background: #ffaa00; box-shadow: 0 0 4px #ffaa00; }

  .skill-cmd { color: #00aa2a; font-size: 12px; }
  .skill-output { font-size: 11px; color: #00ff41; padding-left: 16px; display: flex; flex-wrap: wrap; gap: 6px; margin: 4px 0 10px; }
  .skill-badge { border: 1px solid #00ff41; padding: 2px 6px; font-size: 11px; }

  .quest { display: flex; align-items: flex-start; gap: 8px; font-size: 12px; margin: 5px 0; }
  .quest-done { color: #00ff41; }
  .quest-prog { color: #ffaa00; text-shadow: 0 0 4px #ffaa00; }
  .quest-tag { font-size: 10px; border: 1px solid; padding: 1px 4px; white-space: nowrap; }
  .qt-done { border-color: #00ff41; color: #00ff41; }
  .qt-prog { border-color: #ffaa00; color: #ffaa00; }

  .contact-line { font-size: 12px; margin: 5px 0; }
  .contact-cmd { color: #00aa2a; }
  .contact-val { color: #00ff41; text-decoration: none; }
  .contact-val:hover { text-shadow: 0 0 8px #00ff41; }

  .ascii-art { font-size: 9px; line-height: 1.1; color: #00ff41; text-shadow: 0 0 3px #00ff41; white-space: pre; overflow-x: auto; }

  .stats-imgs { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 8px; }
  .stats-placeholder { border: 1px solid #00aa2a; padding: 8px; text-align: center; font-size: 11px; color: #00aa2a; min-height: 80px; display: flex; align-items: center; justify-content: center; flex-direction: column; gap: 4px; }

  .boot-screen { padding: 20px; }
  .boot-line { font-size: 13px; margin: 3px 0; animation: fadeIn 0.3s ease; }
  @keyframes fadeIn { from{opacity:0;transform:translateX(-5px)} to{opacity:1;transform:translateX(0)} }

  .nav-tabs { display: flex; gap: 0; border-bottom: 1px solid #00ff41; margin-bottom: 0; flex-wrap: wrap; }
  .nav-tab { padding: 6px 14px; font-size: 12px; cursor: pointer; border: 1px solid transparent; border-bottom: none; color: #00aa2a; letter-spacing: 1px; font-family: 'Share Tech Mono', monospace; background: none; }
  .nav-tab:hover { color: #00ff41; background: #001a00; }
  .nav-tab.active { color: #00ff41; border-color: #00ff41; background: #001500; text-shadow: 0 0 6px #00ff41; }

  .tab-content { display: none; }
  .tab-content.active { display: block; }

  .footer-art { text-align: center; font-size: 11px; color: #006600; padding: 16px; border-top: 1px solid #003300; margin-top: 16px; letter-spacing: 2px; }

  .pip-outer { padding: 12px; }

  .header-top { display: flex; align-items: center; justify-content: space-between; border: 1px solid #00ff41; padding: 8px 14px; margin-bottom: 12px; box-shadow: 0 0 16px rgba(0,255,65,0.2); flex-wrap: wrap; gap: 8px; }
  .vault-logo { font-family: 'VT323', monospace; font-size: 32px; color: #00ff41; text-shadow: 0 0 14px #00ff41; }
  .header-right { text-align: right; font-size: 11px; color: #00aa2a; }

  .pip-name { font-family: 'VT323', monospace; font-size: 48px; color: #00ff41; text-shadow: 0 0 20px #00ff41, 0 0 40px rgba(0,255,65,0.3); line-height: 1; }
  .pip-role { font-size: 12px; color: #00cc33; letter-spacing: 1px; margin-top: 4px; }
</style>

<div class="pip crt-flicker" id="pipApp">
  <div class="scanlines"></div>

  <div id="bootScreen" class="boot-screen">
    <div id="bootLines"></div>
    <div style="margin-top:8px;font-size:13px;" id="bootProgress"></div>
  </div>

  <div id="mainContent" style="display:none;" class="pip-outer">
    <div class="header-top">
      <div>
        <div class="vault-logo">◈ VAULT-TEC PIP-BOY 3000 ◈</div>
        <div style="font-size:10px;color:#006600;letter-spacing:2px;">PERSONAL INFORMATION PROCESSOR</div>
      </div>
      <div class="header-right">
        <div>UNIT ID: KR-1337</div>
        <div>VAULT: 101</div>
        <div id="clock" style="color:#00ff41;"></div>
      </div>
    </div>

    <div class="section" style="text-align:center;padding:16px;">
      <div class="ascii-art" id="asciiArt"></div>
      <div style="margin-top:12px;">
        <div class="pip-name">KRISHNA SINGH ARYA</div>
        <div class="pip-role">> Backend Developer | Java Developer | Spring Boot Enthusiast <span class="cursor"></span></div>
      </div>
    </div>

    <div class="nav-tabs">
      <button class="nav-tab active" onclick="switchTab('status')">[ STATS ]</button>
      <button class="nav-tab" onclick="switchTab('skills')">[ SKILLS ]</button>
      <button class="nav-tab" onclick="switchTab('projects')">[ PROJECTS ]</button>
      <button class="nav-tab" onclick="switchTab('quests')">[ QUESTS ]</button>
      <button class="nav-tab" onclick="switchTab('data')">[ DATA ]</button>
      <button class="nav-tab" onclick="switchTab('contact')">[ RADIO ]</button>
    </div>

    <div id="tab-status" class="tab-content active" style="padding:12px 0;">
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:12px;">
        <div class="section">
          <div class="section-title">// STATUS PANEL</div>
          <div class="status-grid">
            <div class="status-item"><span class="status-label">LEVEL: </span><span class="status-val">22</span></div>
            <div class="status-item"><span class="status-label">XP: </span><span class="status-val">14,830</span></div>
            <div class="status-item"><span class="status-label">LOCATION: </span><span class="status-val">India</span></div>
            <div class="status-item"><span class="status-label">FOCUS: </span><span class="status-val">Spring Boot</span></div>
            <div class="status-item"><span class="status-label">STATUS: </span><span class="status-val" style="color:#00ff41;">● AVAILABLE</span></div>
            <div class="status-item"><span class="status-label">CLASS: </span><span class="status-val">Backend Dev</span></div>
          </div>
          <div style="margin-top:12px;font-size:11px;">
            <div class="progress-bar"><span style="color:#00aa2a;width:28px;">HP</span><div class="bar-track"><div class="bar-fill" style="width:90%"></div></div><span>90</span></div>
            <div class="progress-bar"><span style="color:#00aa2a;width:28px;">AP</span><div class="bar-track"><div class="bar-fill" style="width:75%"></div></div><span>75</span></div>
          </div>
        </div>

        <div class="section">
          <div class="section-title">// SPECIAL STATS</div>
          <div style="font-size:11px;">
            <div class="progress-bar"><span style="width:16px;color:#00ff41;font-family:VT323,monospace;font-size:16px;">S</span><span style="color:#00aa2a;width:90px;font-size:10px;">SPRING BOOT</span><div class="bar-track"><div class="bar-fill" id="bar-s" style="width:0%"></div></div><span id="val-s">9</span></div>
            <div class="progress-bar"><span style="width:16px;color:#00ff41;font-family:VT323,monospace;font-size:16px;">P</span><span style="color:#00aa2a;width:90px;font-size:10px;">PROB.SOLVING</span><div class="bar-track"><div class="bar-fill" id="bar-p" style="width:0%"></div></div><span id="val-p">8</span></div>
            <div class="progress-bar"><span style="width:16px;color:#00ff41;font-family:VT323,monospace;font-size:16px;">E</span><span style="color:#00aa2a;width:90px;font-size:10px;">ENDURANCE</span><div class="bar-track"><div class="bar-fill" id="bar-e" style="width:0%"></div></div><span id="val-e">9</span></div>
            <div class="progress-bar"><span style="width:16px;color:#00ff41;font-family:VT323,monospace;font-size:16px;">C</span><span style="color:#00aa2a;width:90px;font-size:10px;">COMMUNICATN</span><div class="bar-track"><div class="bar-fill" id="bar-c" style="width:0%"></div></div><span id="val-c">7</span></div>
            <div class="progress-bar"><span style="width:16px;color:#00ff41;font-family:VT323,monospace;font-size:16px;">I</span><span style="color:#00aa2a;width:90px;font-size:10px;">JAVA INTEL</span><div class="bar-track"><div class="bar-fill" id="bar-i" style="width:0%"></div></div><span id="val-i">9</span></div>
            <div class="progress-bar"><span style="width:16px;color:#00ff41;font-family:VT323,monospace;font-size:16px;">A</span><span style="color:#00aa2a;width:90px;font-size:10px;">API DEV</span><div class="bar-track"><div class="bar-fill" id="bar-a" style="width:0%"></div></div><span id="val-a">8</span></div>
            <div class="progress-bar"><span style="width:16px;color:#00ff41;font-family:VT323,monospace;font-size:16px;">L</span><span style="color:#00aa2a;width:90px;font-size:10px;">LEARNING</span><div class="bar-track"><div class="bar-fill" id="bar-l" style="width:0%"></div></div><span id="val-l">10</span></div>
          </div>
          <div style="font-size:10px;color:#006600;margin-top:8px;text-align:right;">SCALE: /10</div>
        </div>
      </div>
    </div>

    <div id="tab-skills" class="tab-content" style="padding:12px 0;">
      <div class="section">
        <div class="section-title">// SKILL TREE — ACTIVE LOADOUT</div>

        <div class="skill-cmd">$ skills --backend</div>
        <div class="skill-output">
          <span class="skill-badge">Java</span>
          <span class="skill-badge">Spring Boot</span>
          <span class="skill-badge">Spring Security</span>
          <span class="skill-badge">Hibernate</span>
          <span class="skill-badge">REST APIs</span>
          <span class="skill-badge">JWT Auth</span>
          <span class="skill-badge">Microservices</span>
        </div>

        <div class="skill-cmd">$ skills --database</div>
        <div class="skill-output">
          <span class="skill-badge">MySQL</span>
          <span class="skill-badge">PostgreSQL</span>
          <span class="skill-badge">Redis</span>
        </div>

        <div class="skill-cmd">$ skills --tools</div>
        <div class="skill-output">
          <span class="skill-badge">Git</span>
          <span class="skill-badge">Docker</span>
          <span class="skill-badge">Linux</span>
          <span class="skill-badge">IntelliJ IDEA</span>
          <span class="skill-badge">Postman</span>
          <span class="skill-badge">Maven</span>
        </div>

        <div class="skill-cmd">$ skills --proficiency</div>
        <div style="margin-top:8px;font-size:11px;">
          <div class="progress-bar"><span style="width:100px;color:#00aa2a;">Java</span><div class="bar-track"><div class="bar-fill" style="width:90%"></div></div><span>90%</span></div>
          <div class="progress-bar"><span style="width:100px;color:#00aa2a;">Spring Boot</span><div class="bar-track"><div class="bar-fill" style="width:85%"></div></div><span>85%</span></div>
          <div class="progress-bar"><span style="width:100px;color:#00aa2a;">REST APIs</span><div class="bar-track"><div class="bar-fill" style="width:88%"></div></div><span>88%</span></div>
          <div class="progress-bar"><span style="width:100px;color:#00aa2a;">MySQL</span><div class="bar-track"><div class="bar-fill" style="width:80%"></div></div><span>80%</span></div>
          <div class="progress-bar"><span style="width:100px;color:#00aa2a;">Docker</span><div class="bar-track"><div class="bar-fill" style="width:60%"></div></div><span>60%</span></div>
          <div class="progress-bar"><span style="width:100px;color:#00aa2a;">Kubernetes</span><div class="bar-track"><div class="bar-fill" style="width:30%"></div></div><span>30%</span></div>
        </div>
      </div>
    </div>

    <div id="tab-projects" class="tab-content" style="padding:12px 0;">
      <div class="section">
        <div class="section-title">// PROJECT DIRECTORY</div>
        <div style="font-size:12px;color:#00aa2a;margin-bottom:10px;">$ ls -la /projects/</div>

        <div style="font-size:11px;color:#006600;margin-bottom:8px;">
          /projects<br>
          ├── NoteCheckingAndSaving/<br>
          ├── ProxyCacheServer/<br>
          ├── ChatApplication/<br>
          └── SecurityPractice/
        </div>

        <div class="project-card">
          <div style="display:flex;justify-content:space-between;align-items:center;">
            <div class="project-name">📁 NoteCheckingAndSaving</div>
            <div style="font-size:10px;"><span class="status-dot dot-green"></span><span style="color:#00ff41;">DEPLOYED</span></div>
          </div>
          <div class="project-desc">> A Spring Boot application for creating, managing and persisting notes with authentication. Supports full CRUD operations with secure endpoints.</div>
          <div class="project-tags">
            <span class="tag">Java</span><span class="tag">Spring Boot</span><span class="tag">Hibernate</span><span class="tag">MySQL</span><span class="tag">JWT</span>
          </div>
          <div style="margin-top:8px;font-size:11px;"><a class="contact-val" href="https://github.com/Krishna" style="font-size:11px;">$ git clone github.com/Krishna/NoteCheckingAndSaving</a></div>
        </div>

        <div class="project-card">
          <div style="display:flex;justify-content:space-between;align-items:center;">
            <div class="project-name">📁 ProxyCacheServer</div>
            <div style="font-size:10px;"><span class="status-dot dot-green"></span><span style="color:#00ff41;">DEPLOYED</span></div>
          </div>
          <div class="project-desc">> A high-performance proxy cache server built in Java. Intercepts HTTP requests, caches responses and serves cached data on subsequent hits.</div>
          <div class="project-tags">
            <span class="tag">Java</span><span class="tag">HTTP</span><span class="tag">Caching</span><span class="tag">Proxy</span><span class="tag">Networking</span>
          </div>
          <div style="margin-top:8px;font-size:11px;"><a class="contact-val" href="https://github.com/Krishna" style="font-size:11px;">$ git clone github.com/Krishna/ProxyCacheServer</a></div>
        </div>

        <div class="project-card">
          <div style="display:flex;justify-content:space-between;align-items:center;">
            <div class="project-name">📁 ChatApplication</div>
            <div style="font-size:10px;"><span class="status-dot dot-amber"></span><span style="color:#ffaa00;">IN PROGRESS</span></div>
          </div>
          <div class="project-desc">> Real-time chat application with WebSocket support. Features user authentication, chat rooms, message persistence and online presence indicators.</div>
          <div class="project-tags">
            <span class="tag">Spring Boot</span><span class="tag">WebSocket</span><span class="tag">JWT</span><span class="tag">PostgreSQL</span>
          </div>
          <div style="margin-top:8px;font-size:11px;"><a class="contact-val" href="https://github.com/Krishna" style="font-size:11px;">$ git clone github.com/Krishna/ChatApplication</a></div>
        </div>

        <div class="project-card">
          <div style="display:flex;justify-content:space-between;align-items:center;">
            <div class="project-name">📁 SecurityPractice</div>
            <div style="font-size:10px;"><span class="status-dot dot-green"></span><span style="color:#00ff41;">DEPLOYED</span></div>
          </div>
          <div class="project-desc">> Comprehensive Spring Security implementation showcase. Includes OAuth2, JWT, role-based access, method security and custom filters.</div>
          <div class="project-tags">
            <span class="tag">Spring Security</span><span class="tag">OAuth2</span><span class="tag">JWT</span><span class="tag">RBAC</span>
          </div>
          <div style="margin-top:8px;font-size:11px;"><a class="contact-val" href="https://github.com/Krishna" style="font-size:11px;">$ git clone github.com/Krishna/SecurityPractice</a></div>
        </div>
      </div>
    </div>

    <div id="tab-quests" class="tab-content" style="padding:12px 0;">
      <div class="section">
        <div class="section-title">// QUEST LOG — ACHIEVEMENTS</div>
        <div style="font-size:11px;color:#00aa2a;margin-bottom:10px;">$ achievements --list --all</div>

        <div style="margin-bottom:12px;">
          <div style="font-size:11px;color:#00aa2a;margin-bottom:6px;">── MAIN QUESTS ──</div>
          <div class="quest"><span class="quest-tag qt-done">COMPLETED</span><span class="quest-done">Built and deployed Production REST APIs</span></div>
          <div class="quest"><span class="quest-tag qt-done">COMPLETED</span><span class="quest-done">Implemented JWT Authentication system</span></div>
          <div class="quest"><span class="quest-tag qt-done">COMPLETED</span><span class="quest-done">Designed Relational Database schemas</span></div>
          <div class="quest"><span class="quest-tag qt-done">COMPLETED</span><span class="quest-done">Spring Security — Full implementation</span></div>
          <div class="quest"><span class="quest-tag qt-done">COMPLETED</span><span class="quest-done">Built Proxy Cache Server from scratch</span></div>
          <div class="quest"><span class="quest-tag qt-prog">IN PROGRESS</span><span class="quest-prog">Master Docker & containerization</span></div>
          <div class="quest"><span class="quest-tag qt-prog">IN PROGRESS</span><span class="quest-prog">Learn Kubernetes orchestration</span></div>
          <div class="quest"><span class="quest-tag qt-prog">IN PROGRESS</span><span class="quest-prog">Microservices architecture — deep dive</span></div>
        </div>

        <div>
          <div style="font-size:11px;color:#00aa2a;margin-bottom:6px;">── SIDE QUESTS ──</div>
          <div class="quest"><span class="quest-tag qt-done">COMPLETED</span><span class="quest-done">Mastered IntelliJ IDEA ecosystem</span></div>
          <div class="quest"><span class="quest-tag qt-done">COMPLETED</span><span class="quest-done">Learned Git branching strategies</span></div>
          <div class="quest"><span class="quest-tag qt-prog">IN PROGRESS</span><span class="quest-prog">Explore system design patterns</span></div>
          <div class="quest"><span class="quest-tag qt-prog">IN PROGRESS</span><span class="quest-prog">Open source contribution — first PR</span></div>
        </div>

        <div style="margin-top:12px;border:1px solid #003300;padding:8px;font-size:11px;">
          <span style="color:#00aa2a;">COMPLETION: </span>
          <div class="bar-track" style="display:inline-block;width:60%;vertical-align:middle;margin:0 6px;"><div class="bar-fill" style="width:62%"></div></div>
          <span>62%</span>
        </div>
      </div>
    </div>

    <div id="tab-data" class="tab-content" style="padding:12px 0;">
      <div class="section">
        <div class="section-title">// GITHUB STATS TERMINAL</div>
        <div style="font-size:11px;color:#00aa2a;margin-bottom:10px;">$ github-stats --fetch --user Krishna</div>

        <div class="stats-imgs">
          <div class="stats-placeholder">
            <div style="font-size:10px;color:#006600;">[ GITHUB STATS CARD ]</div>
            <img src="https://github-readme-stats.vercel.app/api?username=Krishna&show_icons=true&theme=terminal&bg_color=0a0a0a&title_color=00ff41&text_color=00cc33&icon_color=00ff41&border_color=00ff41" style="max-width:100%;opacity:0.85;" onerror="this.parentElement.innerHTML='<div style=\'color:#006600;font-size:10px;\'>[ GITHUB STATS ]<br>Replace username in URL ]</div>'"/>
          </div>
          <div class="stats-placeholder">
            <div style="font-size:10px;color:#006600;">[ STREAK STATS ]</div>
            <img src="https://github-readme-streak-stats.herokuapp.com/?user=Krishna&theme=terminal&background=0a0a0a&ring=00ff41&fire=00cc33&currStreakLabel=00ff41&border=00ff41" style="max-width:100%;opacity:0.85;" onerror="this.parentElement.innerHTML='<div style=\'color:#006600;font-size:10px;\'>[ STREAK STATS ]<br>[ Replace username in URL ]</div>'"/>
          </div>
        </div>
        <div style="margin-top:8px;" class="stats-placeholder">
          <div style="font-size:10px;color:#006600;">[ TOP LANGUAGES ]</div>
          <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=Krishna&layout=compact&theme=terminal&bg_color=0a0a0a&title_color=00ff41&text_color=00cc33&border_color=00ff41" style="max-width:100%;opacity:0.85;" onerror="this.parentElement.innerHTML='<div style=\'color:#006600;font-size:10px;\'>[ TOP LANGUAGES ]<br>[ Replace username in URL ]</div>'"/>
        </div>
        <div style="font-size:10px;color:#003300;margin-top:8px;">NOTE: Replace 'Krishna' with your actual GitHub username in the image URLs.</div>
      </div>
    </div>

    <div id="tab-contact" class="tab-content" style="padding:12px 0;">
      <div class="section">
        <div class="section-title">// RADIO FREQUENCIES — CONTACT</div>
        <div style="font-size:11px;color:#00aa2a;margin-bottom:12px;">$ contact --scan --all-channels</div>

        <div style="font-size:11px;color:#006600;margin-bottom:10px;">Scanning frequencies... SIGNAL FOUND</div>

        <div class="contact-line">
          <span class="contact-cmd">$ contact --github </span>
          <a class="contact-val" href="https://github.com/Krishna" target="_blank">→ github.com/Krishna</a>
        </div>
        <div class="contact-line">
          <span class="contact-cmd">$ contact --linkedin </span>
          <a class="contact-val" href="https://linkedin.com/in/Krishna" target="_blank">→ linkedin.com/in/Krishna</a>
        </div>
        <div class="contact-line">
          <span class="contact-cmd">$ contact --email </span>
          <a class="contact-val" href="mailto:krishna@example.com">→ krishna@example.com</a>
        </div>
        <div class="contact-line">
          <span class="contact-cmd">$ contact --status </span>
          <span style="color:#00ff41;">→ <span style="animation:blink 1s infinite step-end;">●</span> OPEN TO OPPORTUNITIES</span>
        </div>

        <div style="margin-top:16px;border:1px solid #003300;padding:10px;font-size:11px;color:#00aa2a;">
          <div>> RESPONSE TIME: ~24 hours</div>
          <div>> PREFERRED: Backend roles | Java | Spring Boot</div>
          <div>> TIMEZONE: IST (UTC+5:30)</div>
          <div>> VAULT: India <span class="cursor"></span></div>
        </div>
      </div>
    </div>

    <div class="footer-art">
      ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━<br>
      ◈  END OF TRANSMISSION  ◈  VAULT-TEC PERSONAL INFORMATION PROCESSOR  ◈<br>
      ◈  PIP-BOY 3000 MK IV  ◈  SERIAL NO: VT-KR-1337  ◈  VAULT 101  ◈<br>
      ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
    </div>
  </div>
</div>

<script>
const asciiKrishna = `
██╗  ██╗██████╗ ██╗███████╗██╗  ██╗███╗   ██╗ █████╗
██║ ██╔╝██╔══██╗██║██╔════╝██║  ██║████╗  ██║██╔══██╗
█████╔╝ ██████╔╝██║███████╗███████║██╔██╗ ██║███████║
██╔═██╗ ██╔══██╗██║╚════██║██╔══██║██║╚██╗██║██╔══██║
██║  ██╗██║  ██║██║███████║██║  ██║██║ ╚████║██║  ██║
╚═╝  ╚═╝╚═╝  ╚═╝╚═╝╚══════╝╚═╝  ╚═╝╚═╝  ╚═══╝╚═╝  ╚═╝`;

document.getElementById('asciiArt').textContent = asciiKrishna;

const bootMessages = [
  { text: "VAULT-TEC BIOS v2.01.07 ... OK", delay: 0 },
  { text: "Initializing Vault-Tec Personal Terminal...", delay: 200 },
  { text: "Checking memory banks... [████████████] 100%", delay: 500 },
  { text: "Loading SPECIAL stat module... OK", delay: 800 },
  { text: "Connecting to Vault-Tec mainframe... OK", delay: 1100 },
  { text: "Authenticating user KR-1337... GRANTED", delay: 1400 },
  { text: "Loading profile: KRISHNA", delay: 1700 },
  { text: "Decrypting skill tree... OK", delay: 2000 },
  { text: "Mounting project directories... OK", delay: 2300 },
  { text: "PIP-BOY OS 3.0 ready.", delay: 2600 },
];

const bootEl = document.getElementById('bootLines');
const progressEl = document.getElementById('bootProgress');

bootMessages.forEach((msg, i) => {
  setTimeout(() => {
    const line = document.createElement('div');
    line.className = 'boot-line glow-dim';
    line.style.color = i === bootMessages.length - 1 ? '#00ff41' : '#00aa2a';
    line.textContent = '> ' + msg.text;
    bootEl.appendChild(line);
    const pct = Math.round(((i + 1) / bootMessages.length) * 100);
    const filled = Math.round(pct / 5);
    progressEl.innerHTML = `<span style="color:#00aa2a;">LOADING: [</span><span style="color:#00ff41;">${'█'.repeat(filled)}${'░'.repeat(20 - filled)}</span><span style="color:#00aa2a;">] ${pct}%</span>`;
  }, msg.delay);
});

setTimeout(() => {
  document.getElementById('bootScreen').style.display = 'none';
  document.getElementById('mainContent').style.display = 'block';
  animateBars();
}, 3200);

function animateBars() {
  const bars = [
    { id: 'bar-s', val: 9 },
    { id: 'bar-p', val: 8 },
    { id: 'bar-e', val: 9 },
    { id: 'bar-c', val: 7 },
    { id: 'bar-i', val: 9 },
    { id: 'bar-a', val: 8 },
    { id: 'bar-l', val: 10 },
  ];
  bars.forEach((b, i) => {
    setTimeout(() => {
      const el = document.getElementById(b.id);
      if (el) el.style.width = (b.val * 10) + '%';
    }, i * 100);
  });
}

function switchTab(name) {
  document.querySelectorAll('.tab-content').forEach(t => t.classList.remove('active'));
  document.querySelectorAll('.nav-tab').forEach(t => t.classList.remove('active'));
  document.getElementById('tab-' + name).classList.add('active');
  event.target.classList.add('active');
  if (name === 'status') setTimeout(animateBars, 100);
}

function updateClock() {
  const now = new Date();
  const h = String(now.getHours()).padStart(2, '0');
  const m = String(now.getMinutes()).padStart(2, '0');
  const s = String(now.getSeconds()).padStart(2, '0');
  const el = document.getElementById('clock');
  if (el) el.textContent = h + ':' + m + ':' + s;
}
updateClock();
setInterval(updateClock, 1000);
</script>
