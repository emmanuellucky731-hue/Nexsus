<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NEXUS — Stories · Videos · Community · News</title>
<style>
  /* ── 100% SELF-CONTAINED: zero external fonts, zero CDN, zero APIs ── */
  :root {
    --bg: #0a0a0f;
    --surface: #111118;
    --surface2: #18181f;
    --surface3: #1e1e28;
    --border: rgba(255,255,255,0.07);
    --accent: #e8ff47;
    --accent2: #7c5cfc;
    --accent3: #ff5c8a;
    --accent4: #00d4aa;
    --text: #f0f0f5;
    --text2: #8888aa;
    --text3: #444458;
    --premium: linear-gradient(135deg, #f7c948, #ff8c42);
    --radius: 16px;
    --radius-sm: 10px;
    --font-display: 'Segoe UI', 'SF Pro Display', -apple-system, BlinkMacSystemFont, 'Helvetica Neue', Arial, sans-serif;
    --font-body: 'Segoe UI', 'SF Pro Text', -apple-system, BlinkMacSystemFont, 'Helvetica Neue', Arial, sans-serif;
    --font-serif: Georgia, 'Times New Roman', Times, serif;
  }

  * { margin:0; padding:0; box-sizing:border-box; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--font-body);
    min-height: 100vh;
    overflow-x: hidden;
  }

  body::after {
    content: '';
    position: fixed; inset: 0;
    background: repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(255,255,255,0.005) 2px,rgba(255,255,255,0.005) 4px);
    pointer-events: none; z-index: 9999;
  }

  /* ─── SPLASH ─────────────────────────────────── */
  #splash {
    position: fixed; inset: 0;
    background: var(--bg);
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    z-index: 1000;
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  #splash.hidden { opacity:0; transform:scale(1.04); pointer-events:none; }
  .splash-logo {
    font-family: var(--font-display);
    font-size: 72px; font-weight: 900; letter-spacing: -4px;
    color: var(--accent);
    text-shadow: 0 0 80px rgba(232,255,71,0.5), 0 0 160px rgba(232,255,71,0.2);
    animation: splashPulse 2s ease-in-out infinite;
  }
  .splash-tagline { font-size: 11px; letter-spacing: 5px; text-transform: uppercase; color: var(--text3); margin-top: 10px; }
  .splash-bar-wrap { width: 220px; height: 2px; background: var(--surface3); border-radius: 2px; margin-top: 52px; overflow: hidden; }
  .splash-bar { height: 100%; background: linear-gradient(90deg, var(--accent2), var(--accent), var(--accent4)); animation: loadBar 2.1s cubic-bezier(.4,0,.2,1) forwards; }
  @keyframes splashPulse { 0%,100%{opacity:1} 50%{opacity:0.65} }
  @keyframes loadBar { from{width:0} to{width:100%} }

  /* ─── LAYOUT ─────────────────────────────────── */
  .app { display:flex; min-height:100vh; }

  /* ─── SIDEBAR ────────────────────────────────── */
  .sidebar {
    width: 256px; background: var(--surface);
    border-right: 1px solid var(--border);
    display: flex; flex-direction: column;
    position: fixed; top:0; left:0; bottom:0; z-index:100;
    transition: transform 0.3s ease;
  }
  .sidebar-brand { padding: 26px 22px 18px; border-bottom: 1px solid var(--border); }
  .brand-name { font-family: var(--font-display); font-size: 26px; font-weight: 900; letter-spacing: -1.5px; color: var(--accent); text-shadow: 0 0 30px rgba(232,255,71,0.3); }
  .brand-tagline { font-size: 10px; letter-spacing: 2px; text-transform: uppercase; color: var(--text3); margin-top: 3px; }
  .nav-group { padding: 18px 10px 6px; }
  .nav-group-label { font-size: 9px; letter-spacing: 2.5px; text-transform: uppercase; color: var(--text3); padding: 0 12px; margin-bottom: 5px; }
  .nav-item {
    display: flex; align-items: center; gap: 11px;
    padding: 10px 13px; border-radius: var(--radius-sm);
    cursor: pointer; color: var(--text2); font-size: 13.5px; font-weight: 500;
    transition: all 0.18s; user-select: none;
  }
  .nav-item:hover { background: var(--surface2); color: var(--text); }
  .nav-item.active { background: rgba(232,255,71,0.09); color: var(--accent); }
  .nav-ico { font-size: 17px; width: 22px; text-align: center; }
  .nav-badge { margin-left: auto; font-size: 9.5px; font-weight: 800; padding: 2px 7px; border-radius: 20px; color: #fff; background: var(--accent3); }
  .nav-badge.live { background: var(--accent4); }
  .sidebar-footer { margin-top: auto; padding: 14px 10px; border-top: 1px solid var(--border); }
  .user-row { display: flex; align-items: center; gap: 11px; padding: 10px 12px; border-radius: var(--radius-sm); cursor: pointer; transition: background 0.18s; }
  .user-row:hover { background: var(--surface2); }
  .u-avatar { width: 36px; height: 36px; border-radius: 50%; background: linear-gradient(135deg, var(--accent2), var(--accent3)); display: flex; align-items: center; justify-content: center; font-size: 14px; font-weight: 800; color: #fff; flex-shrink: 0; }
  .u-name { font-size: 13px; font-weight: 700; color: var(--text); }
  .u-role { font-size: 10px; background: var(--premium); -webkit-background-clip: text; background-clip: text; -webkit-text-fill-color: transparent; font-weight: 800; }

  /* ─── MAIN ───────────────────────────────────── */
  .main { margin-left: 256px; flex:1; display:flex; flex-direction:column; }

  /* ─── TOPBAR ─────────────────────────────────── */
  .topbar {
    background: rgba(10,10,15,0.88); backdrop-filter: blur(24px);
    border-bottom: 1px solid var(--border);
    height: 62px; padding: 0 28px;
    display: flex; align-items: center; gap: 14px;
    position: sticky; top:0; z-index:50;
  }
  .hamburger { display:none; width:36px; height:36px; border-radius:50%; background:var(--surface2); border:1px solid var(--border); align-items:center; justify-content:center; cursor:pointer; font-size:17px; color:var(--text2); }
  .search-wrap { flex:1; max-width:460px; background:var(--surface2); border:1px solid var(--border); border-radius:50px; display:flex; align-items:center; padding:0 15px; gap:9px; transition:border-color 0.2s; }
  .search-wrap:focus-within { border-color:rgba(232,255,71,0.35); }
  .search-wrap input { flex:1; background:none; border:none; outline:none; color:var(--text); font-family:var(--font-body); font-size:13.5px; padding:9px 0; }
  .search-wrap input::placeholder { color:var(--text3); }
  .tb-actions { display:flex; gap:9px; margin-left:auto; }
  .tb-btn { width:36px; height:36px; border-radius:50%; background:var(--surface2); border:1px solid var(--border); display:flex; align-items:center; justify-content:center; cursor:pointer; color:var(--text2); font-size:15px; transition:all 0.18s; position:relative; }
  .tb-btn:hover { background:var(--surface3); color:var(--text); }
  .notif-dot { position:absolute; top:5px; right:5px; width:8px; height:8px; background:var(--accent3); border-radius:50%; border:2px solid var(--bg); }

  /* ─── PAGES ──────────────────────────────────── */
  .page { display:none; animation:fadeUp 0.28s ease; }
  .page.active { display:block; }
  @keyframes fadeUp { from{opacity:0;transform:translateY(10px)} to{opacity:1;transform:translateY(0)} }
  .pg { padding: 30px; }
  .pg-title { font-family:var(--font-display); font-size:30px; font-weight:900; letter-spacing:-1.2px; line-height:1.1; margin-bottom:5px; }
  .pg-title em { color:var(--accent); font-style:normal; }
  .pg-sub { font-size:13px; color:var(--text2); margin-bottom:26px; }

  /* ─── TABS ───────────────────────────────────── */
  .tabs { display:flex; gap:3px; background:var(--surface); border:1px solid var(--border); border-radius:50px; padding:4px; width:fit-content; margin-bottom:22px; flex-wrap:wrap; }
  .tab { padding:7px 18px; border-radius:50px; font-size:12.5px; font-weight:500; cursor:pointer; color:var(--text2); transition:all 0.18s; user-select:none; }
  .tab.active { background:var(--accent); color:var(--bg); font-weight:800; }

  /* ─── WIDGET ─────────────────────────────────── */
  .widget { background:var(--surface); border:1px solid var(--border); border-radius:var(--radius); padding:18px; margin-bottom:14px; }
  .widget-hd { font-family:var(--font-display); font-size:13px; font-weight:800; margin-bottom:14px; display:flex; align-items:center; justify-content:space-between; }
  .widget-more { font-size:11.5px; color:var(--accent); cursor:pointer; font-weight:600; }

  /* ─── HOME ───────────────────────────────────── */
  .stories-strip { display:flex; gap:13px; overflow-x:auto; padding-bottom:6px; margin-bottom:28px; scrollbar-width:none; }
  .stories-strip::-webkit-scrollbar { display:none; }
  .story-chip { flex-shrink:0; width:82px; text-align:center; cursor:pointer; }
  .story-ring { width:64px; height:64px; border-radius:50%; padding:2.5px; margin:0 auto 7px; background:linear-gradient(135deg,var(--accent),var(--accent2),var(--accent3)); }
  .story-ring.seen { background:var(--surface3); }
  .story-face { width:100%; height:100%; border-radius:50%; background:var(--surface2); border:2px solid var(--bg); display:flex; align-items:center; justify-content:center; font-size:20px; }
  .story-label { font-size:10.5px; color:var(--text2); white-space:nowrap; overflow:hidden; text-overflow:ellipsis; }
  .story-chip.add-chip .story-ring { background:var(--surface3); }
  .story-chip.add-chip .story-face { color:var(--accent); font-size:26px; }

  .feed-grid { display:grid; grid-template-columns:1fr 360px; gap:22px; }

  .create-box { background:var(--surface); border:1px solid var(--border); border-radius:var(--radius); padding:16px; margin-bottom:16px; }
  .create-row { display:flex; align-items:center; gap:11px; }
  .create-field { flex:1; background:var(--surface2); border:1px solid var(--border); border-radius:50px; padding:10px 17px; color:var(--text); font-family:var(--font-body); font-size:13.5px; outline:none; transition:border-color 0.2s; }
  .create-field:focus { border-color:rgba(232,255,71,0.3); }
  .create-field::placeholder { color:var(--text3); }
  .create-tools { display:flex; gap:5px; flex-wrap:wrap; margin-top:13px; padding-top:13px; border-top:1px solid var(--border); }
  .create-btn { display:flex; align-items:center; gap:6px; padding:7px 13px; border-radius:8px; cursor:pointer; font-size:12.5px; font-weight:500; color:var(--text2); transition:background 0.18s; }
  .create-btn:hover { background:var(--surface2); color:var(--text); }

  .status-banner { background:linear-gradient(135deg,rgba(124,92,252,0.14),rgba(255,92,138,0.09)); border:1px solid rgba(124,92,252,0.2); border-radius:var(--radius); padding:17px 20px; margin-bottom:14px; display:flex; align-items:center; gap:15px; }
  .sb-icon { font-size:28px; }
  .sb-info { flex:1; }
  .sb-title { font-size:14px; font-weight:700; margin-bottom:3px; }
  .sb-sub { font-size:11.5px; color:var(--text2); }
  .sb-timer { font-family:var(--font-display); font-size:19px; font-weight:900; color:var(--accent3); letter-spacing:-0.5px; }

  .post-card { background:var(--surface); border:1px solid var(--border); border-radius:var(--radius); margin-bottom:14px; overflow:hidden; transition:border-color 0.18s; }
  .post-card:hover { border-color:rgba(255,255,255,0.13); }
  .post-head { display:flex; align-items:center; gap:11px; padding:14px 16px; }
  .p-avatar { width:38px; height:38px; border-radius:50%; display:flex; align-items:center; justify-content:center; font-size:14px; font-weight:800; color:#fff; flex-shrink:0; }
  .p-meta { flex:1; }
  .p-author { font-size:13.5px; font-weight:700; display:flex; align-items:center; gap:5px; }
  .p-verified { color:var(--accent4); font-size:12px; }
  .p-time { font-size:11px; color:var(--text3); }
  .p-tag { font-size:9.5px; letter-spacing:1.5px; text-transform:uppercase; padding:3px 9px; border-radius:20px; font-weight:800; }
  .tag-ai { background:rgba(0,212,170,0.12); color:var(--accent4); }
  .tag-video { background:rgba(255,92,138,0.14); color:var(--accent3); }
  .tag-story { background:rgba(124,92,252,0.14); color:var(--accent2); }
  .tag-news { background:rgba(232,255,71,0.1); color:var(--accent); }
  .p-body { padding:0 16px 13px; }
  .p-title { font-family:var(--font-serif); font-size:17px; font-weight:700; line-height:1.35; margin-bottom:7px; }
  .p-text { font-size:13px; color:var(--text2); line-height:1.6; }
  .p-media { background:var(--surface2); aspect-ratio:16/9; display:flex; align-items:center; justify-content:center; font-size:44px; cursor:pointer; position:relative; overflow:hidden; margin-bottom:2px; }
  .p-media-grad { position:absolute; inset:0; }
  .p-play { position:absolute; width:52px; height:52px; border-radius:50%; background:rgba(0,0,0,0.6); display:flex; align-items:center; justify-content:center; font-size:18px; color:#fff; backdrop-filter:blur(6px); border:2px solid rgba(255,255,255,0.2); transition:transform 0.2s; }
  .p-media:hover .p-play { transform:scale(1.1); }
  .p-actions { display:flex; align-items:center; gap:2px; padding:10px; border-top:1px solid var(--border); }
  .act-btn { display:flex; align-items:center; gap:5px; padding:7px 12px; border-radius:8px; cursor:pointer; color:var(--text2); font-size:12.5px; font-weight:500; transition:all 0.18s; background:none; border:none; font-family:var(--font-body); }
  .act-btn:hover { background:var(--surface2); color:var(--text); }
  .act-btn.liked { color:var(--accent3); }
  .act-ml { margin-left:auto; }

  .trend-row { display:flex; align-items:center; gap:11px; padding:9px 0; border-bottom:1px solid var(--border); cursor:pointer; transition:padding-left 0.2s; }
  .trend-row:last-child { border-bottom:none; }
  .trend-row:hover { padding-left:4px; }
  .trend-n { font-family:var(--font-display); font-size:20px; font-weight:900; color:var(--surface3); width:26px; }
  .trend-info { flex:1; }
  .trend-topic { font-size:12.5px; font-weight:700; }
  .trend-count { font-size:10.5px; color:var(--text3); }

  .ch-row { display:flex; align-items:center; gap:11px; padding:9px 0; border-bottom:1px solid var(--border); cursor:pointer; }
  .ch-row:last-child { border-bottom:none; }
  .ch-icon { width:38px; height:38px; border-radius:10px; display:flex; align-items:center; justify-content:center; font-size:17px; flex-shrink:0; }
  .ch-info { flex:1; }
  .ch-name { font-size:12.5px; font-weight:700; }
  .ch-subs { font-size:10.5px; color:var(--text3); }
  .follow-btn { padding:4px 13px; background:rgba(232,255,71,0.08); color:var(--accent); border:1px solid rgba(232,255,71,0.22); border-radius:20px; font-size:11.5px; font-weight:700; cursor:pointer; transition:all 0.18s; }
  .follow-btn:hover { background:var(--accent); color:var(--bg); }
  .follow-btn.ing { background:var(--surface2); color:var(--text2); border-color:var(--border); }

  /* ─── VIDEOS ─────────────────────────────────── */
  .video-grid { display:grid; grid-template-columns:repeat(auto-fill,minmax(290px,1fr)); gap:18px; }
  .v-card { background:var(--surface); border:1px solid var(--border); border-radius:var(--radius); overflow:hidden; cursor:pointer; transition:all 0.2s; }
  .v-card:hover { border-color:rgba(255,255,255,0.15); transform:translateY(-2px); box-shadow:0 14px 44px rgba(0,0,0,0.45); }
  .v-thumb { aspect-ratio:16/9; position:relative; display:flex; align-items:center; justify-content:center; font-size:38px; background:var(--surface2); overflow:hidden; }
  .v-grad { position:absolute; inset:0; }
  .v-dur { position:absolute; bottom:7px; right:7px; background:rgba(0,0,0,0.82); color:#fff; font-size:10.5px; font-weight:700; padding:2px 7px; border-radius:4px; }
  .v-info { padding:13px; }
  .v-title { font-size:13.5px; font-weight:700; line-height:1.4; margin-bottom:7px; }
  .v-meta { font-size:11.5px; color:var(--text3); }
  .v-author { color:var(--text2); }

  /* ─── STORIES ────────────────────────────────── */
  .stories-grid { display:grid; grid-template-columns:repeat(auto-fill,minmax(270px,1fr)); gap:16px; }
  .s-card { background:var(--surface); border:1px solid var(--border); border-radius:var(--radius); padding:18px; cursor:pointer; transition:all 0.2s; }
  .s-card:hover { border-color:rgba(232,255,71,0.22); transform:translateY(-2px); }
  .s-type { font-size:9.5px; letter-spacing:2px; text-transform:uppercase; color:var(--accent); font-weight:800; margin-bottom:8px; }
  .s-title { font-family:var(--font-serif); font-size:19px; font-weight:700; line-height:1.3; margin-bottom:9px; }
  .s-excerpt { font-size:12.5px; color:var(--text2); line-height:1.6; margin-bottom:13px; }
  .s-footer { display:flex; align-items:center; gap:9px; }
  .s-read { font-size:10.5px; color:var(--text3); }
  .earn-tag { margin-left:auto; background:rgba(0,212,170,0.1); color:var(--accent4); font-size:10.5px; font-weight:700; padding:3px 9px; border-radius:20px; }

  /* ─── NEWS ───────────────────────────────────── */
  .news-hero { background:var(--surface); border:1px solid var(--border); border-radius:var(--radius); display:grid; grid-template-columns:1fr 1fr; overflow:hidden; margin-bottom:16px; }
  .news-hero-media { background:var(--surface2); display:flex; align-items:center; justify-content:center; font-size:72px; position:relative; overflow:hidden; min-height:230px; }
  .news-hero-body { padding:26px; display:flex; flex-direction:column; justify-content:center; }
  .ai-verified { display:inline-flex; align-items:center; gap:5px; font-size:10px; letter-spacing:1.5px; text-transform:uppercase; font-weight:800; color:var(--accent4); background:rgba(0,212,170,0.1); padding:4px 11px; border-radius:20px; margin-bottom:11px; width:fit-content; }
  .news-hero-title { font-family:var(--font-serif); font-size:20px; font-weight:700; line-height:1.3; margin-bottom:9px; }
  .news-hero-excerpt { font-size:12.5px; color:var(--text2); line-height:1.6; margin-bottom:14px; }
  .news-meta { font-size:11px; color:var(--text3); }
  .news-row { background:var(--surface); border:1px solid var(--border); border-radius:var(--radius-sm); padding:14px 16px; margin-bottom:9px; display:flex; gap:14px; cursor:pointer; transition:border-color 0.18s; }
  .news-row:hover { border-color:rgba(255,255,255,0.13); }
  .news-ico { font-size:28px; flex-shrink:0; width:40px; text-align:center; }
  .news-body { flex:1; }
  .news-cat { font-size:9.5px; font-weight:800; letter-spacing:2px; text-transform:uppercase; color:var(--accent); margin-bottom:3px; }
  .news-title { font-size:13.5px; font-weight:700; line-height:1.4; margin-bottom:4px; }
  .news-time { font-size:10.5px; color:var(--text3); }
  .accuracy-col { display:flex; flex-direction:column; align-items:flex-end; gap:4px; margin-left:auto; justify-content:center; }
  .acc-bar { width:56px; height:3px; background:var(--surface3); border-radius:2px; overflow:hidden; }
  .acc-fill { height:100%; background:var(--accent4); border-radius:2px; }
  .acc-lbl { font-size:9.5px; color:var(--text3); }

  /* ─── COMMUNITY ──────────────────────────────── */
  .com-hero { background:linear-gradient(135deg,rgba(124,92,252,0.14),rgba(232,255,71,0.05)); border:1px solid rgba(124,92,252,0.2); border-radius:var(--radius); padding:26px; margin-bottom:22px; display:flex; align-items:center; gap:18px; }
  .com-hero-icon { font-size:44px; }
  .com-hero-info { flex:1; }
  .com-hero-name { font-family:var(--font-display); font-size:22px; font-weight:900; margin-bottom:5px; }
  .com-stats { display:flex; gap:18px; }
  .com-stat { font-size:12.5px; color:var(--text2); }
  .com-stat strong { color:var(--text); }
  .join-all-btn { padding:11px 26px; background:var(--accent2); color:#fff; border:none; border-radius:50px; font-size:13.5px; font-weight:800; cursor:pointer; font-family:var(--font-body); transition:opacity 0.18s; }
  .join-all-btn:hover { opacity:0.84; }
  .com-grid { display:grid; grid-template-columns:repeat(auto-fill,minmax(250px,1fr)); gap:14px; }
  .com-card { background:var(--surface); border:1px solid var(--border); border-radius:var(--radius); padding:18px; cursor:pointer; transition:all 0.2s; }
  .com-card:hover { border-color:rgba(124,92,252,0.3); transform:translateY(-2px); }
  .com-card-ico { font-size:28px; margin-
