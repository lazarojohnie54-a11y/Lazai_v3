<!DOCTYPE html>
<html lang="sw">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
<title>LazAI PRO v3 🇹🇿</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;700;800&family=Rajdhani:wght@400;500;600;700&family=Share+Tech+Mono&display=swap" rel="stylesheet">
<style>
/* ══ THEMES ══ */
body.theme-blue{
  --bg:#030810;--s1:#060F1C;--s2:#091525;--card:#0B1A2E;
  --border:#0E2540;--border2:#163550;
  --p:#00F5CC;--p2:#0099FF;--acc:#00F5CC;
  --text:#8BBCD8;--text2:#C5DFF0;--muted:#1C3D5A;
}
body.theme-black{
  --bg:#0A0A0A;--s1:#111111;--s2:#181818;--card:#141414;
  --border:#252525;--border2:#333333;
  --p:#FFFFFF;--p2:#AAAAAA;--acc:#FFFFFF;
  --text:#888888;--text2:#CCCCCC;--muted:#333333;
}
body.theme-yellow{
  --bg:#0F0D00;--s1:#1A1700;--s2:#222000;--card:#1C1A00;
  --border:#3A3600;--border2:#4A4400;
  --p:#FFD700;--p2:#FFA500;--acc:#FFD700;
  --text:#C8B860;--text2:#EED970;--muted:#3A3200;
}
body.theme-red{
  --bg:#0F0005;--s1:#1A000A;--s2:#220010;--card:#1C0008;
  --border:#3A0015;--border2:#4A0020;
  --p:#FF3355;--p2:#FF6600;--acc:#FF3355;
  --text:#C86070;--text2:#EE8090;--muted:#3A0015;
}
body.theme-white{
  --bg:#F0F4F8;--s1:#E4EAF0;--s2:#D8E0EA;--card:#FFFFFF;
  --border:#C8D4E0;--border2:#B0C0D0;
  --p:#0066CC;--p2:#0099FF;--acc:#0066CC;
  --text:#4A6080;--text2:#1A3050;--muted:#A0B8CC;
}

*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent;}
html,body{height:100%;background:var(--bg);font-family:'Rajdhani',sans-serif;color:var(--text2);overflow:hidden;transition:background 0.3s,color 0.3s;}

body::before{content:'';position:fixed;inset:0;
  background-image:linear-gradient(rgba(var(--p-rgb,0,245,204),0.02) 1px,transparent 1px),linear-gradient(90deg,rgba(var(--p-rgb,0,245,204),0.02) 1px,transparent 1px);
  background-size:32px 32px;pointer-events:none;z-index:0;opacity:0.7;}

/* ══ LOCK ══ */
#lock{position:fixed;inset:0;z-index:999;background:var(--bg);display:flex;flex-direction:column;align-items:center;justify-content:center;padding:24px;}
.lock-glow{width:96px;height:96px;border-radius:50%;background:linear-gradient(135deg,var(--p),var(--p2));display:flex;align-items:center;justify-content:center;font-size:40px;margin-bottom:18px;box-shadow:0 0 60px rgba(0,245,204,0.25);animation:lp 3s ease-in-out infinite;}
@keyframes lp{0%,100%{transform:scale(1)}50%{transform:scale(1.04)}}
.lock-title{font-family:'Syne',sans-serif;font-weight:800;font-size:30px;letter-spacing:4px;color:var(--text2);margin-bottom:2px;}
.lock-title span{color:var(--p);}
.lock-ver{font-family:'Share Tech Mono',monospace;font-size:9px;letter-spacing:6px;color:var(--muted);margin-bottom:6px;}
.lock-by{font-size:11px;color:var(--muted);margin-bottom:28px;font-family:'Share Tech Mono',monospace;}
.lock-by b{color:var(--p);}
.lock-f{width:100%;max-width:300px;background:var(--card);border:1px solid var(--border);border-radius:14px;padding:14px 20px;color:var(--text2);font-size:18px;font-family:'Share Tech Mono',monospace;text-align:center;letter-spacing:6px;outline:none;margin-bottom:10px;}
.lock-f:focus{border-color:var(--p);opacity:0.6;}
.lock-f::placeholder{letter-spacing:2px;font-size:13px;color:var(--muted);}
.lock-go{width:100%;max-width:300px;padding:14px;background:linear-gradient(135deg,var(--p),var(--p2));border:none;border-radius:14px;color:var(--bg);font-family:'Syne',sans-serif;font-size:15px;font-weight:800;letter-spacing:3px;cursor:pointer;}
.lock-go:active{opacity:0.85;}
.lock-err{font-size:11px;color:#FF3355;text-align:center;margin-top:8px;font-family:'Share Tech Mono',monospace;height:16px;}

/* ══ APP ══ */
#app{display:none;flex-direction:column;height:100%;position:relative;z-index:1;}

/* HEADER */
.hdr{display:flex;align-items:center;gap:10px;padding:9px 13px 7px;background:rgba(var(--bg-rgb,3,8,16),0.96);border-bottom:1px solid var(--border);flex-shrink:0;backdrop-filter:blur(12px);}
.hdr-av{width:34px;height:34px;border-radius:9px;background:linear-gradient(135deg,var(--p),var(--p2));display:flex;align-items:center;justify-content:center;font-family:'Syne',sans-serif;font-weight:800;font-size:13px;color:var(--bg);flex-shrink:0;}
.hdr-name{font-family:'Syne',sans-serif;font-weight:800;font-size:14px;color:var(--text2);letter-spacing:1px;}
.hdr-name span{color:var(--p);}
.hdr-sub{font-family:'Share Tech Mono',monospace;font-size:8px;color:var(--muted);letter-spacing:1px;}
.hdr-right{display:flex;flex-direction:column;align-items:flex-end;gap:2px;margin-left:auto;}
.hdr-badge{font-family:'Share Tech Mono',monospace;font-size:8px;background:rgba(0,245,204,0.08);border:1px solid rgba(0,245,204,0.2);border-radius:5px;padding:2px 6px;color:var(--p);letter-spacing:1px;}
.pts-b{font-family:'Share Tech Mono',monospace;font-size:9px;color:#FFD700;letter-spacing:1px;cursor:pointer;}

/* PERSONALITY */
.pers-bar{display:flex;gap:5px;padding:5px 10px;background:var(--s1);border-bottom:1px solid var(--border);overflow-x:auto;flex-shrink:0;}
.pers-bar::-webkit-scrollbar{display:none;}
.pb{background:var(--card);border:1px solid var(--border);border-radius:18px;padding:4px 10px;font-size:10px;color:var(--text);cursor:pointer;white-space:nowrap;font-family:'Rajdhani',sans-serif;font-weight:600;}
.pb.on{background:rgba(0,245,204,0.08);border-color:var(--p);color:var(--p);}

/* TABS */
.tabs{display:flex;background:var(--s1);border-bottom:1px solid var(--border);flex-shrink:0;}
.tab{flex:1;padding:8px 2px 6px;text-align:center;cursor:pointer;font-size:8px;font-weight:700;color:var(--muted);letter-spacing:1px;border-bottom:2px solid transparent;transition:all 0.2s;font-family:'Rajdhani',sans-serif;}
.tab.on{color:var(--p);border-bottom-color:var(--p);}
.tab-ic{font-size:14px;display:block;margin-bottom:1px;}

/* PANELS */
.pnl{display:none;flex:1;overflow:hidden;flex-direction:column;}
.pnl.on{display:flex;}
.scroll{overflow-y:auto;flex:1;padding:12px 13px;}
.scroll::-webkit-scrollbar{width:2px;}
.scroll::-webkit-scrollbar-thumb{background:var(--border);}

/* ══ CHAT ══ */
.msgs{flex:1;overflow-y:auto;padding:12px 13px;display:flex;flex-direction:column;gap:10px;}
.msgs::-webkit-scrollbar{width:2px;}
.msg{max-width:85%;display:flex;flex-direction:column;gap:3px;}
.msg.u{align-self:flex-end;align-items:flex-end;}
.msg.b{align-self:flex-start;align-items:flex-start;}
.msg-lbl{font-size:8px;font-family:'Share Tech Mono',monospace;color:var(--muted);display:flex;align-items:center;gap:4px;}
.b-av{width:14px;height:14px;border-radius:4px;background:linear-gradient(135deg,var(--p),var(--p2));display:inline-flex;align-items:center;justify-content:center;font-size:7px;font-weight:800;color:var(--bg);font-family:'Syne',sans-serif;}
.bubble{padding:9px 12px;border-radius:13px;font-size:13px;line-height:1.7;word-break:break-word;}
.msg.u .bubble{background:linear-gradient(135deg,rgba(0,153,255,0.18),rgba(0,245,204,0.08));border:1px solid rgba(0,245,204,0.15);border-bottom-right-radius:4px;color:var(--text2);}
.msg.b .bubble{background:var(--card);border:1px solid var(--border);border-bottom-left-radius:4px;}
.msg-t{font-size:8px;color:var(--muted);font-family:'Share Tech Mono',monospace;}
.typing-b{display:flex;gap:4px;align-items:center;padding:10px 13px;background:var(--card);border:1px solid var(--border);border-radius:13px;border-bottom-left-radius:4px;}
.typing-b span{width:5px;height:5px;border-radius:50%;background:var(--p);animation:td 1.2s infinite;}
.typing-b span:nth-child(2){animation-delay:.2s;}
.typing-b span:nth-child(3){animation-delay:.4s;}
@keyframes td{0%,60%,100%{transform:translateY(0);opacity:.4}30%{transform:translateY(-4px);opacity:1}}
.qk{padding:6px 10px;display:flex;gap:5px;overflow-x:auto;border-top:1px solid var(--border);flex-shrink:0;}
.qk::-webkit-scrollbar{display:none;}
.qp{background:var(--card);border:1px solid var(--border);border-radius:16px;padding:4px 10px;font-size:10px;color:var(--text);cursor:pointer;white-space:nowrap;font-family:'Rajdhani',sans-serif;font-weight:600;}
.qp:active{border-color:var(--p);color:var(--p);}
.bot-bar{display:flex;flex-direction:column;background:var(--s1);border-top:1px solid var(--border);flex-shrink:0;padding:7px 10px;}
.hist-row{display:flex;align-items:center;justify-content:space-between;padding:0 2px 5px;}
.hist-txt{font-size:8px;color:var(--muted);font-family:'Share Tech Mono',monospace;}
.hist-clr{font-size:8px;color:var(--muted);background:none;border:none;cursor:pointer;font-family:'Share Tech Mono',monospace;}
.hist-st{font-size:8px;font-family:'Share Tech Mono',monospace;}
.inp-row{display:flex;gap:6px;align-items:flex-end;}
.chat-ta{flex:1;background:var(--card);border:1px solid var(--border);border-radius:11px;padding:9px 12px;color:var(--text2);font-size:14px;font-family:'Rajdhani',sans-serif;outline:none;resize:none;max-height:76px;}
.chat-ta:focus{border-color:var(--p);opacity:0.6;}
.chat-ta::placeholder{color:var(--muted);}
.send-b,.voice-b{width:40px;height:40px;border-radius:10px;border:none;cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:16px;flex-shrink:0;}
.send-b{background:linear-gradient(135deg,var(--p),var(--p2));color:var(--bg);}
.send-b:active,.voice-b:active{transform:scale(0.9);}
.send-b:disabled{opacity:0.3;cursor:not-allowed;}
.voice-b{background:var(--card);border:1px solid var(--border);}
.voice-b.on{background:rgba(255,51,85,0.15);border-color:#FF3355;animation:vp 1s infinite;}
@keyframes vp{0%,100%{box-shadow:0 0 0 0 rgba(255,51,85,0.4)}50%{box-shadow:0 0 0 8px rgba(255,51,85,0)}}

/* ══ TOOLS ══ */
.tools-grid{display:grid;grid-template-columns:1fr 1fr;gap:9px;margin-bottom:14px;}
.tc{background:var(--card);border:1px solid var(--border);border-radius:13px;padding:13px 11px;cursor:pointer;text-align:center;transition:all 0.15s;}
.tc:active{transform:scale(0.96);border-color:var(--p);}
.tc-ic{font-size:26px;display:block;margin-bottom:5px;}
.tc-n{font-family:'Syne',sans-serif;font-size:12px;font-weight:700;color:var(--text2);margin-bottom:2px;}
.tc-d{font-size:10px;color:var(--muted);line-height:1.4;}
.tool-box{background:var(--s2);border:1px solid var(--border);border-radius:13px;padding:13px;}
.tool-box-t{font-family:'Syne',sans-serif;font-size:13px;font-weight:800;color:var(--p);margin-bottom:10px;}
.t-inp{width:100%;background:var(--card);border:1px solid var(--border);border-radius:10px;padding:10px 12px;color:var(--text2);font-size:13px;font-family:'Rajdhani',sans-serif;outline:none;resize:none;min-height:68px;margin-bottom:9px;}
.t-inp:focus{border-color:var(--p);opacity:0.6;}
.t-inp::placeholder{color:var(--muted);}
.t-run{width:100%;padding:11px;background:linear-gradient(135deg,var(--p),var(--p2));border:none;border-radius:10px;color:var(--bg);font-family:'Syne',sans-serif;font-size:13px;font-weight:800;cursor:pointer;}
.t-res{background:var(--card);border:1px solid var(--border);border-radius:10px;padding:12px;font-size:13px;line-height:1.7;margin-top:9px;display:none;white-space:pre-wrap;color:var(--text2);}
.t-back{font-size:11px;color:var(--muted);background:none;border:none;cursor:pointer;font-family:'Share Tech Mono',monospace;margin-bottom:11px;}

/* ══ MEMORY ══ */
.mem-hdr{background:linear-gradient(135deg,rgba(0,245,204,0.06),rgba(0,153,255,0.04));border:1px solid var(--border2);border-radius:13px;padding:14px;margin-bottom:13px;text-align:center;}
.mem-av{width:52px;height:52px;border-radius:50%;background:linear-gradient(135deg,var(--p),var(--p2));display:flex;align-items:center;justify-content:center;font-size:22px;margin:0 auto 7px;}
.mem-uname{font-family:'Syne',sans-serif;font-size:17px;font-weight:800;color:var(--text2);}
.mem-since{font-size:9px;color:var(--muted);font-family:'Share Tech Mono',monospace;margin-top:2px;}
.mem-stats{display:flex;gap:7px;margin-top:11px;}
.ms{flex:1;background:var(--card);border:1px solid var(--border);border-radius:9px;padding:9px 5px;text-align:center;}
.ms-v{font-family:'Share Tech Mono',monospace;font-size:15px;color:#FFD700;display:block;font-weight:900;}
.ms-l{font-size:8px;color:var(--muted);font-family:'Share Tech Mono',monospace;}
.mem-sec{margin-bottom:13px;}
.mem-sec-t{font-family:'Syne',sans-serif;font-size:10px;font-weight:800;color:var(--p);letter-spacing:2px;margin-bottom:7px;}
.mem-item{background:var(--card);border:1px solid var(--border);border-radius:9px;padding:9px 12px;margin-bottom:5px;display:flex;align-items:center;gap:9px;}
.mi-ic{font-size:15px;flex-shrink:0;}
.mi-k{font-size:10px;color:var(--muted);font-family:'Share Tech Mono',monospace;}
.mi-v{font-size:13px;color:var(--text2);font-weight:600;}
.mi-e{font-size:11px;color:var(--muted);background:none;border:none;cursor:pointer;margin-left:auto;}
.mem-log{background:var(--card);border:1px solid var(--border);border-radius:9px;padding:8px 12px;margin-bottom:4px;font-size:11px;color:var(--text);line-height:1.5;}
.mem-log-t{font-size:8px;color:var(--muted);font-family:'Share Tech Mono',monospace;margin-top:2px;}

/* ══ IMAGE ══ */
.style-row{display:flex;gap:5px;overflow-x:auto;padding-bottom:3px;margin-bottom:9px;}
.style-row::-webkit-scrollbar{display:none;}
.sp{background:var(--card);border:1px solid var(--border);border-radius:16px;padding:4px 10px;font-size:10px;cursor:pointer;white-space:nowrap;color:var(--text);font-family:'Rajdhani',sans-serif;font-weight:600;}
.sp.on{border-color:var(--p);color:var(--p);background:rgba(0,245,204,0.06);}
.img-ta{width:100%;background:var(--card);border:1px solid var(--border);border-radius:11px;padding:11px 13px;color:var(--text2);font-size:13px;font-family:'Rajdhani',sans-serif;outline:none;resize:none;height:68px;margin-bottom:9px;}
.img-ta:focus{border-color:var(--p);opacity:0.6;}
.img-ta::placeholder{color:var(--muted);}
.img-go{width:100%;padding:12px;background:linear-gradient(135deg,#9D00FF,#FF3355);border:none;border-radius:11px;color:#fff;font-family:'Syne',sans-serif;font-size:13px;font-weight:800;cursor:pointer;}
.img-ph{background:var(--card);border:1px solid var(--border);border-radius:13px;padding:36px 20px;text-align:center;color:var(--muted);}
#imgOut img{width:100%;border-radius:13px;border:1px solid var(--border);margin-top:10px;}

/* ══ SETTINGS ══ */
.set-sec{margin-bottom:16px;}
.set-t{font-family:'Syne',sans-serif;font-size:10px;font-weight:800;color:var(--p);letter-spacing:2px;margin-bottom:9px;}
.theme-grid{display:grid;grid-template-columns:repeat(5,1fr);gap:8px;}
.theme-btn{border-radius:10px;height:48px;border:2px solid transparent;cursor:pointer;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:2px;font-size:8px;font-family:'Share Tech Mono',monospace;transition:all 0.2s;}
.theme-btn.on{border-color:var(--p);transform:scale(1.06);}
.theme-btn span{font-size:16px;}
.set-row{display:flex;align-items:center;justify-content:space-between;background:var(--card);border:1px solid var(--border);border-radius:10px;padding:12px 13px;margin-bottom:7px;}
.set-row-l{font-size:13px;color:var(--text2);font-weight:600;}
.set-row-s{font-size:10px;color:var(--muted);}
.set-inp{background:var(--s2);border:1px solid var(--border);border-radius:8px;padding:6px 10px;color:var(--text2);font-size:12px;font-family:'Rajdhani',sans-serif;outline:none;width:140px;}
.set-inp:focus{border-color:var(--p);opacity:0.6;}
.danger-btn{width:100%;padding:12px;background:rgba(255,51,85,0.1);border:1px solid rgba(255,51,85,0.3);border-radius:10px;color:#FF3355;font-family:'Syne',sans-serif;font-size:12px;font-weight:700;cursor:pointer;}

/* ══ DAILY CHALLENGE ══ */
.challenge-card{background:linear-gradient(135deg,rgba(0,245,204,0.07),rgba(157,0,255,0.06));border:1px solid var(--border2);border-radius:14px;padding:16px;margin-bottom:13px;}
.ch-header{display:flex;align-items:center;gap:10px;margin-bottom:12px;}
.ch-ic{font-size:28px;}
.ch-title{font-family:'Syne',sans-serif;font-size:14px;font-weight:800;color:var(--text2);}
.ch-sub{font-size:10px;color:var(--muted);font-family:'Share Tech Mono',monospace;}
.ch-badge{margin-left:auto;background:rgba(255,215,0,0.15);border:1px solid rgba(255,215,0,0.3);border-radius:8px;padding:4px 9px;font-size:10px;color:#FFD700;font-family:'Share Tech Mono',monospace;}
.ch-q{font-size:14px;color:var(--text2);line-height:1.7;margin-bottom:12px;font-weight:600;}
.ch-opts{display:flex;flex-direction:column;gap:7px;margin-bottom:10px;}
.ch-opt{background:var(--card);border:1.5px solid var(--border);border-radius:10px;padding:11px 14px;font-size:13px;color:var(--text);cursor:pointer;text-align:left;font-family:'Rajdhani',sans-serif;font-weight:600;transition:all 0.15s;}
.ch-opt:active{transform:scale(0.98);}
.ch-opt.correct{background:rgba(0,255,136,0.12);border-color:#00FF88;color:#00FF88;}
.ch-opt.wrong{background:rgba(255,51,85,0.12);border-color:#FF3355;color:#FF3355;}
.ch-opt.disabled{pointer-events:none;}
.ch-result{border-radius:10px;padding:11px 13px;font-size:12px;line-height:1.6;display:none;}
.ch-result.ok{background:rgba(0,255,136,0.08);border:1px solid rgba(0,255,136,0.2);color:#00FF88;}
.ch-result.fail{background:rgba(255,51,85,0.08);border:1px solid rgba(255,51,85,0.2);color:#FF7788;}
.ch-done{background:linear-gradient(135deg,rgba(255,215,0,0.1),rgba(255,140,0,0.08));border:1px solid rgba(255,215,0,0.2);border-radius:12px;padding:20px;text-align:center;}
.ch-done-ic{font-size:44px;display:block;margin-bottom:8px;}
.ch-done-t{font-family:'Syne',sans-serif;font-size:16px;font-weight:800;color:#FFD700;margin-bottom:4px;}
.ch-done-s{font-size:12px;color:var(--text);}
.ch-streak{display:flex;gap:5px;justify-content:center;margin-top:10px;}
.ch-dot{width:12px;height:12px;border-radius:50%;}

/* ══ DRAFT GAME ══ */
.draft-wrap{display:flex;flex-direction:column;align-items:center;padding:12px;}
.draft-hud{display:flex;gap:10px;width:100%;max-width:360px;margin-bottom:10px;}
.draft-hud-b{flex:1;background:var(--card);border:1px solid var(--border);border-radius:9px;padding:8px;text-align:center;}
.draft-hud-v{font-family:'Share Tech Mono',monospace;font-size:14px;font-weight:900;color:var(--text2);}
.draft-hud-l{font-size:8px;color:var(--muted);font-family:'Share Tech Mono',monospace;margin-top:2px;}
.draft-hud-b.active{border-color:var(--p);background:rgba(0,245,204,0.06);}
.draft-status{background:var(--card);border:1px solid var(--border);border-radius:9px;padding:8px 14px;margin-bottom:10px;font-family:'Share Tech Mono',monospace;font-size:10px;color:var(--p);text-align:center;letter-spacing:2px;width:100%;max-width:360px;}
.draft-board{display:grid;grid-template-columns:repeat(8,1fr);gap:1px;background:var(--border);border:2px solid var(--border);border-radius:10px;overflow:hidden;width:100%;max-width:360px;aspect-ratio:1/1;}
.sq{aspect-ratio:1/1;display:flex;align-items:center;justify-content:center;cursor:pointer;position:relative;transition:background 0.1s;}
.sq.dark{background:#1A2A3A;}
.sq.light{background:#2A3A4A;}
body.theme-yellow .sq.dark{background:#2A2000;}
body.theme-yellow .sq.light{background:#3A3010;}
body.theme-red .sq.dark{background:#2A0010;}
body.theme-red .sq.light{background:#1A0008;}
body.theme-white .sq.dark{background:#8090A0;}
body.theme-white .sq.light{background:#B0C0D0;}
body.theme-black .sq.dark{background:#1A1A1A;}
body.theme-black .sq.light{background:#2A2A2A;}
.sq.sel{background:rgba(0,245,204,0.25) !important;box-shadow:inset 0 0 0 2px var(--p);}
.sq.hint{background:rgba(255,215,0,0.2) !important;}
.piece{width:78%;height:78%;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:900;transition:transform 0.1s;box-shadow:0 2px 6px rgba(0,0,0,0.4);}
.piece.p1{background:radial-gradient(circle at 35% 35%,#FF6688,#CC0033);}
.piece.p2{background:radial-gradient(circle at 35% 35%,#AACCFF,#2244CC);}
.piece.king::after{content:'♛';font-size:11px;position:absolute;top:50%;left:50%;transform:translate(-50%,-50%);color:rgba(255,255,255,0.9);}
.draft-btns{display:flex;gap:8px;margin-t
