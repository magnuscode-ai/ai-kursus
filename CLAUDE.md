<!DOCTYPE html>
<html lang="da">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Claude Code Guide — Fra Nybegynder til Pro</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Mono:wght@400;500&family=Lora:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0a0a0f;
    --surface: #111118;
    --surface2: #1a1a24;
    --border: #2a2a3a;
    --accent: #7c6dfa;
    --accent2: #e05cff;
    --green: #22d3a6;
    --amber: #f59e0b;
    --red: #f43f5e;
    --text: #e8e8f0;
    --muted: #7070a0;
    --ink: #c4c4d8;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    font-family: 'Lora', serif;
    background: var(--bg);
    color: var(--text);
    line-height: 1.7;
    overflow-x: hidden;
  }

  /* ─── HERO ─── */
  .hero {
    position: relative;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    padding: 60px 24px;
    overflow: hidden;
  }

  .hero-bg {
    position: absolute; inset: 0;
    background:
      radial-gradient(ellipse 80% 60% at 50% 0%, rgba(124,109,250,0.18) 0%, transparent 70%),
      radial-gradient(ellipse 60% 40% at 80% 80%, rgba(224,92,255,0.10) 0%, transparent 60%),
      radial-gradient(ellipse 40% 50% at 20% 60%, rgba(34,211,166,0.07) 0%, transparent 60%);
  }

  .hero-grid {
    position: absolute; inset: 0;
    background-image:
      linear-gradient(rgba(124,109,250,0.06) 1px, transparent 1px),
      linear-gradient(90deg, rgba(124,109,250,0.06) 1px, transparent 1px);
    background-size: 50px 50px;
    mask-image: radial-gradient(ellipse 80% 80% at 50% 50%, black 20%, transparent 80%);
  }

  .badge-top {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: rgba(124,109,250,0.12);
    border: 1px solid rgba(124,109,250,0.3);
    border-radius: 100px;
    padding: 6px 16px;
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    color: var(--accent);
    letter-spacing: 0.1em;
    text-transform: uppercase;
    margin-bottom: 32px;
    animation: fadeDown 0.6s ease both;
  }

  .hero h1 {
    font-family: 'Syne', sans-serif;
    font-size: clamp(40px, 8vw, 88px);
    font-weight: 800;
    line-height: 1.0;
    letter-spacing: -0.03em;
    animation: fadeUp 0.7s ease 0.1s both;
  }

  .hero h1 .line1 { display: block; color: var(--text); }
  .hero h1 .line2 {
    display: block;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  .hero-sub {
    font-size: 18px;
    color: var(--muted);
    margin-top: 24px;
    max-width: 520px;
    animation: fadeUp 0.7s ease 0.2s both;
  }

  .hero-toc {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    justify-content: center;
    margin-top: 48px;
    animation: fadeUp 0.7s ease 0.3s both;
  }

  .toc-chip {
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 8px 16px;
    font-family: 'DM Mono', monospace;
    font-size: 13px;
    color: var(--ink);
    cursor: pointer;
    transition: all 0.2s;
    text-decoration: none;
  }
  .toc-chip:hover {
    border-color: var(--accent);
    color: var(--accent);
    background: rgba(124,109,250,0.08);
    transform: translateY(-2px);
  }

  /* ─── MAIN CONTENT ─── */
  .main { max-width: 860px; margin: 0 auto; padding: 0 24px 120px; }

  /* Section */
  .section {
    margin-top: 100px;
    scroll-margin-top: 40px;
  }

  .section-label {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 12px;
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

  .section-title {
    font-family: 'Syne', sans-serif;
    font-size: clamp(28px, 5vw, 42px);
    font-weight: 700;
    line-height: 1.1;
    margin-bottom: 20px;
  }

  .section-intro {
    font-size: 17px;
    color: var(--ink);
    margin-bottom: 40px;
    max-width: 680px;
  }

  /* Steps */
  .steps { display: flex; flex-direction: column; gap: 20px; }

  .step {
    display: grid;
    grid-template-columns: 56px 1fr;
    gap: 20px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 28px;
    transition: border-color 0.2s;
    position: relative;
    overflow: hidden;
  }
  .step::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--accent), transparent);
    opacity: 0;
    transition: opacity 0.3s;
  }
  .step:hover { border-color: rgba(124,109,250,0.4); }
  .step:hover::before { opacity: 1; }

  .step-num {
    width: 48px; height: 48px;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'Syne', sans-serif;
    font-weight: 800;
    font-size: 20px;
    color: #fff;
    flex-shrink: 0;
    margin-top: 2px;
  }

  .step-content h3 {
    font-family: 'Syne', sans-serif;
    font-size: 20px;
    font-weight: 700;
    margin-bottom: 8px;
    color: var(--text);
  }

  .step-content p {
    color: var(--ink);
    font-size: 15px;
    line-height: 1.65;
    margin-bottom: 12px;
  }

  /* Code blocks */
  .code-block {
    background: #0d0d14;
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 14px 18px;
    margin: 12px 0;
    font-family: 'DM Mono', monospace;
    font-size: 13px;
    color: var(--green);
    position: relative;
    overflow-x: auto;
  }
  .code-block .comment { color: var(--muted); }
  .code-block .cmd { color: var(--accent); }

  .copy-btn {
    position: absolute;
    top: 10px; right: 10px;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 4px 10px;
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: var(--muted);
    cursor: pointer;
    transition: all 0.2s;
  }
  .copy-btn:hover { color: var(--accent); border-color: var(--accent); }

  /* Tags */
  .tag {
    display: inline-block;
    padding: 2px 10px;
    border-radius: 6px;
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    font-weight: 500;
  }
  .tag-win { background: rgba(59,130,246,0.15); color: #60a5fa; }
  .tag-mac { background: rgba(34,211,166,0.15); color: var(--green); }
  .tag-both { background: rgba(124,109,250,0.15); color: var(--accent); }
  .tag-tip { background: rgba(245,158,11,0.15); color: var(--amber); }
  .tag-warn { background: rgba(244,63,94,0.15); color: var(--red); }

  /* Info boxes */
  .info-box {
    border-radius: 12px;
    padding: 18px 22px;
    margin: 16px 0;
    font-size: 15px;
    display: flex;
    gap: 14px;
    align-items: flex-start;
  }
  .info-box .icon { font-size: 20px; flex-shrink: 0; margin-top: 1px; }
  .info-tip { background: rgba(245,158,11,0.08); border: 1px solid rgba(245,158,11,0.25); color: var(--ink); }
  .info-warn { background: rgba(244,63,94,0.08); border: 1px solid rgba(244,63,94,0.25); color: var(--ink); }
  .info-good { background: rgba(34,211,166,0.08); border: 1px solid rgba(34,211,166,0.25); color: var(--ink); }

  /* Cards grid */
  .cards {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    gap: 16px;
    margin-top: 32px;
  }

  .card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 24px;
    transition: all 0.2s;
  }
  .card:hover { border-color: rgba(124,109,250,0.35); transform: translateY(-3px); }

  .card-icon { font-size: 28px; margin-bottom: 12px; }
  .card h4 {
    font-family: 'Syne', sans-serif;
    font-size: 16px;
    font-weight: 700;
    margin-bottom: 8px;
  }
  .card p { font-size: 14px; color: var(--muted); line-height: 1.6; }

  /* Prompt examples */
  .prompt-card {
    background: var(--surface2);
    border: 1px solid var(--border);
    border-left: 3px solid var(--accent);
    border-radius: 10px;
    padding: 18px 20px;
    margin: 12px 0;
    font-size: 14px;
    color: var(--ink);
    line-height: 1.65;
    font-family: 'DM Mono', monospace;
    position: relative;
  }
  .prompt-card .label {
    font-size: 10px;
    text-transform: uppercase;
    letter-spacing: 0.12em;
    color: var(--accent);
    margin-bottom: 8px;
    font-family: 'DM Mono', monospace;
  }

  /* Table */
  .comp-table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 24px;
    font-size: 14px;
  }
  .comp-table th {
    background: var(--surface2);
    padding: 12px 16px;
    text-align: left;
    font-family: 'Syne', sans-serif;
    font-size: 13px;
    color: var(--muted);
    border-bottom: 1px solid var(--border);
  }
  .comp-table td {
    padding: 14px 16px;
    border-bottom: 1px solid rgba(42,42,58,0.5);
    color: var(--ink);
    vertical-align: top;
  }
  .comp-table tr:hover td { background: rgba(124,109,250,0.04); }

  /* CLAUDE.md block */
  .file-block {
    background: #0a0a12;
    border: 1px solid var(--border);
    border-radius: 14px;
    overflow: hidden;
    margin: 20px 0;
  }
  .file-header {
    background: var(--surface2);
    padding: 12px 18px;
    font-family: 'DM Mono', monospace;
    font-size: 13px;
    color: var(--muted);
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    gap: 8px;
  }
  .file-dot { width: 10px; height: 10px; border-radius: 50%; }
  .file-body {
    padding: 20px;
    font-family: 'DM Mono', monospace;
    font-size: 13px;
    line-height: 1.75;
    color: var(--ink);
    white-space: pre-wrap;
  }
  .file-body .md-h1 { color: var(--text); font-size: 16px; font-family: 'Syne', sans-serif; font-weight: 700; }
  .file-body .md-h2 { color: var(--accent); }
  .file-body .md-comment { color: var(--muted); }
  .file-body .md-val { color: var(--green); }

  /* OS tabs */
  .os-tabs {
    display: flex;
    gap: 8px;
    margin-bottom: -1px;
  }
  .os-tab {
    padding: 8px 18px;
    border-radius: 8px 8px 0 0;
    font-family: 'DM Mono', monospace;
    font-size: 13px;
    cursor: pointer;
    border: 1px solid var(--border);
    border-bottom: none;
    background: var(--surface);
    color: var(--muted);
    transition: all 0.2s;
  }
  .os-tab.active { background: var(--surface2); color: var(--text); border-color: rgba(124,109,250,0.4); }
  .os-content { display: none; }
  .os-content.active { display: block; }

  /* Divider */
  .divider {
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--border), transparent);
    margin: 80px 0;
  }

  /* Checklist */
  .checklist { list-style: none; display: flex; flex-direction: column; gap: 10px; margin-top: 20px; }
  .checklist li {
    display: flex; gap: 12px; align-items: flex-start;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 14px 18px;
    font-size: 15px;
    color: var(--ink);
  }
  .checklist li::before {
    content: '✓';
    color: var(--green);
    font-family: 'DM Mono', monospace;
    font-weight: 700;
    flex-shrink: 0;
  }

  /* Footer */
  .footer {
    text-align: center;
    padding: 80px 24px 40px;
    color: var(--muted);
    font-size: 14px;
  }

  /* Animations */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeDown {
    from { opacity: 0; transform: translateY(-12px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* Scroll animations */
  .reveal {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.6s ease, transform 0.6s ease;
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }

  /* Progress bar */
  .progress-bar {
    position: fixed;
    top: 0; left: 0;
    height: 3px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    width: 0%;
    transition: width 0.1s;
    z-index: 999;
  }

  @media (max-width: 600px) {
    .step { grid-template-columns: 1fr; }
    .step-num { width: 36px; height: 36px; font-size: 16px; border-radius: 8px; }
    .cards { grid-template-columns: 1fr; }
  }
</style>
</head>
<body>

<div class="progress-bar" id="progressBar"></div>

<!-- HERO -->
<section class="hero">
  <div class="hero-bg"></div>
  <div class="hero-grid"></div>
  <div class="badge-top">⚡ Din komplette guide</div>
  <h1>
    <span class="line1">Claude Code</span>
    <span class="line2">Fra 0 til Pro</span>
  </h1>
  <p class="hero-sub">Specielt lavet til akademiet-ai.dk — lær at bygge dine kurser hurtigere, bedre og uden at copy-paste kode.</p>
  <div class="hero-toc">
    <a href="#del1" class="toc-chip">01 — Hvad er Claude Code?</a>
    <a href="#del2" class="toc-chip">02 — Installation</a>
    <a href="#del3" class="toc-chip">03 — Første gang</a>
    <a href="#del4" class="toc-chip">04 — CLAUDE.md</a>
    <a href="#del5" class="toc-chip">05 — Prompts der virker</a>
    <a href="#del6" class="toc-chip">06 — Workflow med GitHub</a>
    <a href="#del7" class="toc-chip">07 — Pro-tricks</a>
  </div>
</section>

<div class="main">

  <!-- DEL 1 -->
  <section class="section reveal" id="del1">
    <div class="section-label">01 — Forstå det</div>
    <h2 class="section-title">Hvad er Claude Code egentlig?</h2>
    <p class="section-intro">Det er ikke en chat. Det er en AI der sidder <em>inde</em> i din projektmappe og kan læse, skrive og ændre alle dine filer på samme tid.</p>

    <table class="comp-table">
      <thead>
        <tr>
          <th>Claude Chat (som nu)</th>
          <th>Claude Code</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Du copy-paster kode ind og ud</td>
          <td>Claude læser og ændrer filerne direkte</td>
        </tr>
        <tr>
          <td>Kan kun se det du sender</td>
          <td>Ser alle dine filer på én gang</td>
        </tr>
        <tr>
          <td>Mister kontekst efter lang tid</td>
          <td>CLAUDE.md holder konteksten altid frisk</td>
        </tr>
        <tr>
          <td>Godt til planlægning og idéer</td>
          <td>Godt til at bygge og ændre kode</td>
        </tr>
        <tr>
          <td>Du sætter koden ind selv</td>
          <td>Claude committer direkte til GitHub</td>
        </tr>
      </tbody>
    </table>

    <div class="info-box info-good" style="margin-top:28px;">
      <span class="icon">💡</span>
      <div><strong>TL;DR:</strong> Brug chatten til at <em>planlægge</em> hvad du vil bygge. Brug Claude Code til at <em>bygge det</em>. De to ting supplerer hinanden perfekt.</div>
    </div>
  </section>

  <div class="divider"></div>

  <!-- DEL 2 -->
  <section class="section reveal" id="del2">
    <div class="section-label">02 — Opsætning</div>
    <h2 class="section-title">Installation trin-for-trin</h2>
    <p class="section-intro">Følg trinene i rækkefølge. Hop ikke over noget.</p>

    <div class="steps">

      <div class="step reveal">
        <div class="step-num">1</div>
        <div class="step-content">
          <h3>Installer Node.js <span class="tag tag-both">Begge systemer</span></h3>
          <p>Claude Code kræver Node.js version 18 eller nyere. Tjek om du allerede har det:</p>
          <div class="code-block">
            <button class="copy-btn" onclick="copyCode(this)">Kopiér</button>
            <span class="cmd">node --version</span>
            <br><span class="comment"># Skal vise: v18.x.x eller højere</span>
          </div>
          <p>Har du det ikke, eller er det en ældre version? Download fra <strong>nodejs.org</strong> og installer LTS-versionen.</p>
        </div>
      </div>

      <div class="step reveal">
        <div class="step-num">2</div>
        <div class="step-content">
          <h3>Installer VS Code <span class="tag tag-both">Anbefalet editor</span></h3>
          <p>Hvis du ikke allerede har det: gå til <strong>code.visualstudio.com</strong> og download. Det er gratis. Sørg for at have version 1.85 eller nyere.</p>
          <div class="info-box info-tip">
            <span class="icon">⚠️</span>
            <div><strong>Windows-bruger?</strong> Du skal installere WSL2 (Windows Subsystem for Linux). Søg "WSL2 install" på Microsoft.com — det er et enkelt trin i PowerShell.</div>
          </div>
        </div>
      </div>

      <div class="step reveal">
        <div class="step-num">3</div>
        <div class="step-content">
          <h3>Installer Claude Code via terminal <span class="tag tag-both">Begge systemer</span></h3>
          <p>Åbn terminal (Mac: Cmd+Space → "Terminal" / Windows: søg "WSL") og kør:</p>
          <div class="code-block">
            <button class="copy-btn" onclick="copyCode(this)">Kopiér</button>
            <span class="cmd">npm install -g @anthropic-ai/claude-code</span>
          </div>
          <p>Vent til det er færdigt (kan tage 1-2 min). Tjek at det virkede:</p>
          <div class="code-block">
            <button class="copy-btn" onclick="copyCode(this)">Kopiér</button>
            <span class="cmd">claude --version</span>
          </div>
        </div>
      </div>

      <div class="step reveal">
        <div class="step-num">4</div>
        <div class="step-content">
          <h3>Log ind med Claude Pro <span class="tag tag-mac">OAuth — ingen API-nøgle</span></h3>
          <p>Da du har Claude Pro, logger du ind med OAuth — det vil sige den åbner bare din browser og du logger ind som normalt. Ingen API-nøgle, ingen ekstra betaling.</p>
          <div class="code-block">
            <button class="copy-btn" onclick="copyCode(this)">Kopiér</button>
            <span class="cmd">claude</span>
            <br><span class="comment"># Følg instrukserne i terminalen — den åbner din browser</span>
          </div>
          <div class="info-box info-good">
            <span class="icon">✅</span>
            <div>Første gang du kører <code>claude</code> starter den en guide. Godkend de permissions den beder om — det er nødvendigt for at den kan læse og skrive filer.</div>
          </div>
        </div>
      </div>

      <div class="step reveal">
        <div class="step-num">5</div>
        <div class="step-content">
          <h3>Installer VS Code-udvidelsen <span class="tag tag-tip">Anbefalet</span></h3>
          <p>I VS Code: tryk <strong>Ctrl+Shift+X</strong> (Windows) eller <strong>Cmd+Shift+X</strong> (Mac), søg "Claude Code" og installer den officielle udvidelse fra Anthropic. Den giver dig en panel ved siden af din kode hvor du kan se ændringer og acceptere/afvise dem visuelt.</p>
        </div>
      </div>

    </div>
  </section>

  <div class="divider"></div>

  <!-- DEL 3 -->
  <section class="section reveal" id="del3">
    <div class="section-label">03 — Første gang</div>
    <h2 class="section-title">Åbn dit Akademiet-AI-projekt</h2>
    <p class="section-intro">Sådan kommer du i gang med dit eksisterende projekt på GitHub.</p>

    <div class="steps">

      <div class="step reveal">
        <div class="step-num">1</div>
        <div class="step-content">
          <h3>Klon dit projekt (første gang)</h3>
          <p>Hvis du ikke allerede har projektet lokalt på din computer, klon det fra GitHub:</p>
          <div class="code-block">
            <button class="copy-btn" onclick="copyCode(this)">Kopiér</button>
            <span class="cmd">git clone https://github.com/magnuscode-ai/ai-kursus</span>
            <br><span class="cmd">cd ai-kursus</span>
          </div>
          <p>Har du det allerede på din computer? Åbn den mappe direkte i VS Code (<strong>File → Open Folder</strong>).</p>
        </div>
      </div>

      <div class="step reveal">
        <div class="step-num">2</div>
        <div class="step-content">
          <h3>Åbn terminalen i den rigtige mappe</h3>
          <p>I VS Code: tryk <strong>Ctrl+`</strong> (backtick — tasten til venstre for 1). Det åbner terminalen direkte i din projektmappe. Tjek at du er det rigtige sted:</p>
          <div class="code-block">
            <button class="copy-btn" onclick="copyCode(this)">Kopiér</button>
            <span class="cmd">ls</span>
            <br><span class="comment"># Du skal se dine filer: platform.html, eksamen-d.html osv.</span>
          </div>
        </div>
      </div>

      <div class="step reveal">
        <div class="step-num">3</div>
        <div class="step-content">
          <h3>Start Claude Code i projektet</h3>
          <div class="code-block">
            <button class="copy-btn" onclick="copyCode(this)">Kopiér</button>
            <span class="cmd">claude</span>
          </div>
          <p>Nu starter Claude Code og du kan begynde at skrive til den ligesom i chatten — bare direkte i terminalen. Den kender nu alle dine filer.</p>
          <div class="info-box info-good">
            <span class="icon">🎉</span>
            <div>Du er nu i gang! Prøv at skrive: <em>"Hvad er der i denne mappe?"</em> — Claude svarer og lister dine filer op.</div>
          </div>
        </div>
      </div>

    </div>
  </section>

  <div class="divider"></div>

  <!-- DEL 4 -->
  <section class="section reveal" id="del4">
    <div class="section-label">04 — Din hemmelige våben</div>
    <h2 class="section-title">CLAUDE.md filen</h2>
    <p class="section-intro">CLAUDE.md er en tekstfil du lægger i roden af dit projekt. Den fortæller Claude Code alt om dit projekt <em>hver eneste session</em>. Det er det der erstatter at du skal forklare alting forfra hele tiden.</p>

    <div class="info-box info-tip">
      <span class="icon">⭐</span>
      <div><strong>Dette er det vigtigste trin.</strong> En god CLAUDE.md er forskellen på en Claude der gætter og en Claude der kender dit projekt indefra og ud.</div>
    </div>

    <p style="margin-top: 24px; color: var(--ink); font-size: 15px;">Opret filen i din projektmappe (<code>ai-kursus/CLAUDE.md</code>) og indsæt dette som udgangspunkt:</p>

    <div class="file-block reveal">
      <div class="file-header">
        <div class="file-dot" style="background:#f43f5e"></div>
        <div class="file-dot" style="background:#f59e0b"></div>
        <div class="file-dot" style="background:#22d3a6"></div>
        &nbsp; CLAUDE.md — akademiet-ai.dk
      </div>
      <div class="file-body"><span class="md-h1"># akademiet-ai.dk — AI-kursus Platform</span>

<span class="md-h2">## Projekt-oversigt</span>
Dette er en dansk AI-uddannelsesplatform (Duolingo for AI).
Hosted på GitHub Pages: magnuscode-ai.github.io/ai-kursus
Domæne: akademiet-ai.dk

<span class="md-h2">## Teknisk stack</span>
- Ren HTML/CSS/JavaScript (ingen frameworks)
- Firebase Auth + Firestore (projectId: learnai-dk, region: europe-west1)
- Anthropic API: claude-haiku-4-5-20251001 (møde-simulator), claude-sonnet-4-6 (C+ streaming)
- Three.js (DNA helix på platform.html)
- GitHub Pages hosting

<span class="md-h2">## Kursusstruktur</span>
- Niveau D: Gratis, 50 coins ved bestå, Bronze badge
- Niveau C: 799 DKK, 100 coins, Sølv badge
- Niveau B: 1.499 DKK, 200 coins, Guld badge  
- Niveau A: 4.599 DKK, 500 coins, Diamant badge
- Sidekurser: købes med coins

<span class="md-h2">## Design system</span>
- Fonts: Outfit + Lora (Google Fonts)
- Farver: C1=indigo #4F46E5, C2=teal #0D9488, C3=violet #7C3AED, C+=rose #E11D48
- Dark theme, premium/cinematic æstetik
- Aggressive animationer foretrukket

<span class="md-h2">## Vigtige regler</span>
- Byg ALTID korrekt, ikke hurtigt — spørg hvis noget er uklart
- Anti-gæt i quizzes: svar altid jævnt fordelt og shufflede
- Toast-notifikationer: sort pill centreret på skærmen
- Locked-toast: sort pill centreret på skærmen
- Journey-bar altid centreret

<span class="md-h2">## Nuværende filer</span>
- platform.html: Forside + auth + kursus-oversigt
- eksamen-d.html + eksamen-d-del2.html: D-eksamen (2 dele)
- kursus-c1 til c3: C-kursus moduler
- bibliotek.html: Prompt-bibliotek (localStorage key: learnai_prompt_library_v2)
- kursus-cplus.html + intro-cplus.html: C+ kursus</div>
    </div>

    <div class="info-box info-tip" style="margin-top: 20px;">
      <span class="icon">💡</span>
      <div><strong>Hold den opdateret!</strong> Hver gang du bygger noget nyt, tilføj det til CLAUDE.md. Det tager 30 sekunder og sparer dig 10 minutter forklaring næste gang.</div>
    </div>
  </section>

  <div class="divider"></div>

  <!-- DEL 5 -->
  <section class="section reveal" id="del5">
    <div class="section-label">05 — Kunsten at prompte</div>
    <h2 class="section-title">Prompts der faktisk virker</h2>
    <p class="section-intro">Claude Code er som chatten — jo bedre du prompter, jo bedre output. Her er dine templates til akademiet-ai.dk.</p>

    <div class="cards" style="grid-template-columns: 1fr; gap: 20px;">

      <div class="card reveal" style="border-left: 3px solid var(--accent);">
        <div class="card-icon">🏗️</div>
        <h4>Ny HTML-fil fra bunden</h4>
        <p style="margin-bottom: 12px;">Brug når du vil bygge en helt ny side.</p>
        <div class="prompt-card">
          <div class="label">📋 Prompt-skabelon</div>
          Byg en ny fil kaldet [filnavn].html til akademiet-ai.dk. Siden skal:
          <br>— [Beskriv hvad siden gør]
          <br>— Bruge vores standard dark theme med [farve] som accentfarve
          <br>— Inkludere Firebase Auth-check i toppen (redirect til platform.html hvis ikke logget ind)
          <br>— Animationsstil: cinematic, premium — se på kursus-c1.html som reference
          <br>— [Evt. specifikt funktionalitet, f.eks. quiz/eksamen/modul-lås]
        </div>
      </div>

      <div class="card reveal" style="border-left: 3px solid var(--green);">
        <div class="card-icon">🔧</div>
        <h4>Ret en fejl i eksisterende fil</h4>
        <p style="margin-bottom: 12px;">Brug når noget ikke virker som det skal.</p>
        <div class="prompt-card">
          <div class="label">📋 Prompt-skabelon</div>
          I filen [filnavn].html virker [beskriv fejlen præcist].
          <br>Forventet opførsel: [hvad skal der ske]
          <br>Faktisk opførsel: [hvad sker der i stedet]
          <br>Ret kun dette — touch ikke andre dele af filen.
        </div>
      </div>

      <div class="card reveal" style="border-left: 3px solid var(--amber);">
        <div class="card-icon">⚡</div>
        <h4>Tilføj feature til eksisterende side</h4>
        <p style="margin-bottom: 12px;">Brug når du vil udvide en side med ny funktionalitet.</p>
        <div class="prompt-card">
          <div class="label">📋 Prompt-skabelon</div>
          I [filnavn].html skal du tilføje [feature].
          <br>Den skal placeres [præcis placering, f.eks. "efter modul 3-knappen"].
          <br>Den skal matche sidens eksisterende stil og animationer.
          <br>Brug [specifikke teknologier hvis relevant, f.eks. Firebase/Firestore].
        </div>
      </div>

      <div class="card reveal" style="border-left: 3px solid var(--red);">
        <div class="card-icon">🔄</div>
        <h4>Konsistens på tværs af filer</h4>
        <p style="margin-bottom: 12px;">En af Claude Codes superkræfter — noget chatten ikke kan.</p>
        <div class="prompt-card">
          <div class="label">📋 Prompt-skabelon</div>
          Tjek alle kursus-*.html filer og sørg for at [regel/design/funktionalitet] er ens på tværs af dem alle. 
          <br>Reference-implementationen er i [filnavn].html.
          <br>Lav kun ændringer der er nødvendige for konsistens.
        </div>
      </div>

    </div>

    <div class="info-box info-warn" style="margin-top: 32px;">
      <span class="icon">⚠️</span>
      <div><strong>Undgå vage prompts som:</strong> "Gør siden bedre" eller "Fix fejlene". Vær altid specifik. Hvad præcist skal ændres? Hvad er det forventede resultat?</div>
    </div>
  </section>

  <div class="divider"></div>

  <!-- DEL 6 -->
  <section class="section reveal" id="del6">
    <div class="section-label">06 — Workflow</div>
    <h2 class="section-title">Arbejdsflow med GitHub</h2>
    <p class="section-intro">Sådan ser et professionelt workflow ud fra idé til live på GitHub Pages.</p>

    <div class="steps">

      <div class="step reveal">
        <div class="step-num">1</div>
        <div class="step-content">
          <h3>Planlæg i chatten (her!)</h3>
          <p>Brug Claude.ai chat til at afklare scope, design og krav. F.eks.: "Hvad skal eksamen-c.html indeholde?" Få et klart billede af hvad der skal bygges, FØR du åbner Claude Code.</p>
        </div>
      </div>

      <div class="step reveal">
        <div class="step-num">2</div>
        <div class="step-content">
          <h3>Commit eksisterende arbejde FØRST</h3>
          <p>Før Claude Code laver ændringer, sørg for at have en ren Git-tilstand:</p>
          <div class="code-block">
            <button class="copy-btn" onclick="copyCode(this)">Kopiér</button>
            <span class="cmd">git add .</span>
            <br><span class="cmd">git commit -m "Checkpoint: før Claude Code session"</span>
          </div>
          <p>Så kan du altid gå tilbage hvis noget går galt.</p>
        </div>
      </div>

      <div class="step reveal">
        <div class="step-num">3</div>
        <div class="step-content">
          <h3>Byg med Claude Code</h3>
          <p>Start Claude Code i din mappe og giv din prompt. Claude viser dig hvad den vil ændre <em>før</em> den gør det — du godkender eller afviser.</p>
          <div class="code-block">
            <button class="copy-btn" onclick="copyCode(this)">Kopiér</button>
            <span class="cmd">claude</span>
            <br><span class="comment"># Skriv din prompt og tryk Enter</span>
          </div>
        </div>
      </div>

      <div class="step reveal">
        <div class="step-num">4</div>
        <div class="step-content">
          <h3>Review ændringerne</h3>
          <p>Brug <strong>/diff</strong> i Claude Code for at se præcist hvad der er ændret. I VS Code-udvidelsen kan du se det visuelt med grøn/rød highlighting.</p>
          <div class="code-block">
            <span class="cmd">/diff</span>
            <br><span class="comment"># Viser alle ændringer siden sidste commit</span>
          </div>
        </div>
      </div>

      <div class="step reveal">
        <div class="step-num">5</div>
        <div class="step-content">
          <h3>Test i browseren</h3>
          <p>Åbn filen direkte i din browser (højreklik → "Open with Live Server" i VS Code) og tjek at alt ser rigtigt ud.</p>
        </div>
      </div>

      <div class="step reveal">
        <div class="step-num">6</div>
        <div class="step-content">
          <h3>Push til GitHub Pages</h3>
          <div class="code-block">
            <button class="copy-btn" onclick="copyCode(this)">Kopiér</button>
            <span class="cmd">git add .</span>
            <br><span class="cmd">git commit -m "feat: tilføj eksamen-c.html"</span>
            <br><span class="cmd">git push</span>
            <br><span class="comment"># Live på magnuscode-ai.github.io/ai-kursus inden for 1-2 min</span>
          </div>
        </div>
      </div>

    </div>
  </section>

  <div class="divider"></div>

  <!-- DEL 7 -->
  <section class="section reveal" id="del7">
    <div class="section-label">07 — Genveje og tricks</div>
    <h2 class="section-title">Pro-tricks du skal kende</h2>
    <p class="section-intro">Disse kommandoer og vaner gør dig 3x hurtigere.</p>

    <div class="cards">

      <div class="card reveal">
        <div class="card-icon">🔀</div>
        <h4>/clear</h4>
        <p>Ryd konteksten når du skifter til en ny opgave. Holder sessionen hurtig og fokuseret.</p>
        <div class="code-block" style="margin-top: 10px; font-size: 12px;">
          <span class="cmd">/clear</span>
        </div>
      </div>

      <div class="card reveal">
        <div class="card-icon">⏪</div>
        <h4>/rewind</h4>
        <p>Fortryd Claude Codes seneste ændringer og gå tilbage til forrige tilstand. Din sikkerhedsnet.</p>
        <div class="code-block" style="margin-top: 10px; font-size: 12px;">
          <span class="cmd">/rewind</span>
        </div>
      </div>

      <div class="card reveal">
        <div class="card-icon">📋</div>
        <h4>/diff</h4>
        <p>Se præcist hvad der er ændret i denne session. Altid et godt tjek inden du committer.</p>
        <div class="code-block" style="margin-top: 10px; font-size: 12px;">
          <span class="cmd">/diff</span>
        </div>
      </div>

      <div class="card reveal">
        <div class="card-icon">🎯</div>
        <h4>@ for specifikke filer</h4>
        <p>Fortæl Claude præcist hvilken fil du taler om ved at bruge @-syntaksen.</p>
        <div class="code-block" style="margin-top: 10px; font-size: 12px;">
          <span class="cmd">Ret @eksamen-d.html så...</span>
        </div>
      </div>

      <div class="card reveal">
        <div class="card-icon">🛑</div>
        <h4>Escape / Ctrl+C</h4>
        <p>Stop Claude midt i en handling hvis den er ved at gøre noget forkert. Claude stopper øjeblikkeligt.</p>
      </div>

      <div class="card reveal">
        <div class="card-icon">💾</div>
        <h4>Checkpoints</h4>
        <p>Commit til Git jævnligt under arbejdet. Det er dine "save points" — du kan altid vende tilbage.</p>
        <div class="code-block" style="margin-top: 10px; font-size: 12px;">
          <span class="cmd">git commit -m "wip: eksamen-c step 1"</span>
        </div>
      </div>

    </div>

    <div class="section-label" style="margin-top: 56px;">✅ Din tjekliste inden du starter</div>
    <ul class="checklist">
      <li>Node.js 18+ er installeret (tjek med node --version)</li>
      <li>Claude Code er installeret (tjek med claude --version)</li>
      <li>Du er logget ind (kør claude i din terminal)</li>
      <li>CLAUDE.md eksisterer i roden af dit projekt</li>
      <li>Du har commitet dit nuværende arbejde til Git</li>
      <li>Du er i den rigtige mappe (ls viser dine projektfiler)</li>
      <li>VS Code er åben med projektet</li>
    </ul>

  </section>

</div>

<!-- FOOTER -->
<footer class="footer">
  <p style="font-family: 'Syne', sans-serif; font-size: 18px; font-weight: 700; margin-bottom: 8px;">akademiet-ai.dk</p>
  <p>Claude Code Guide — Opdateret 2025 · Bygget til magnuscode-ai/ai-kursus projektet</p>
</footer>

<script>
  // Progress bar
  window.addEventListener('scroll', () => {
    const total = document.body.scrollHeight - window.innerHeight;
    const pct = (window.scrollY / total) * 100;
    document.getElementById('progressBar').style.width = pct + '%';
  });

  // Scroll reveal
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) { e.target.classList.add('visible'); }
    });
  }, { threshold: 0.1 });

  document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

  // Copy buttons
  function copyCode(btn) {
    const block = btn.closest('.code-block');
    const text = Array.from(block.childNodes)
      .filter(n => n.nodeType === 3 || (n.nodeType === 1 && n.tagName !== 'BUTTON'))
      .map(n => n.textContent)
      .join('')
      .trim();
    navigator.clipboard.writeText(text).then(() => {
      btn.textContent = '✓ Kopieret';
      setTimeout(() => btn.textContent = 'Kopiér', 2000);
    });
  }
</script>

</body>
</html>
