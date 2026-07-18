[content-intelligence-studio.html](https://github.com/user-attachments/files/30144500/content-intelligence-studio.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Content Intelligence Studio</title>
<style>
  :root{
    --ink:#0d1420;
    --ink-2:#141d2e;
    --ink-3:#1b2740;
    --paper:#f6f4ee;
    --paper-dim:#e8e4d8;
    --line: rgba(246,244,238,0.10);
    --line-soft: rgba(246,244,238,0.06);
    --accent:#d9a441;
    --accent-soft: rgba(217,164,65,0.16);
    --blue:#5b83c4;
    --blue-soft: rgba(91,131,196,0.16);
    --good:#5fae7f;
    --good-soft: rgba(95,174,127,0.14);
    --bad:#c1665a;
    --bad-soft: rgba(193,102,90,0.14);
    --text-hi: #f6f4ee;
    --text-mid: rgba(246,244,238,0.72);
    --text-low: rgba(246,244,238,0.46);
    --display: Iowan Old Style, "Palatino Linotype", Palatino, Georgia, serif;
    --body: -apple-system, BlinkMacSystemFont, "Segoe UI", Inter, Roboto, Helvetica, Arial, sans-serif;
    --mono: "SF Mono", SFMono-Regular, Consolas, "Liberation Mono", Menlo, monospace;
    --radius: 14px;
    color-scheme: dark;
  }
  html.light{
    --ink:#f6f4ee;
    --ink-2:#ffffff;
    --ink-3:#efece2;
    --line: rgba(13,20,32,0.10);
    --line-soft: rgba(13,20,32,0.06);
    --text-hi:#141a24;
    --text-mid: rgba(20,26,36,0.72);
    --text-low: rgba(20,26,36,0.46);
    color-scheme: light;
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{
    background:var(--ink);
    color:var(--text-hi);
    font-family:var(--body);
    min-height:100vh;
    transition:background .35s ease,color .35s ease;
    -webkit-font-smoothing:antialiased;
  }
  @media (prefers-reduced-motion: reduce){
    *{animation-duration:0.001ms !important; transition-duration:0.001ms !important;}
  }
  a{color:inherit;}
  ::selection{background:var(--accent-soft);}

  .topbar{
    position:sticky; top:0; z-index:50;
    display:flex; align-items:center; justify-content:space-between;
    padding:16px 28px;
    background:linear-gradient(to bottom, var(--ink) 70%, transparent);
    backdrop-filter:blur(6px);
    border-bottom:1px solid var(--line-soft);
  }
  .brand{display:flex; align-items:center; gap:10px;}
  .brand-mark{
    width:30px;height:30px;border-radius:8px;
    background:conic-gradient(from 220deg, var(--accent), var(--blue), var(--accent));
    display:flex;align-items:center;justify-content:center;
    font-family:var(--display); font-weight:600; font-size:15px; color:#0d1420;
  }
  .brand-name{font-family:var(--display); font-size:18px; letter-spacing:0.2px;}
  .brand-sub{font-size:11px; color:var(--text-low); letter-spacing:0.08em; text-transform:uppercase; margin-top:-2px;}
  .topbar-actions{display:flex; align-items:center; gap:10px;}
  .icon-btn{
    width:36px;height:36px;border-radius:10px;border:1px solid var(--line);
    background:var(--ink-2); color:var(--text-mid); cursor:pointer;
    display:flex;align-items:center;justify-content:center; font-size:15px;
    transition:all .2s ease;
  }
  .icon-btn:hover{border-color:var(--accent); color:var(--accent);}

  .wrap{max-width:1180px; margin:0 auto; padding:0 28px 80px;}

  .hero{ padding:64px 0 28px; }
  .eyebrow{
    font-family:var(--mono); font-size:11px; letter-spacing:0.14em; text-transform:uppercase;
    color:var(--accent); margin-bottom:14px; display:flex; align-items:center; gap:8px;
  }
  .eyebrow::before{content:""; width:16px; height:1px; background:var(--accent);}
  h1.headline{
    font-family:var(--display); font-weight:500; font-size:clamp(32px,4.4vw,52px);
    line-height:1.08; margin:0 0 16px; letter-spacing:-0.01em;
  }
  h1.headline em{color:var(--accent); font-style:normal;}
  .lede{font-size:16px; color:var(--text-mid); max-width:600px; line-height:1.6; margin-bottom:8px;}
  .brief-chips{display:flex; flex-wrap:wrap; gap:8px; margin:22px 0 8px;}
  .chip{
    font-family:var(--mono); font-size:11.5px; padding:6px 12px; border-radius:100px;
    border:1px solid var(--line); color:var(--text-mid); background:var(--ink-2);
  }
  .chip b{color:var(--text-hi); font-weight:600;}

  .intake-grid{ display:grid; grid-template-columns:1.1fr 0.9fr; gap:20px; margin-top:32px; }
  @media (max-width:840px){ .intake-grid{grid-template-columns:1fr;} }

  .panel{
    background:var(--ink-2); border:1px solid var(--line); border-radius:var(--radius);
    padding:22px;
  }
  .panel-title{ font-family:var(--display); font-size:16px; margin:0 0 4px; display:flex; align-items:center; gap:8px; }
  .panel-hint{font-size:12.5px; color:var(--text-low); margin:0 0 16px;}

  textarea#postText{
    width:100%; min-height:220px; resize:vertical;
    background:var(--ink-3); border:1px solid var(--line); border-radius:10px;
    color:var(--text-hi); padding:14px; font-family:var(--body); font-size:14.5px; line-height:1.6;
    outline:none; transition:border-color .2s ease;
  }
  textarea#postText:focus{border-color:var(--accent);}
  .char-count{text-align:right; font-family:var(--mono); font-size:11px; color:var(--text-low); margin-top:6px;}

  .dropzone{
    margin-top:14px; border:1.5px dashed var(--line); border-radius:10px;
    padding:22px; text-align:center; cursor:pointer; transition:all .2s ease;
    color:var(--text-mid); font-size:13px;
  }
  .dropzone:hover, .dropzone.drag{border-color:var(--accent); background:var(--accent-soft); color:var(--text-hi);}
  .dropzone .dz-icon{font-size:22px; margin-bottom:6px;}
  #imgInput{display:none;}
  .img-preview-wrap{margin-top:14px; position:relative; display:none;}
  .img-preview-wrap img{width:100%; border-radius:10px; border:1px solid var(--line); display:block;}
  .img-remove{
    position:absolute; top:8px; right:8px; width:28px; height:28px; border-radius:8px;
    background:rgba(13,20,32,0.72); border:1px solid var(--line); color:#fff; cursor:pointer;
  }

  .goal-list{display:flex; flex-direction:column; gap:10px;}
  .goal-item{
    display:flex; gap:10px; align-items:flex-start; padding:10px 12px; border-radius:10px;
    border:1px solid var(--line-soft); font-size:13px; color:var(--text-mid);
  }
  .goal-item .dot{width:6px;height:6px;border-radius:50%; background:var(--accent); margin-top:6px; flex:none;}

  .rigor-row{display:flex; gap:8px; margin-top:6px;}
  .rigor-btn{
    flex:1; padding:10px; border-radius:10px; border:1px solid var(--line); background:var(--ink-3);
    color:var(--text-mid); font-size:12px; cursor:pointer; text-align:center; transition:all .2s ease;
  }
  .rigor-btn.active{border-color:var(--accent); color:var(--accent); background:var(--accent-soft);}

  .run-row{display:flex; align-items:center; gap:14px; margin-top:26px; flex-wrap:wrap;}
  .btn{
    font-family:var(--body); font-weight:600; font-size:14.5px; padding:14px 26px; border-radius:100px;
    border:none; cursor:pointer; transition:all .2s ease; display:inline-flex; align-items:center; gap:8px;
  }
  .btn-primary{background:var(--accent); color:#1a1206;}
  .btn-primary:hover{transform:translateY(-1px); box-shadow:0 8px 24px rgba(217,164,65,0.25);}
  .btn-primary:disabled{opacity:0.5; cursor:not-allowed; transform:none; box-shadow:none;}
  .btn-ghost{background:transparent; border:1px solid var(--line); color:var(--text-mid);}
  .btn-ghost:hover{border-color:var(--accent); color:var(--accent);}
  .run-note{font-size:12px; color:var(--text-low);}

  #dashboard{display:none;}
  .dash-grid{display:grid; grid-template-columns:300px 1fr; gap:20px; align-items:start; margin-top:24px;}
  @media (max-width:960px){ .dash-grid{grid-template-columns:1fr;} }

  .desk{
    background:var(--ink-2); border:1px solid var(--line); border-radius:var(--radius); padding:18px;
    position:sticky; top:80px;
  }
  .desk-title{font-family:var(--mono); font-size:11px; letter-spacing:0.1em; text-transform:uppercase; color:var(--text-low); margin-bottom:14px;}
  .reviewer{
    display:flex; gap:12px; padding:12px 8px; border-radius:10px; margin-bottom:4px; align-items:flex-start;
    transition:background .2s ease;
  }
  .reviewer.active-row{background:var(--accent-soft);}
  .reviewer .r-icon{
    width:32px;height:32px; border-radius:8px; background:var(--ink-3); border:1px solid var(--line);
    display:flex; align-items:center; justify-content:center; font-size:15px; flex:none;
  }
  .reviewer .r-body{flex:1; min-width:0;}
  .reviewer .r-name{font-size:13px; font-weight:600;}
  .reviewer .r-focus{font-size:11.5px; color:var(--text-low); margin-top:1px;}
  .r-status{font-family:var(--mono); font-size:10px; margin-top:4px; letter-spacing:0.05em;}
  .r-status.queued{color:var(--text-low);}
  .r-status.working{color:var(--accent);}
  .r-status.done{color:var(--good);}
  .r-status.failed{color:var(--bad);}
  .spin{display:inline-block; width:8px; height:8px; border-radius:50%; background:var(--accent); margin-right:5px; animation:pulse 1s infinite ease-in-out;}
  @keyframes pulse{0%,100%{opacity:.3;} 50%{opacity:1;}}

  .log-console{
    margin-top:14px; background:var(--ink); border:1px solid var(--line); border-radius:10px;
    padding:12px; max-height:220px; overflow-y:auto; font-family:var(--mono); font-size:11px; color:var(--text-mid);
  }
  .log-line{padding:3px 0; border-bottom:1px solid var(--line-soft); display:flex; gap:8px;}
  .log-line .t{color:var(--text-low); flex:none;}

  .main-col{display:flex; flex-direction:column; gap:20px;}

  .score-hero{
    background:var(--ink-2); border:1px solid var(--line); border-radius:var(--radius); padding:26px;
    display:flex; gap:26px; align-items:center; flex-wrap:wrap;
  }
  .score-ring{width:120px; height:120px; position:relative; flex:none;}
  .score-ring svg{transform:rotate(-90deg); width:100%; height:100%;}
  .score-ring circle{fill:none; stroke-width:8;}
  .score-ring .bg{stroke:var(--line);}
  .score-ring .fg{stroke:var(--accent); stroke-linecap:round; transition:stroke-dashoffset 1.2s cubic-bezier(.4,0,.2,1);}
  .score-ring .num{
    position:absolute; inset:0; display:flex; flex-direction:column; align-items:center; justify-content:center;
    font-family:var(--display); font-size:30px;
  }
  .score-ring .num span{font-family:var(--mono); font-size:10px; color:var(--text-low); text-transform:uppercase; letter-spacing:0.08em;}
  .score-hero-body{flex:1; min-width:220px;}
  .score-hero-body h2{font-family:var(--display); font-size:20px; margin:0 0 6px;}
  .score-hero-body p{font-size:13.5px; color:var(--text-mid); line-height:1.6; margin:0;}

  .cat-grid{display:grid; grid-template-columns:repeat(auto-fit,minmax(200px,1fr)); gap:14px;}
  .cat-card{
    background:var(--ink-2); border:1px solid var(--line); border-radius:12px; padding:16px; cursor:pointer;
    transition:border-color .2s ease, transform .15s ease;
  }
  .cat-card:hover{border-color:var(--accent); transform:translateY(-2px);}
  .cat-card.selected{border-color:var(--accent); background:var(--accent-soft);}
  .cat-top{display:flex; justify-content:space-between; align-items:flex-start;}
  .cat-icon{font-size:16px;}
  .cat-score{font-family:var(--display); font-size:24px;}
  .cat-name{font-size:12.5px; color:var(--text-mid); margin-top:8px;}
  .bar-track{height:4px; background:var(--line); border-radius:2px; margin-top:10px; overflow:hidden;}
  .bar-fill{height:100%; background:var(--accent); border-radius:2px; transition:width 1s ease;}

  .detail-panel{
    background:var(--ink-2); border:1px solid var(--line); border-radius:var(--radius); padding:22px; display:none;
  }
  .detail-panel.show{display:block;}
  .detail-head{display:flex; justify-content:space-between; align-items:center; margin-bottom:14px;}
  .detail-head h3{font-family:var(--display); font-size:17px; margin:0;}
  .close-detail{background:none; border:none; color:var(--text-low); cursor:pointer; font-size:16px;}
  .kv-block{margin-bottom:16px;}
  .kv-label{font-family:var(--mono); font-size:10.5px; text-transform:uppercase; letter-spacing:0.08em; color:var(--accent); margin-bottom:8px;}
  .kv-block ul{margin:0; padding-left:18px; color:var(--text-mid); font-size:13.5px; line-height:1.7;}
  .kv-block p{margin:0; color:var(--text-mid); font-size:13.5px; line-height:1.7;}
  .kv-block.weak .kv-label{color:var(--bad);}
  .kv-block.strong .kv-label{color:var(--good);}

  .tabs{display:flex; gap:6px; flex-wrap:wrap; border-bottom:1px solid var(--line); padding-bottom:0; margin-bottom:20px;}
  .tab{
    padding:10px 16px; font-size:13px; color:var(--text-mid); cursor:pointer; border-bottom:2px solid transparent;
    font-weight:600;
  }
  .tab.active{color:var(--accent); border-bottom-color:var(--accent);}
  .tab-panel{display:none;}
  .tab-panel.active{display:block;}

  .report-block{margin-bottom:22px;}
  .report-block h4{font-family:var(--display); font-size:15px; margin:0 0 8px; color:var(--accent);}
  .report-block p, .report-block li{font-size:14px; color:var(--text-mid); line-height:1.75;}
  .report-block ul{padding-left:18px; margin:0;}

  .rewrite-cols{display:grid; grid-template-columns:1fr 1fr; gap:16px;}
  @media (max-width:700px){ .rewrite-cols{grid-template-columns:1fr;} }
  .rewrite-card{background:var(--ink-3); border:1px solid var(--line); border-radius:10px; padding:16px;}
  .rewrite-card .rw-label{font-family:var(--mono); font-size:10.5px; text-transform:uppercase; letter-spacing:0.08em; margin-bottom:8px;}
  .rewrite-card.before .rw-label{color:var(--bad);}
  .rewrite-card.after .rw-label{color:var(--good);}
  .rewrite-card pre{white-space:pre-wrap; font-family:var(--body); font-size:13.5px; line-height:1.65; margin:0; color:var(--text-hi);}
  .copy-btn{margin-top:10px; font-size:11px; padding:6px 12px; border-radius:8px; border:1px solid var(--line); background:transparent; color:var(--text-mid); cursor:pointer;}
  .copy-btn:hover{border-color:var(--accent); color:var(--accent);}

  .hook-list{display:flex; flex-direction:column; gap:10px;}
  .hook-item{
    display:flex; gap:12px; align-items:center; padding:12px 14px; background:var(--ink-3);
    border:1px solid var(--line); border-radius:10px; font-size:13.5px;
  }
  .hook-item .hnum{font-family:var(--mono); color:var(--accent); flex:none;}

  .checklist{display:flex; flex-direction:column; gap:8px;}
  .check-item{display:flex; gap:10px; align-items:flex-start; padding:10px 12px; border-radius:10px; background:var(--ink-3); border:1px solid var(--line);}
  .check-item input{margin-top:3px; accent-color:var(--accent);}
  .check-item label{font-size:13.5px; color:var(--text-mid); line-height:1.5;}

  .perf-estimate{
    background:linear-gradient(135deg, var(--blue-soft), var(--accent-soft));
    border:1px solid var(--line); border-radius:12px; padding:16px 18px; font-size:13px; color:var(--text-mid);
    display:flex; gap:10px; align-items:flex-start; margin-top:6px;
  }
  .perf-estimate b{color:var(--text-hi);}

  .followup-row{display:flex; flex-wrap:wrap; gap:8px; margin-top:6px;}
  .followup-chip{
    font-size:12.5px; padding:8px 14px; border-radius:100px; border:1px solid var(--line);
    background:var(--ink-3); color:var(--text-mid); cursor:pointer; transition:all .2s ease;
  }
  .followup-chip:hover{border-color:var(--accent); color:var(--accent);}

  .error-banner{
    background:var(--bad-soft); border:1px solid var(--bad); color:var(--text-hi); border-radius:10px;
    padding:14px 16px; font-size:13px; display:flex; justify-content:space-between; align-items:center; gap:12px; margin-top:14px;
  }
  .error-banner button{background:var(--bad); border:none; color:#fff; padding:8px 14px; border-radius:8px; cursor:pointer; font-size:12px; flex:none;}

  .fade-in{animation:fadeIn .5s ease both;}
  @keyframes fadeIn{from{opacity:0; transform:translateY(6px);} to{opacity:1; transform:translateY(0);}}

  .footer-note{text-align:center; color:var(--text-low); font-size:11.5px; margin-top:50px; font-family:var(--mono);}
</style>
</head>
<body>

<div class="topbar">
  <div class="brand">
    <div class="brand-mark">C</div>
    <div>
      <div class="brand-name">Content Intelligence Studio</div>
      <div class="brand-sub">AI editorial desk</div>
    </div>
  </div>
  <div class="topbar-actions">
    <button class="icon-btn" id="themeToggle" title="Toggle theme">◐</button>
  </div>
</div>

<div class="wrap">

  <div id="intake">
    <div class="hero">
      <div class="eyebrow">Pre-publish review</div>
      <h1 class="headline">Send your post through the <em>editorial desk</em><br>before it goes to LinkedIn.</h1>
      <p class="lede">A panel of specialist AI reviewers reads your caption and image the way a sharp editor, a growth strategist, and your most honest colleague would — then hands back a scored, actionable report.</p>
      <div class="brief-chips">
        <div class="chip">Format: <b>Social post</b></div>
        <div class="chip">Platform: <b>LinkedIn</b></div>
        <div class="chip">Goal: <b>Personal brand growth</b></div>
        <div class="chip">Inputs: <b>Text + image</b></div>
      </div>
    </div>

    <div class="intake-grid">
      <div class="panel">
        <p class="panel-title">✏️ Your post</p>
        <p class="panel-hint">Paste the caption exactly as you plan to publish it.</p>
        <textarea id="postText" placeholder="Paste your LinkedIn post text here..."></textarea>
        <div class="char-count"><span id="charCount">0</span> characters</div>

        <div class="dropzone" id="dropzone">
          <div class="dz-icon">🖼️</div>
          <div>Drop an image here, or <b>click to upload</b></div>
          <div style="font-size:11px;color:var(--text-low);margin-top:4px;">Thumbnail, screenshot, or supporting graphic</div>
        </div>
        <input type="file" id="imgInput" accept="image/*">
        <div class="img-preview-wrap" id="imgPreviewWrap">
          <img id="imgPreview" src="" alt="Upload preview">
          <button class="img-remove" id="imgRemove">✕</button>
        </div>
      </div>

      <div class="panel">
        <p class="panel-title">🎯 Review setup</p>
        <p class="panel-hint">Confirmed from your intake answers — adjust rigor if needed.</p>
        <div class="goal-list">
          <div class="goal-item"><div class="dot"></div>Optimized for personal-brand growth: authority, memorability, and follow-worthiness — not just reach.</div>
          <div class="goal-item"><div class="dot"></div>Reviewed against LinkedIn's feed behavior: hook strength, dwell time, comment-bait, native format.</div>
          <div class="goal-item"><div class="dot"></div>Image analyzed directly by Claude's vision when attached.</div>
        </div>
        <p class="panel-title" style="margin-top:18px;font-size:13px;">Review rigor</p>
        <div class="rigor-row">
          <div class="rigor-btn" data-rigor="gentle">Gentle</div>
          <div class="rigor-btn active" data-rigor="balanced">Balanced</div>
          <div class="rigor-btn" data-rigor="brutal">Brutal</div>
        </div>
      </div>
    </div>

    <div class="run-row">
      <button class="btn btn-primary" id="runBtn">▶ Run editorial review</button>
      <span class="run-note" id="runNote">Add post text (image optional) to begin.</span>
    </div>
  </div>

  <div id="dashboard">
    <div class="hero" style="padding:36px 0 8px;">
      <div class="eyebrow">Live review</div>
      <h1 class="headline" style="font-size:clamp(26px,3.4vw,36px);">The desk is <em id="stateWord">reviewing</em> your post.</h1>
      <button class="btn btn-ghost" id="backBtn" style="margin-top:4px;">← Start a new review</button>
    </div>

    <div id="errorArea"></div>

    <div class="dash-grid">
      <div class="desk">
        <div class="desk-title">Reviewer panel</div>
        <div id="reviewerList"></div>
        <div class="log-console" id="logConsole"></div>
      </div>

      <div class="main-col">
        <div class="score-hero" id="scoreHero" style="display:none;">
          <div class="score-ring">
            <svg viewBox="0 0 120 120">
              <circle class="bg" cx="60" cy="60" r="52"></circle>
              <circle class="fg" id="scoreRingFg" cx="60" cy="60" r="52" stroke-dasharray="326.7" stroke-dashoffset="326.7"></circle>
            </svg>
            <div class="num"><span>Overall</span><div id="scoreNum">–</div></div>
          </div>
          <div class="score-hero-body">
            <h2 id="scoreHeadline">Compiling verdict…</h2>
            <p id="scoreSummary">Reviewers are still reading your post.</p>
          </div>
        </div>

        <div class="cat-grid" id="catGrid"></div>

        <div class="detail-panel" id="detailPanel">
          <div class="detail-head">
            <h3 id="detailTitle">Reviewer notes</h3>
            <button class="close-detail" id="closeDetail">✕ close</button>
          </div>
          <div id="detailBody"></div>
        </div>

        <div class="panel" id="reportPanel" style="display:none;">
          <div class="tabs" id="tabBar">
            <div class="tab active" data-tab="summary">Executive summary</div>
            <div class="tab" data-tab="rewrite">Rewrite</div>
            <div class="tab" data-tab="hooks">Hooks &amp; titles</div>
            <div class="tab" data-tab="checklist">Checklist</div>
            <div class="tab" data-tab="next">Go deeper</div>
          </div>

          <div class="tab-panel active" id="tab-summary">
            <div class="report-block"><h4>Executive summary</h4><p id="repExecSummary"></p></div>
            <div class="report-block"><h4>Content health report</h4><p id="repHealth"></p></div>
            <div class="report-block"><h4>Highest-impact improvements</h4><ul id="repImprovements"></ul></div>
            <div class="report-block">
              <h4>Predicted performance potential</h4>
              <div class="perf-estimate">⚡ <span><b>AI estimate, not a guarantee:</b> <span id="repPerf"></span></span></div>
            </div>
          </div>

          <div class="tab-panel" id="tab-rewrite">
            <div class="rewrite-cols">
              <div class="rewrite-card before">
                <div class="rw-label">Before — your draft</div>
                <pre id="rwBefore"></pre>
              </div>
              <div class="rewrite-card after">
                <div class="rw-label">After — desk rewrite</div>
                <pre id="rwAfter"></pre>
                <button class="copy-btn" id="copyRewrite">Copy rewrite</button>
              </div>
            </div>
          </div>

          <div class="tab-panel" id="tab-hooks">
            <div class="report-block"><h4>Alternative hooks (opening lines)</h4><div class="hook-list" id="hookList"></div></div>
            <div class="report-block"><h4>Alternative titles / lead-ins</h4><div class="hook-list" id="titleList"></div></div>
          </div>

          <div class="tab-panel" id="tab-checklist">
            <div class="report-block"><h4>Publishing checklist</h4><div class="checklist" id="checklistBody"></div></div>
          </div>

          <div class="tab-panel" id="tab-next">
            <div class="report-block"><h4>Go deeper</h4><p style="margin-bottom:10px;">Send one of these to refine the review further:</p>
              <div class="followup-row" id="followupRow"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="footer-note">CONTENT INTELLIGENCE STUDIO — every score and note above is generated live by Claude, not scripted logic.</div>
</div>

<script>
(function(){
  "use strict";

  var themeToggle = document.getElementById('themeToggle');
  themeToggle.addEventListener('click', function(){
    document.documentElement.classList.toggle('light');
    themeToggle.textContent = document.documentElement.classList.contains('light') ? '◑' : '◐';
  });

  var state = {
    postText: '',
    imageBase64: null,
    imageMediaType: null,
    rigor: 'balanced',
    reviewers: [],
    results: {},
    finalReport: null
  };

  var RIGOR_TEXT = {
    gentle: "Be encouraging and light-touch. Lead with what's working, and phrase critique gently and constructively, but never invent praise that isn't earned.",
    balanced: "Be honest and constructive. Give full credit where it's due and name real weaknesses plainly, without being harsh for its own sake.",
    brutal: "Be brutally honest. Do not soften weaknesses. Call out mediocrity, cliches, and weak craft directly, while still being fair and specific."
  };

  var postTextEl = document.getElementById('postText');
  var charCount = document.getElementById('charCount');
  postTextEl.addEventListener('input', function(){
    state.postText = postTextEl.value;
    charCount.textContent = state.postText.length;
    updateRunNote();
  });

  var rigorBtns = document.querySelectorAll('.rigor-btn');
  rigorBtns.forEach(function(btn){
    btn.addEventListener('click', function(){
      rigorBtns.forEach(function(b){ b.classList.remove('active'); });
      btn.classList.add('active');
      state.rigor = btn.dataset.rigor;
    });
  });

  var dropzone = document.getElementById('dropzone');
  var imgInput = document.getElementById('imgInput');
  var imgPreviewWrap = document.getElementById('imgPreviewWrap');
  var imgPreview = document.getElementById('imgPreview');
  var imgRemove = document.getElementById('imgRemove');

  dropzone.addEventListener('click', function(){ imgInput.click(); });
  dropzone.addEventListener('dragover', function(e){ e.preventDefault(); dropzone.classList.add('drag'); });
  dropzone.addEventListener('dragleave', function(){ dropzone.classList.remove('drag'); });
  dropzone.addEventListener('drop', function(e){
    e.preventDefault(); dropzone.classList.remove('drag');
    if(e.dataTransfer.files && e.dataTransfer.files[0]) handleImage(e.dataTransfer.files[0]);
  });
  imgInput.addEventListener('change', function(){
    if(imgInput.files && imgInput.files[0]) handleImage(imgInput.files[0]);
  });
  imgRemove.addEventListener('click', function(e){
    e.stopPropagation();
    state.imageBase64 = null; state.imageMediaType = null;
    imgPreviewWrap.style.display = 'none';
    imgInput.value = '';
  });

  function handleImage(file){
    if(!file.type.indexOf('image/') === 0) return;
    if(file.type.indexOf('image/') !== 0) return;
    var reader = new FileReader();
    reader.onload = function(e){
      var dataUrl = e.target.result;
      var commaIdx = dataUrl.indexOf(',');
      state.imageMediaType = file.type;
      state.imageBase64 = dataUrl.slice(commaIdx+1);
      imgPreview.src = dataUrl;
      imgPreviewWrap.style.display = 'block';
    };
    reader.readAsDataURL(file);
  }

  var runNote = document.getElementById('runNote');
  var runBtn = document.getElementById('runBtn');
  function updateRunNote(){
    if(state.postText.trim().length < 10){
      runNote.textContent = 'Add post text (image optional) to begin.';
    } else {
      runNote.textContent = 'Ready — the desk will assemble specialist reviewers automatically.';
    }
  }

  async function callClaude(systemPrompt, userContent, maxTokens, attempt){
    attempt = attempt || 1;
    var body = {
      model: "claude-sonnet-4-6",
      max_tokens: maxTokens || 1400,
      system: systemPrompt,
      messages: [{ role: "user", content: userContent }]
    };
    try{
      var res = await fetch("https://api.anthropic.com/v1/messages", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(body)
      });
      if(!res.ok){
        throw new Error("API responded with status " + res.status);
      }
      var data = await res.json();
      var textBlocks = (data.content || []).filter(function(b){ return b.type==='text'; }).map(function(b){ return b.text; });
      var text = textBlocks.join("\n").trim();
      if(!text) throw new Error("Empty response from model");
      return text;
    }catch(err){
      if(attempt < 3){
        await new Promise(function(r){ setTimeout(r, 700*attempt); });
        return callClaude(systemPrompt, userContent, maxTokens, attempt+1);
      }
      throw err;
    }
  }

  function buildUserContent(promptText){
    var content = [];
    if(state.imageBase64){
      content.push({ type:"image", source:{ type:"base64", media_type: state.imageMediaType, data: state.imageBase64 } });
    }
    content.push({ type:"text", text: promptText });
    return content;
  }

  function parseFields(raw){
    var out = { score:null, strengths:[], weaknesses:[], opportunities:[], reasoning:'', recommendation:'' };
    var lines = raw.split(/\r?\n/);
    var cur = null;
    lines.forEach(function(line){
      var l = line.trim();
      var m = l.match(/^SCORE:\s*(\d{1,3})/i);
      if(m){ out.score = Math.max(0, Math.min(100, parseInt(m[1],10))); cur=null; return; }
      if(/^STRENGTHS:/i.test(l)){ cur='strengths'; return; }
      if(/^WEAKNESSES:/i.test(l)){ cur='weaknesses'; return; }
      if(/^OPPORTUNITIES:/i.test(l)){ cur='opportunities'; return; }
      if(/^REASONING:/i.test(l)){ cur='reasoning'; out.reasoning += l.replace(/^REASONING:/i,'').trim(); return; }
      if(/^RECOMMENDATION:/i.test(l)){ cur='recommendation'; out.recommendation += l.replace(/^RECOMMENDATION:/i,'').trim(); return; }
      if(!l) return;
      if(cur==='strengths' || cur==='weaknesses' || cur==='opportunities'){
        var item = l.replace(/^[-•*]\s*/, '');
        if(item) out[cur].push(item);
      } else if(cur==='reasoning'){
        out.reasoning += (out.reasoning?' ':'') + l;
      } else if(cur==='recommendation'){
        out.recommendation += (out.recommendation?' ':'') + l;
      }
    });
    if(out.score===null) out.score = 65;
    return out;
  }

  function parseListSection(raw, label){
    var re = new RegExp(label+':\\s*([\\s\\S]*?)(?=\\n[A-Z_]+:|$)', 'i');
    var m = raw.match(re);
    if(!m) return [];
    return m[1].split(/\r?\n/).map(function(s){ return s.replace(/^[-•*]\s*/,'').trim(); }).filter(Boolean);
  }
  function parseTextSection(raw, label){
    var re = new RegExp(label+':\\s*([\\s\\S]*?)(?=\\n[A-Z_]+:|$)', 'i');
    var m = raw.match(re);
    return m ? m[1].trim() : '';
  }

  var logConsole = document.getElementById('logConsole');
  function log(msg){
    var div = document.createElement('div');
    div.className = 'log-line';
    var t = new Date().toLocaleTimeString([], {hour:'2-digit',minute:'2-digit',second:'2-digit'});
    div.innerHTML = '<span class="t">'+t+'</span><span>'+escapeHtml(msg)+'</span>';
    logConsole.appendChild(div);
    logConsole.scrollTop = logConsole.scrollHeight;
  }
  function escapeHtml(s){
    return String(s).replace(/[&<>"']/g, function(c){
      return ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'})[c];
    });
  }

  var DEFAULT_REVIEWERS = [
    { key:'hook', icon:'🪝', name:'Hook & Scroll-Stop Editor', focus:'First two lines and scroll-stopping power' },
    { key:'value', icon:'💡', name:'Value & Narrative Editor', focus:'Substance, storytelling, and payoff' },
    { key:'visual', icon:'🖼️', name:'Visual Reviewer', focus:'How the image reads and supports the post', requiresImage:true },
    { key:'format', icon:'📐', name:'LinkedIn Format Strategist', focus:'Native formatting, line breaks, feed behavior' },
    { key:'voice', icon:'🎙️', name:'Personal Brand Voice Coach', focus:'Authenticity, authority, and memorability' },
    { key:'cta', icon:'📣', name:'Engagement & CTA Reviewer', focus:'Comment-bait, replyability, and close' }
  ];

  async function orchestrateReviewers(){
    var hasImage = !!state.imageBase64;
    var sys = "You are the managing editor at an elite content strategy studio. Given a brief about a piece of content, you design a short multi-stage review workflow of specialist AI reviewers tailored to that exact content. Respond ONLY in plain text lines, one reviewer per line, in this exact format and nothing else:\nREVIEWER: <short role name> | <single emoji> | <one-sentence focus of what they judge>\nProduce between 4 and 6 reviewers. Do not use JSON, markdown, numbering, or any other text.";
    var userPrompt = "Content type: LinkedIn post (text"+(hasImage?" + image":"")+").\nPrimary goal: personal brand growth (followers, authority, memorability).\nReview rigor: "+state.rigor+".\nDesign the specialist reviewer panel for this exact post."+(hasImage?" Include one reviewer specifically for the attached image.":"");
    try{
      log('Orchestrator: designing review workflow…');
      var raw = await callClaude(sys, [{type:'text', text:userPrompt}], 500);
      var lines = raw.split(/\r?\n/).filter(function(l){ return /^REVIEWER:/i.test(l.trim()); });
      var reviewers = lines.map(function(l,i){
        var b = l.replace(/^REVIEWER:\s*/i,'');
        var parts = b.split('|').map(function(s){ return s.trim(); });
        return { key:'r'+i, name: parts[0]||('Reviewer '+(i+1)), icon: parts[1]||'🔎', focus: parts[2]||'General quality review' };
      }).filter(function(r){ return r.name; });
      if(reviewers.length >= 3){
        log('Orchestrator: assembled '+reviewers.length+' specialist reviewers.');
        return reviewers;
      }
      throw new Error('Insufficient reviewers parsed');
    }catch(err){
      log('Orchestrator fallback: using standard LinkedIn panel.');
      return DEFAULT_REVIEWERS.filter(function(r){ return !r.requiresImage || hasImage; })
        .map(function(r){ return {key:r.key,name:r.name,icon:r.icon,focus:r.focus}; });
    }
  }

  function reviewerSystemPrompt(reviewer){
    return "You are \""+reviewer.name+"\", a specialist reviewer at an elite editorial studio, reviewing a LinkedIn post whose goal is personal-brand growth. Your sole focus: "+reviewer.focus+". "+RIGOR_TEXT[state.rigor]+" Judge only through your specialist lens; do not try to cover everything. Respond ONLY in this exact plain-text field format, with no JSON, no markdown headers, no extra commentary:\nSCORE: <integer 0-100>\nSTRENGTHS:\n- <point>\n- <point>\nWEAKNESSES:\n- <point>\n- <point>\nOPPORTUNITIES:\n- <point>\nREASONING: <2-3 sentences of specific reasoning tied to this exact post>\nRECOMMENDATION: <one concrete, specific action to take>\nBe concrete — reference actual words, phrases, or visual details from the post, not generic advice.";
  }

  function synthesisSystemPrompt(){
    return "You are the Editor-in-Chief synthesizing a full panel review of a LinkedIn post aimed at personal-brand growth, rigor level: "+state.rigor+". You have the individual specialist reviews. Produce a final consulting report. Respond ONLY in this exact plain-text field format, nothing else, no JSON, no markdown symbols other than the field names shown:\nEXECUTIVE_SUMMARY: <3-4 sentences, direct verdict on the post as a whole>\nHEALTH_REPORT: <2-3 sentences on overall content health — clarity, credibility, native fit for LinkedIn>\nTOP_IMPROVEMENTS:\n- <highest impact fix>\n- <second highest impact fix>\n- <third highest impact fix>\nPREDICTED_PERFORMANCE: <1-2 sentences estimating relative engagement/reach potential, explicitly phrased as an AI estimate, not a promise>\nREWRITE: <a complete rewritten version of the post, ready to publish, in the author's voice, ideally 3-8 short lines with natural LinkedIn line breaks>\nALT_HOOKS:\n- <alternative opening line 1>\n- <alternative opening line 2>\n- <alternative opening line 3>\nALT_TITLES:\n- <alternative first-line/title framing 1>\n- <alternative first-line/title framing 2>\nCHECKLIST:\n- <publishing checklist item>\n- <publishing checklist item>\n- <publishing checklist item>\n- <publishing checklist item>\nDEEPER_PROMPTS:\n- <a follow-up question/prompt the user could ask to refine further>\n- <a follow-up question/prompt the user could ask to refine further>\n- <a follow-up question/prompt the user could ask to refine further>";
  }

  var intakeEl = document.getElementById('intake');
  var dashboardEl = document.getElementById('dashboard');
  var reviewerListEl = document.getElementById('reviewerList');
  var errorArea = document.getElementById('errorArea');
  var stateWord = document.getElementById('stateWord');

  runBtn.addEventListener('click', startReview);
  document.getElementById('backBtn').addEventListener('click', function(){
    dashboardEl.style.display = 'none';
    intakeEl.style.display = 'block';
    window.scrollTo({top:0, behavior:'smooth'});
  });

  async function startReview(){
    if(state.postText.trim().length < 10){
      runNote.textContent = 'Post text is too short to review.';
      return;
    }
    intakeEl.style.display = 'none';
    dashboardEl.style.display = 'block';
    window.scrollTo({top:0, behavior:'smooth'});
    resetDashboard();

    try{
      state.reviewers = await orchestrateReviewers();
      renderReviewerList();

      for(var i=0;i<state.reviewers.length;i++){
        await runReviewer(state.reviewers[i]);
      }

      stateWord.textContent = 'synthesizing';
      log('Editor-in-Chief: synthesizing final report…');
      await runSynthesis();

      stateWord.textContent = 'complete';
      log('Review complete.');
    }catch(err){
      showError('The review hit a snag: '+err.message, startReview);
    }
  }

  function resetDashboard(){
    errorArea.innerHTML='';
    reviewerListEl.innerHTML='';
    logConsole.innerHTML='';
    document.getElementById('scoreHero').style.display='none';
    document.getElementById('catGrid').innerHTML='';
    document.getElementById('detailPanel').classList.remove('show');
    document.getElementById('reportPanel').style.display='none';
    state.results = {};
    state.finalReport = null;
    stateWord.textContent = 'reviewing';
    log('Post received. Assembling specialist panel…');
  }

  function renderReviewerList(){
    reviewerListEl.innerHTML = state.reviewers.map(function(r){
      return '<div class="reviewer" id="row-'+r.key+'">'+
        '<div class="r-icon">'+r.icon+'</div>'+
        '<div class="r-body">'+
          '<div class="r-name">'+escapeHtml(r.name)+'</div>'+
          '<div class="r-focus">'+escapeHtml(r.focus)+'</div>'+
          '<div class="r-status queued" id="status-'+r.key+'">queued</div>'+
        '</div>'+
      '</div>';
    }).join('');
  }

  function setReviewerStatus(key, status){
    var row = document.getElementById('row-'+key);
    var el = document.getElementById('status-'+key);
    if(!el) return;
    el.className = 'r-status '+status;
    if(row) row.classList.toggle('active-row', status==='working');
    if(status==='working') el.innerHTML = '<span class="spin"></span>reviewing…';
    else el.textContent = status;
  }

  async function runReviewer(reviewer){
    setReviewerStatus(reviewer.key, 'working');
    log(reviewer.name+': reading post…');
    try{
      var userText = "POST TEXT:\n\""+state.postText+"\"\n\n"+(state.imageBase64 ? "An image is attached above — analyze it directly as part of your review where relevant to your focus." : "No image was attached to this post.");
      var raw = await callClaude(reviewerSystemPrompt(reviewer), buildUserContent(userText), 700);
      var parsed = parseFields(raw);
      state.results[reviewer.key] = parsed;
      setReviewerStatus(reviewer.key, 'done');
      log(reviewer.name+': done — score '+parsed.score+'/100.');
      renderCategoryCards();
    }catch(err){
      setReviewerStatus(reviewer.key, 'failed');
      log(reviewer.name+': failed ('+err.message+').');
      state.results[reviewer.key] = { score:null, strengths:[], weaknesses:['Review failed to complete.'], opportunities:[], reasoning:'This reviewer could not complete analysis.', recommendation:'Retry the review.' };
    }
  }

  function renderCategoryCards(){
    var grid = document.getElementById('catGrid');
    grid.innerHTML = state.reviewers.map(function(r){
      var res = state.results[r.key];
      var score = res && res.score!==null ? res.score : null;
      return '<div class="cat-card fade-in" data-key="'+r.key+'">'+
        '<div class="cat-top"><div class="cat-icon">'+r.icon+'</div><div class="cat-score">'+(score!==null?score:'…')+'</div></div>'+
        '<div class="cat-name">'+escapeHtml(r.name)+'</div>'+
        '<div class="bar-track"><div class="bar-fill" style="width:'+(score!==null?score:0)+'%;"></div></div>'+
      '</div>';
    }).join('');
    document.querySelectorAll('.cat-card').forEach(function(card){
      card.addEventListener('click', function(){ openDetail(card.dataset.key); });
    });

    var scored = state.reviewers.map(function(r){ return state.results[r.key]; }).filter(function(r){ return r && r.score!==null; });
    if(scored.length){
      var avg = Math.round(scored.reduce(function(a,b){ return a+b.score; },0)/scored.length);
      showScoreHero(avg, scored.length===state.reviewers.length);
    }
  }

  function showScoreHero(avg, complete){
    var hero = document.getElementById('scoreHero');
    hero.style.display = 'flex';
    document.getElementById('scoreNum').textContent = avg;
    var circumference = 326.7;
    var offset = circumference - (avg/100)*circumference;
    document.getElementById('scoreRingFg').style.strokeDashoffset = offset;
    document.getElementById('scoreHeadline').textContent = complete ? verdictHeadline(avg) : 'Reviewing in progress…';
    document.getElementById('scoreSummary').textContent = complete ? 'All specialist reviewers have weighed in — full report below.' : 'Score will settle as remaining reviewers finish.';
  }
  function verdictHeadline(avg){
    if(avg>=85) return 'Strong — close to publish-ready.';
    if(avg>=70) return 'Solid, with clear upside.';
    if(avg>=55) return 'Workable, needs real revision.';
    return 'Needs a rework before publishing.';
  }

  function openDetail(key){
    var reviewer = state.reviewers.find(function(r){ return r.key===key; });
    var res = state.results[key];
    if(!reviewer || !res) return;
    document.querySelectorAll('.cat-card').forEach(function(c){ c.classList.toggle('selected', c.dataset.key===key); });
    document.getElementById('detailTitle').textContent = reviewer.icon+' '+reviewer.name;
    var body = document.getElementById('detailBody');
    body.innerHTML =
      kvBlock('reasoning','Reasoning', res.reasoning ? '<p>'+escapeHtml(res.reasoning)+'</p>' : '<p>—</p>') +
      kvBlock('strong strengths','Strengths', listOrEmpty(res.strengths)) +
      kvBlock('weak weaknesses','Weaknesses', listOrEmpty(res.weaknesses)) +
      kvBlock('opportunities','Missed opportunities', listOrEmpty(res.opportunities)) +
      kvBlock('recommendation','Recommendation', res.recommendation ? '<p>'+escapeHtml(res.recommendation)+'</p>' : '<p>—</p>');
    document.getElementById('detailPanel').classList.add('show');
    document.getElementById('detailPanel').scrollIntoView({behavior:'smooth', block:'nearest'});
  }
  function listOrEmpty(arr){
    if(!arr || !arr.length) return '<p>—</p>';
    return '<ul>'+arr.map(function(i){ return '<li>'+escapeHtml(i)+'</li>'; }).join('')+'</ul>';
  }
  function kvBlock(cls, label, html){
    return '<div class="kv-block '+cls+'"><div class="kv-label">'+label+'</div>'+html+'</div>';
  }
  document.getElementById('closeDetail').addEventListener('click', function(){
    document.getElementById('detailPanel').classList.remove('show');
    document.querySelectorAll('.cat-card').forEach(function(c){ c.classList.remove('selected'); });
  });

  async function runSynthesis(){
    var panelSummary = state.reviewers.map(function(r){
      var res = state.results[r.key] || {};
      return r.name+' (score '+(res.score!==null&&res.score!==undefined?res.score:'n/a')+'): '+
        'Strengths: '+(res.strengths||[]).join('; ')+'. '+
        'Weaknesses: '+(res.weaknesses||[]).join('; ')+'. '+
        'Opportunities: '+(res.opportunities||[]).join('; ')+'. '+
        'Reasoning: '+(res.reasoning||'')+'. Recommendation: '+(res.recommendation||'');
    }).join('\n\n');

    var userText = "ORIGINAL POST:\n\""+state.postText+"\"\n\nSPECIALIST PANEL FINDINGS:\n"+panelSummary+"\n\nSynthesize the final consulting report now.";
    try{
      var raw = await callClaude(synthesisSystemPrompt(), buildUserContent(userText), 1800);
      var report = {
        execSummary: parseTextSection(raw,'EXECUTIVE_SUMMARY'),
        health: parseTextSection(raw,'HEALTH_REPORT'),
        improvements: parseListSection(raw,'TOP_IMPROVEMENTS'),
        perf: parseTextSection(raw,'PREDICTED_PERFORMANCE'),
        rewrite: parseTextSection(raw,'REWRITE'),
        altHooks: parseListSection(raw,'ALT_HOOKS'),
        altTitles: parseListSection(raw,'ALT_TITLES'),
        checklist: parseListSection(raw,'CHECKLIST'),
        deeperPrompts: parseListSection(raw,'DEEPER_PROMPTS')
      };
      state.finalReport = report;
      renderFinalReport(report);
    }catch(err){
      showError('Could not generate the final synthesis report: '+err.message, runSynthesis);
    }
  }

  function renderFinalReport(report){
    document.getElementById('reportPanel').style.display = 'block';
    document.getElementById('repExecSummary').textContent = report.execSummary || '—';
    document.getElementById('repHealth').textContent = report.health || '—';
    document.getElementById('repImprovements').innerHTML = report.improvements.map(function(i){ return '<li>'+escapeHtml(i)+'</li>'; }).join('') || '<li>—</li>';
    document.getElementById('repPerf').textContent = report.perf || '—';

    document.getElementById('rwBefore').textContent = state.postText;
    document.getElementById('rwAfter').textContent = report.rewrite || '—';

    document.getElementById('hookList').innerHTML = report.altHooks.map(function(h,i){
      return '<div class="hook-item"><span class="hnum">0'+(i+1)+'</span><span>'+escapeHtml(h)+'</span></div>';
    }).join('') || '<p>—</p>';
    document.getElementById('titleList').innerHTML = report.altTitles.map(function(h,i){
      return '<div class="hook-item"><span class="hnum">0'+(i+1)+'</span><span>'+escapeHtml(h)+'</span></div>';
    }).join('') || '<p>—</p>';

    document.getElementById('checklistBody').innerHTML = report.checklist.map(function(c,i){
      return '<div class="check-item"><input type="checkbox" id="chk'+i+'"><label for="chk'+i+'">'+escapeHtml(c)+'</label></div>';
    }).join('') || '<p>—</p>';

    document.getElementById('followupRow').innerHTML = report.deeperPrompts.map(function(p){
      return '<div class="followup-chip">'+escapeHtml(p)+'</div>';
    }).join('');

    document.querySelectorAll('.followup-chip').forEach(function(chip, idx){
      chip.addEventListener('click', function(){ runFollowup(report.deeperPrompts[idx]); });
    });

    document.getElementById('reportPanel').scrollIntoView({behavior:'smooth', block:'nearest'});
  }

  document.getElementById('copyRewrite').addEventListener('click', function(){
    var text = document.getElementById('rwAfter').textContent;
    navigator.clipboard.writeText(text).then(function(){
      var btn = document.getElementById('copyRewrite');
      var orig = btn.textContent; btn.textContent = 'Copied!';
      setTimeout(function(){ btn.textContent = orig; }, 1400);
    }).catch(function(){});
  });

  async function runFollowup(prompt){
    log('Follow-up: '+prompt);
    var sys = "You are the Editor-in-Chief of an elite content studio, continuing a consulting engagement on a LinkedIn post aimed at personal-brand growth. Answer the specific follow-up question directly and concretely, referencing the original post. Respond in plain prose, 3-6 sentences, no JSON, no markdown symbols.";
    var userText = "ORIGINAL POST:\n\""+state.postText+"\"\n\nFOLLOW-UP QUESTION: "+prompt;
    try{
      var answer = await callClaude(sys, buildUserContent(userText), 500);
      var box = document.createElement('div');
      box.className = 'report-block fade-in';
      box.innerHTML = '<h4>'+escapeHtml(prompt)+'</h4><p>'+escapeHtml(answer)+'</p>';
      document.getElementById('tab-next').appendChild(box);
    }catch(err){
      showError('Follow-up failed: '+err.message, function(){ runFollowup(prompt); });
    }
  }

  document.getElementById('tabBar').addEventListener('click', function(e){
    var tab = e.target.closest('.tab');
    if(!tab) return;
    document.querySelectorAll('.tab').forEach(function(t){ t.classList.remove('active'); });
    document.querySelectorAll('.tab-panel').forEach(function(p){ p.classList.remove('active'); });
    tab.classList.add('active');
    document.getElementById('tab-'+tab.dataset.tab).classList.add('active');
  });

  function showError(msg, retryFn){
    errorArea.innerHTML = '<div class="error-banner"><span>⚠ '+escapeHtml(msg)+'</span><button id="retryBtn">Retry</button></div>';
    document.getElementById('retryBtn').addEventListener('click', function(){
      errorArea.innerHTML='';
      retryFn();
    });
  }

  updateRunNote();
})();
</script>
</body>
</html>
https://claude.ai/public/artifacts/3dbfac27-2efc-421d-82e5-eacb6978364e<img width="2800" height="1414" alt="Image 18-07-26 at 6 52 AM" src="https://github.com/user-attachments/assets/d65f1387-abf6-4b66-9b56-bc45f72087c5" />
<img width="2804" height="1224" alt="Image 18-07-26 at 6 53 AM" src="https://github.com/user-attachments/assets/b16f0f36-c79d-4225-8a45-ad29636b8f0a" />
