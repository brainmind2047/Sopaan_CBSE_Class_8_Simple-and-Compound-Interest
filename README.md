<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Sopaan · Simple and Compound Interest</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,500;9..144,700&family=Source+Sans+3:wght@400;600;700&family=IBM+Plex+Mono:wght@500;600&display=swap">
<style>
  html,body{margin:0;} img{max-width:100%;} [hidden]{display:none !important;}
  :root{
    --navy:#16264A; --navy-2:#1F3B6B; --gold:#C79A3E; --gold-soft:#F3E7C9;
    --paper:#FBF9F4; --paper-2:#F1EAD8; --card:#FFFFFF;
    --ink:#211E1A; --ink-soft:#655D4C; --rule:#E4DCC8;
    --success:#2E8B57; --success-soft:#E1F2E7;
    --danger:#BF4B45; --danger-soft:#FAE3E1;
    --locked:#C7BEA9;
    --focus:#1F3B6B;
    --accent-text:#1F3B6B; --retry-text:#8A661F;
    color-scheme:light;
  }
  @media (prefers-color-scheme: dark){
    :root:not([data-theme="light"]){
      --navy:#0E1830; --navy-2:#16264A; --gold:#E0B75B; --gold-soft:#3A2F16;
      --paper:#141210; --paper-2:#1C1914; --card:#1C1914;
      --ink:#EDE7DA; --ink-soft:#B2A996; --rule:#3A342A;
      --success:#7BC79A; --success-soft:#1B2E22;
      --danger:#E38884; --danger-soft:#331D1B;
      --locked:#4A4436;
      --focus:#E0B75B;
      --accent-text:#E0B75B; --retry-text:#E0B75B;
      color-scheme:dark;
    }
  }
  :root[data-theme="dark"]{
    --navy:#0E1830; --navy-2:#16264A; --gold:#E0B75B; --gold-soft:#3A2F16;
    --paper:#141210; --paper-2:#1C1914; --card:#1C1914;
    --ink:#EDE7DA; --ink-soft:#B2A996; --rule:#3A342A;
    --success:#7BC79A; --success-soft:#1B2E22;
    --danger:#E38884; --danger-soft:#331D1B;
    --locked:#4A4436;
    --focus:#E0B75B;
    --accent-text:#E0B75B; --retry-text:#E0B75B;
    color-scheme:dark;
  }

  *{box-sizing:border-box;}
  body{background:var(--paper); color:var(--ink); font-family:'Source Sans 3',-apple-system,'Segoe UI',sans-serif; padding-inline:0; padding-block:0;}
  h1,h2,h3{font-family:'Fraunces',Georgia,serif; text-wrap:balance; margin:0;}
  .num{font-family:'IBM Plex Mono',ui-monospace,monospace; font-variant-numeric:tabular-nums;}

  header.brand{
    background:linear-gradient(155deg,var(--navy) 0%, var(--navy-2) 100%);
    color:#F4EFDF; padding-block:calc(20px + env(safe-area-inset-top,0px)) 18px; padding-inline:20px;
  }
  .brand-row{display:flex; align-items:center; gap:12px; max-width:900px; margin:0 auto;}
  .crest{
    width:42px; height:42px; border-radius:10px; background:var(--gold); color:var(--navy);
    display:flex; align-items:center; justify-content:center; font-family:'Fraunces',serif; font-weight:700; font-size:18px; flex-shrink:0;
  }
  .brand-name{font-size:12px; letter-spacing:.08em; text-transform:uppercase; color:var(--gold); font-weight:700;}
  .series-name{font-size:19px; font-weight:700; font-family:'Fraunces',serif;}
  .chapter-eyebrow{max-width:900px; margin:14px auto 0; font-size:12px; letter-spacing:.06em; text-transform:uppercase; color:#AEB9D6;}
  .chapter-title{font-size:28px; max-width:900px; margin:2px auto 0;}
  .chapter-sub{font-size:14.5px; color:var(--gold); font-weight:700; max-width:900px; margin:3px auto 0;}

  .chapter-progress{max-width:900px; margin:14px auto 0; display:flex; align-items:center; gap:10px;}
  .cp-track{flex:1; height:6px; border-radius:99px; background:rgba(255,255,255,.18); overflow:hidden;}
  .cp-fill{height:100%; background:var(--gold); border-radius:99px; transition:width .3s ease;}
  .cp-label{font-size:11.5px; color:#CFD7EA; white-space:nowrap;}

  .tabbar{position:sticky; top:env(safe-area-inset-top,0px); z-index:15; background:var(--paper); border-bottom:1px solid var(--rule); overflow-x:auto; white-space:nowrap;}
  .tabbar-inner{max-width:900px; margin:0 auto; display:flex; padding-inline:16px;}
  .tab-btn{font-family:inherit; font-size:14px; font-weight:600; color:var(--ink-soft); background:none; border:none; padding:13px 16px; cursor:pointer; position:relative; flex-shrink:0;}
  .tab-btn.active{color:var(--accent-text);}
  .tab-btn.active::after{content:''; position:absolute; left:12px; right:12px; bottom:0; height:3px; background:var(--gold); border-radius:3px 3px 0 0;}
  .tab-count{font-size:11px; color:var(--ink-soft); margin-left:5px;}

  .slide-progress{max-width:900px; margin:0 auto; padding:10px 16px 0; display:flex; align-items:center; gap:10px;}
  .sp-track{flex:1; height:5px; border-radius:99px; background:var(--rule); overflow:hidden;}
  .sp-fill{height:100%; background:var(--accent-text); border-radius:99px; transition:width .3s ease;}
  .sp-label{font-size:12px; color:var(--ink-soft); white-space:nowrap; font-weight:600;}

  .wrap{max-width:900px; margin:0 auto; padding:16px 16px calc(110px + env(safe-area-inset-bottom,0px));}

  .qcard{background:var(--card); border:1px solid var(--rule); border-radius:14px; padding:18px;}
  .qhead{display:flex; align-items:flex-start; gap:10px; margin-bottom:10px;}
  .qnum{width:32px; height:32px; border-radius:8px; background:var(--gold-soft); color:var(--accent-text); display:flex; align-items:center; justify-content:center; font-weight:700; font-family:'Fraunces',serif; flex-shrink:0; font-size:14px;}
  .qtext{font-size:16px; line-height:1.55; flex:1;}
  .qtag{font-size:10.5px; color:var(--gold); background:var(--gold-soft); padding:2px 7px; border-radius:99px; font-weight:700; margin-left:6px; white-space:nowrap;}
  .marks-pill{font-size:11px; font-weight:700; color:var(--ink-soft); border:1px solid var(--rule); padding:3px 9px; border-radius:99px; margin-left:auto; flex-shrink:0; white-space:nowrap;}
  .step-badge{font-size:11px; font-weight:700; color:var(--accent-text); background:var(--paper-2); border:1px solid var(--rule); padding:3px 9px; border-radius:99px; display:inline-block; margin-bottom:12px;}

  .options{display:flex; flex-direction:column; gap:8px; margin-top:10px;}
  .opt{display:flex; align-items:center; gap:10px; padding:11px 12px; border:1.5px solid var(--rule); border-radius:10px; cursor:pointer; font-size:15px; background:var(--paper);}
  .opt input{accent-color:var(--navy-2);}
  .opt.is-correct{border-color:var(--success); background:var(--success-soft);}
  .opt.is-wrong{border-color:var(--danger); background:var(--danger-soft);}
  .opt.locked{cursor:not-allowed;}

  .subpart-label{font-weight:700; font-size:12.5px; color:var(--accent-text); text-transform:uppercase; letter-spacing:.03em; margin:14px 0 6px;}
  .or-divider{text-align:center; font-size:11px; font-weight:700; letter-spacing:.08em; color:var(--ink-soft); margin:8px 0;}

  .steps{display:flex; flex-direction:column; gap:10px;}
  .step-line{font-size:14.5px; line-height:1.9; background:var(--paper); border:1px dashed var(--rule); border-radius:10px; padding:9px 12px;}
  .step-line.resolved{opacity:.9;}
  .blank-input{font-family:'IBM Plex Mono',monospace; font-size:14px; border:1.5px solid var(--rule); border-radius:6px; padding:3px 8px; width:120px; background:var(--card); color:var(--ink); margin:0 2px;}
  .blank-input:focus{outline:none; border-color:var(--focus); box-shadow:0 0 0 3px var(--gold-soft);}
  .blank-input.is-correct{border-color:var(--success); background:var(--success-soft);}
  .blank-input.is-wrong{border-color:var(--danger); background:var(--danger-soft);}
  .blank-input[disabled]{opacity:.85;}
  .reveal-note{font-size:12px; color:var(--danger); padding-left:2px; margin-top:-2px;}

  .feedback{font-size:13.5px; padding:10px 12px; border-radius:9px; margin-top:14px; display:none;}
  .feedback.show{display:block;}
  .feedback.ok{background:var(--success-soft); color:var(--success);}
  .feedback.retry{background:var(--gold-soft); color:var(--retry-text);}
  .feedback.reveal{background:var(--danger-soft); color:var(--danger);}
  .feedback.err{background:var(--danger-soft); color:var(--danger);}
  .attempts-dots{display:inline-flex; gap:4px; margin-left:2px;}
  .attempts-dots span{width:6px; height:6px; border-radius:50%; background:var(--ink-soft); opacity:.3; display:inline-block;}
  .attempts-dots span.used{opacity:1; background:var(--danger);}

  .ar-box{background:var(--paper-2); border-radius:10px; padding:10px 12px; margin-bottom:12px; font-size:13px; color:var(--ink-soft);}

  .navbar{
    position:fixed; left:0; right:0; bottom:0; z-index:30; background:var(--paper);
    border-top:1px solid var(--rule); padding:10px 16px calc(10px + env(safe-area-inset-bottom,0px));
  }
  .navbar-inner{max-width:900px; margin:0 auto; display:flex; gap:8px; flex-wrap:wrap; align-items:center;}
  .btn{font-family:inherit; font-size:13.5px; font-weight:700; padding:10px 14px; border-radius:9px; border:1.5px solid var(--rule); background:var(--card); color:var(--ink); cursor:pointer;}
  .btn:hover{border-color:var(--navy-2);}
  .btn:disabled{opacity:.4; cursor:not-allowed;}
  .btn-primary{background:var(--navy-2); color:#fff; border-color:var(--navy-2);}
  .navbar .spacer{flex:1;}

  .fab{position:fixed; right:16px; bottom:calc(74px + env(safe-area-inset-bottom,0px)); background:var(--gold); color:var(--navy); border:none; border-radius:999px; padding:11px 16px; font-family:inherit; font-weight:700; font-size:13px; display:flex; align-items:center; gap:7px; cursor:pointer; box-shadow:0 6px 16px rgba(0,0,0,.18); z-index:35;}
  .fab-badge{background:rgba(255,255,255,.55); border-radius:99px; padding:1px 7px; font-size:11px;}

  .overlay{position:fixed; inset:0; background:rgba(20,18,14,.45); z-index:50; display:none; align-items:flex-end; justify-content:center;}
  .overlay.show{display:flex;}
  .palette{background:var(--card); width:min(480px,100%); max-height:78vh; overflow-y:auto; border-radius:18px 18px 0 0; padding:18px 18px calc(18px + env(safe-area-inset-bottom,0px)); border:1px solid var(--rule); border-bottom:none;}
  @media (min-width:640px){ .overlay{align-items:center;} .palette{border-radius:18px; border-bottom:1px solid var(--rule); max-height:74vh;} }
  .palette-head{display:flex; align-items:center; justify-content:space-between; margin-bottom:6px;}
  .palette-head h2{font-size:16px;}
  .palette-close{background:none; border:none; font-size:20px; color:var(--ink-soft); cursor:pointer; padding:4px;}
  .palette-legend{display:flex; gap:12px; flex-wrap:wrap; font-size:11px; color:var(--ink-soft); margin:10px 0 14px;}
  .palette-legend span{display:inline-flex; align-items:center; gap:5px;}
  .dot{width:9px; height:9px; border-radius:50%; display:inline-block;}
  .dot.correct{background:var(--success);} .dot.revealed{background:var(--danger);}
  .dot.skipped{background:var(--gold);} .dot.locked{background:var(--locked);}
  .dot.current{background:var(--navy-2);}
  .chip-grid{display:grid; grid-template-columns:repeat(auto-fill,minmax(48px,1fr)); gap:8px;}
  .chip{border:1.5px solid var(--rule); border-radius:9px; padding:8px 4px; text-align:center; font-family:'IBM Plex Mono',monospace; font-size:12.5px; font-weight:600; cursor:pointer; background:var(--paper); color:var(--ink);}
  .chip[data-status="correct"]{border-color:var(--success); background:var(--success-soft); color:var(--success);}
  .chip[data-status="revealed"]{border-color:var(--danger); background:var(--danger-soft); color:var(--danger);}
  .chip[data-status="skipped"]{border-color:var(--gold); background:var(--gold-soft); color:var(--retry-text);}
  .chip[data-status="locked"]{border-color:var(--rule); color:var(--locked); cursor:not-allowed; background:var(--paper-2);}
  .chip[data-status="current"]{outline:2px solid var(--navy-2); outline-offset:1px;}

  .toast{position:fixed; left:50%; bottom:calc(140px + env(safe-area-inset-bottom,0px)); transform:translateX(-50%); background:var(--ink); color:var(--paper); padding:9px 16px; border-radius:99px; font-size:13px; opacity:0; pointer-events:none; transition:opacity .25s ease; z-index:60;}
  .toast.show{opacity:1;}

  .done-card{text-align:center; padding:36px 20px;}
  .done-card .big{font-size:38px; margin-bottom:6px;}
  .score-pills{display:flex; gap:10px; justify-content:center; flex-wrap:wrap; margin:16px 0;}
  .score-pill{padding:8px 16px; border-radius:99px; font-size:13px; font-weight:700;}

  footer.brandfoot{max-width:900px; margin:14px auto 0; padding:0 16px calc(110px + env(safe-area-inset-bottom,0px)); text-align:center; font-size:12px; color:var(--ink-soft);}

  .mode-pill{font-family:inherit; font-size:12.5px; font-weight:700; color:var(--navy); background:var(--gold); border:none; border-radius:99px; padding:6px 14px; cursor:pointer; margin-top:12px; display:inline-flex; align-items:center; gap:6px;}
  .mode-pick{display:flex; flex-direction:column; gap:14px; padding:8px 0 24px;}
  .mode-card{background:var(--card); border:1.5px solid var(--rule); border-radius:16px; padding:22px; cursor:pointer; text-align:left;}
  .mode-card:hover{border-color:var(--navy-2);}
  .mode-card .mode-icon{font-size:26px; margin-bottom:8px;}
  .mode-card h3{font-size:18px; margin-bottom:6px;}
  .mode-card p{font-size:13.5px; color:var(--ink-soft); line-height:1.5; margin:0;}
  .quiz-hint{font-size:12.5px; color:var(--ink-soft); background:var(--paper-2); border-radius:9px; padding:8px 12px; margin-bottom:14px;}
  .review-row{border:1px solid var(--rule); border-radius:10px; padding:11px 13px; margin-bottom:10px;}
  .review-tag{font-size:11.5px; font-weight:700; margin-bottom:4px; display:block;}
  .review-tag.ok{color:var(--success);} .review-tag.bad{color:var(--danger);} .review-tag.na{color:var(--ink-soft);}
  .review-q{font-size:13.5px; margin-bottom:6px; color:var(--ink-soft);}
  .review-ans{font-size:13px; margin-bottom:2px;}

  .who-row{max-width:900px; margin:12px auto 0; display:flex; flex-wrap:wrap; gap:8px; align-items:center;}
  .who-row .mode-pill{margin-top:0;}
  .who{display:inline-flex; flex-wrap:wrap; align-items:center; gap:6px; font-size:12.5px; color:#CFD7EA;}
  .who b{color:#F4EFDF;}
  .who button{font-family:inherit; font-size:12px; font-weight:700; color:#F4EFDF; background:rgba(255,255,255,.12); border:1px solid rgba(255,255,255,.22); border-radius:99px; padding:5px 11px; cursor:pointer;}
  .who button:hover{background:rgba(255,255,255,.2);}
  .login-card{max-width:460px; margin:8px auto 0; background:var(--card); border:1px solid var(--rule); border-radius:16px; padding:22px;}
  .login-card h2{font-size:21px; margin-bottom:4px;}
  .login-card p.lead{font-size:13.5px; color:var(--ink-soft); margin:0 0 16px; line-height:1.5;}
  .fld{display:flex; flex-direction:column; gap:5px; margin-bottom:12px;}
  .fld label{font-size:12px; font-weight:700; letter-spacing:.04em; text-transform:uppercase; color:var(--ink-soft);}
  .fld input{font-family:inherit; font-size:15px; padding:10px 12px; border:1.5px solid var(--rule); border-radius:9px; background:var(--paper); color:var(--ink);}
  .fld input:focus{outline:none; border-color:var(--focus); box-shadow:0 0 0 3px var(--gold-soft);}
  .fld-row{display:grid; grid-template-columns:1fr 1fr; gap:10px;}
  .login-err{font-size:13px; color:var(--danger); background:var(--danger-soft); border-radius:8px; padding:8px 10px; margin-bottom:12px;}
  .login-note{font-size:12px; color:var(--ink-soft); margin-top:12px; line-height:1.5;}
  .known{margin:0 0 16px; display:flex; flex-direction:column; gap:6px;}
  .known-label{font-size:12px; font-weight:700; letter-spacing:.04em; text-transform:uppercase; color:var(--ink-soft);}
  .known-btn{display:flex; justify-content:space-between; align-items:center; gap:10px; text-align:left; font-family:inherit; font-size:14.5px; padding:10px 12px; border:1.5px solid var(--rule); border-radius:10px; background:var(--paper); color:var(--ink); cursor:pointer;}
  .known-btn:hover{border-color:var(--navy-2);}
  .known-btn small{font-size:12px; color:var(--ink-soft);}
  .rec-card{background:var(--card); border:1px solid var(--rule); border-radius:14px; padding:18px; margin-bottom:14px;}
  .rec-card h2{font-size:19px; margin-bottom:10px;}
  .rec-card h3{font-size:15px; margin:4px 0 8px;}
  .rec-table-wrap{overflow-x:auto;}
  .rec-table{width:100%; border-collapse:collapse; font-size:13.5px; font-variant-numeric:tabular-nums;}
  .rec-table th{text-align:left; font-size:11.5px; text-transform:uppercase; letter-spacing:.04em; color:var(--ink-soft); padding:6px 8px; border-bottom:1px solid var(--rule); white-space:nowrap;}
  .rec-table td{padding:8px; border-bottom:1px solid var(--rule); white-space:nowrap;}
  .rec-bar{display:inline-block; width:70px; height:6px; border-radius:99px; background:var(--rule); overflow:hidden; vertical-align:middle; margin-right:6px;}
  .rec-bar i{display:block; height:100%; background:var(--success);}
  .rec-empty{font-size:13.5px; color:var(--ink-soft);}
  .sec-sub{max-width:900px; margin:0 auto; padding:10px 16px 0; font-size:12.5px; font-weight:700; color:var(--accent-text); letter-spacing:.02em;}
  .opt{flex-wrap:wrap;}
  .opt-l{font-family:'IBM Plex Mono',monospace; font-size:13px; font-weight:600; color:var(--ink-soft);}
  .opt-t{flex:1; min-width:0;}
  .opt.is-chosen:not(.is-correct):not(.is-wrong){border-color:var(--navy-2); background:var(--gold-soft);}
  .opt-tag{font-size:11px; font-weight:700; padding:2px 8px; border-radius:99px; background:var(--card); border:1px solid currentColor; white-space:nowrap;}
  .opt.is-correct .opt-tag{color:var(--success);} .opt.is-wrong .opt-tag{color:var(--danger);} .opt.is-chosen:not(.is-correct):not(.is-wrong) .opt-tag{color:var(--accent-text);}
  .chosen{font-size:13.5px; margin-top:10px; padding:8px 12px; border-radius:9px;}
  .chosen.ok{background:var(--success-soft); color:var(--success);} .chosen.bad{background:var(--danger-soft); color:var(--danger);}
  .chosen + .chosen{margin-top:6px;}
  .solution{margin-top:14px; border:1px solid var(--rule); border-left:4px solid var(--gold); background:var(--paper-2); border-radius:10px; padding:12px 14px;}
  .sol-h{font-family:'Fraunces',Georgia,serif; font-weight:700; font-size:14px; color:var(--accent-text); margin-bottom:6px;}
  .sol-line{font-size:14.5px; line-height:1.7;}
  .rev-sol summary{cursor:pointer; font-size:12.5px; font-weight:700; color:var(--accent-text); margin-top:6px;}
  .rev-sol .solution{margin-top:8px;}
  .chapter-credit{max-width:900px; margin:4px auto 0; font-size:12px; color:#CFD7EA;}
  footer.brandfoot a{color:inherit;}
  .blank-input.wide{width:260px; max-width:100%; font-family:'Source Sans 3',sans-serif;}
  .blank-input.expr{width:170px; max-width:100%;}
  /*fix-layout*/ .cp-fill,.sp-fill{width:0;} .fld{min-width:0;} .fld input{width:100%; min-width:0; box-sizing:border-box;}
  .fig{margin:6px 0 10px; display:flex; justify-content:center;}
  .figsvg{width:100%; max-width:340px; height:auto; overflow:visible;}
  .figsvg .ln,.figsvg .arm{stroke:var(--ink); stroke-width:1.6; fill:none;}
  .figsvg .arm{stroke:var(--accent-text); stroke-width:2;}
  .figsvg .pt{fill:var(--ink);}
  .figsvg .lb{fill:var(--ink); font:600 13px 'Source Sans 3',sans-serif;}
  .figsvg .al{fill:var(--accent-text); font:700 12px 'Source Sans 3',sans-serif;}
  .figsvg .wg{fill:var(--gold-soft); stroke:var(--gold); stroke-width:1.2;}
  .figsvg .wg2{fill:rgba(199,154,62,.35); stroke:var(--gold); stroke-width:1.2;}
  .figsvg .ra{fill:none; stroke:var(--ink); stroke-width:1.2;}
  .figsvg .ahd{fill:var(--ink);}
  .figsvg .pr{fill:var(--paper-2); stroke:var(--ink-soft); stroke-width:1.2;}
  .figsvg .tk{stroke:var(--ink-soft); stroke-width:.8;}
  .figsvg .po{fill:var(--ink); font:600 8.5px 'IBM Plex Mono',monospace;}
  .figsvg .pi{fill:var(--danger); font:600 7.5px 'IBM Plex Mono',monospace;}
  .figsvg .sh{fill:var(--gold-soft); stroke:var(--ink); stroke-width:1.5; stroke-linejoin:round;}
  .figsvg .sh2{fill:rgba(199,154,62,.38); stroke:var(--ink); stroke-width:1.5; stroke-linejoin:round;}
  .figsvg .sh3{fill:rgba(199,154,62,.22); stroke:var(--ink); stroke-width:1.5; stroke-linejoin:round;}
  .figsvg .none{fill:none;}
  .figsvg .hid{stroke-dasharray:5 4; fill:none;}
  .figsvg .tick{stroke:var(--ink); stroke-width:1.4; fill:none;}
  .figsvg .shd{fill:var(--accent-text); fill-opacity:.55;}
  .figsvg .cell{fill:var(--card); stroke:var(--ink); stroke-width:1.1;}
  .figsvg .dr{fill:var(--danger);} .figsvg .dw{fill:var(--card); stroke:var(--ink); stroke-width:1.2;}
  .figsvg .dotfill{fill:var(--danger);}
  .tt{border-collapse:collapse; font-size:13.5px; margin:4px auto; font-variant-numeric:tabular-nums;} .tt th,.tt td{border:1px solid var(--rule); padding:4px 9px; text-align:left;} .tt th{background:var(--paper-2); font-weight:700;} .ttw{overflow-x:auto; max-width:100%;}
  .fq{display:inline-flex; flex-direction:column; vertical-align:middle; text-align:center; font-size:.82em; line-height:1.12; margin:0 2px;}
  .fq>span:first-child{border-bottom:1.5px solid currentColor; padding:0 2px;}
  .fq>span:last-child{padding:0 2px;}
  .mx{white-space:nowrap;}
  .blank-input.fr{width:110px;}
  @media (prefers-reduced-motion:reduce){ *{transition:none !important;} }
.datline{display:block;margin-top:8px;padding:8px 10px;border-radius:8px;background:var(--paper-2);font:500 14px/1.7 'IBM Plex Mono',monospace;word-spacing:2px;overflow-wrap:anywhere;}

  .theory{display:flex;flex-direction:column;gap:16px;padding-bottom:40px;}
  .hub{display:grid;grid-template-columns:1fr;gap:12px;}
  @media (min-width:640px){ .hub{grid-template-columns:repeat(3,1fr);} }
  .hub-card{background:var(--card);border:1px solid var(--rule);border-radius:14px;padding:16px;display:flex;flex-direction:column;gap:8px;}
  .hub-card h3{font-family:'Fraunces',serif;font-size:18px;margin:0;color:var(--accent-text);}
  .hub-card p{margin:0;font-size:14px;color:var(--ink-soft);line-height:1.5;}
  .hub-btns{display:flex;flex-wrap:wrap;gap:8px;margin-top:auto;}
  .hub-btn{min-height:40px;border:1.5px solid var(--rule);background:var(--paper-2);color:var(--ink);border-radius:10px;padding:8px 12px;font:600 14px 'Source Sans 3',sans-serif;cursor:pointer;text-align:left;}
  .hub-btn:hover{border-color:var(--gold);}
  .hub-btn.primary{background:var(--navy);color:#F4EFDF;border-color:var(--navy);}
  .note{background:var(--card);border:1px solid var(--rule);border-radius:14px;padding:18px;scroll-margin-top:120px;}
  .note h2{font-family:'Fraunces',serif;font-size:22px;margin:0 0 4px;color:var(--ink);}
  .note .lt{font-size:13.5px;color:var(--ink-soft);margin:0 0 12px;}
  .note .lt b{color:var(--accent-text);}
  .note h4{font:700 15px 'Source Sans 3',sans-serif;margin:16px 0 6px;color:var(--accent-text);}
  .note p,.note li{font-size:15.5px;line-height:1.6;}
  .note ul{padding-left:20px;margin:6px 0;}
  .keybox{background:var(--gold-soft);border-left:4px solid var(--gold);border-radius:8px;padding:10px 12px;margin:10px 0;font-size:15px;line-height:1.6;}
  .keybox b{color:var(--ink);}
  .ex{background:var(--paper-2);border-radius:10px;padding:12px;margin:10px 0;}
  .ex .exh{font-family:'Fraunces',serif;font-weight:700;color:var(--accent-text);margin-bottom:4px;}
  .ex .exl{font-size:15px;line-height:1.7;}
  .ttab{width:100%;border-collapse:collapse;font-size:14.5px;margin:8px 0;}
  .ttab th,.ttab td{border:1px solid var(--rule);padding:7px 8px;text-align:left;vertical-align:top;}
  .ttab th{background:var(--paper-2);}
  .tscroll{overflow-x:auto;}
  .mono{font-family:'IBM Plex Mono',monospace;font-size:.92em;}
  @media (max-width:480px){ .ttab{font-size:13.5px;} .ttab th,.ttab td{padding:6px;} }
  .note .figsvg{max-width:100%;height:auto;display:block;margin:8px auto;}


  .rep-top{display:flex;flex-wrap:wrap;gap:18px;align-items:center;justify-content:center;margin-top:8px;}
  .rep-legend{flex:1;min-width:220px;display:flex;flex-direction:column;gap:8px;}
  .rep-cap{font:700 13px 'Source Sans 3',sans-serif;color:var(--ink-soft);text-transform:uppercase;letter-spacing:.05em;}
  .rep-li{display:flex;align-items:center;gap:6px;font-size:15px;}
  .rep-n{margin-left:auto;white-space:nowrap;padding-left:8px;font-family:'IBM Plex Mono',monospace;font-weight:600;}
  .sw{display:inline-block;width:12px;height:12px;border-radius:3px;flex:none;}
  .rep-grid{display:grid;grid-template-columns:1fr;gap:12px;}
  @media (min-width:640px){ .rep-grid{grid-template-columns:1fr 1fr;} }
  .rep-card{background:var(--card);border:1px solid var(--rule);border-radius:14px;padding:14px;display:flex;flex-direction:column;gap:10px;}
  .rep-h{display:flex;align-items:center;gap:8px;font:700 16px 'Source Sans 3',sans-serif;}
  .crit{display:inline-grid;place-items:center;width:28px;height:28px;border-radius:50%;color:var(--card);font:700 15px Fraunces,serif;flex:none;}
  .rep-row{display:flex;gap:14px;align-items:center;}
  .rep-stats{display:flex;flex-direction:column;gap:5px;font-size:14.5px;}
  .rep-stats div{display:flex;align-items:center;gap:6px;}
  .rep-lvl{margin-top:4px;color:var(--accent-text);} .rep-lvl span{color:var(--ink-soft);font-size:13px;}
  .rep-note{font-size:13px;color:var(--ink-soft);}


  .skip-chips{display:flex;flex-wrap:wrap;gap:8px;justify-content:center;margin:12px 0;}
  .skip-chips .chip{min-width:48px;min-height:40px;cursor:pointer;border:1.5px solid var(--gold);background:var(--gold-soft);color:var(--retry-text);border-radius:10px;font:600 14px 'IBM Plex Mono',monospace;}
  .skip-btns{display:flex;flex-wrap:wrap;gap:10px;justify-content:center;margin-top:12px;}


  .kb-toggle{border:none;background:transparent;font-size:15px;cursor:pointer;padding:0 2px;vertical-align:middle;opacity:.7;}
  .vkb{position:fixed;left:0;right:0;bottom:0;z-index:80;background:var(--paper-2);border-top:1px solid var(--rule);box-shadow:0 -6px 20px rgba(0,0,0,.12);padding:6px 6px 8px;display:none;}
  .vkb.show{display:block;}
  .vkb-top{display:flex;justify-content:space-between;align-items:center;max-width:640px;margin:0 auto 4px;font:600 12px 'Source Sans 3',sans-serif;color:var(--ink-soft);}
  .vkb-link{border:none;background:none;color:var(--accent-text);font:600 12px 'Source Sans 3',sans-serif;cursor:pointer;text-decoration:underline;}
  .vkb-row{display:flex;gap:5px;max-width:640px;margin:0 auto 5px;}
  .vkb-k{flex:1;min-height:42px;border:1px solid var(--rule);border-radius:8px;background:var(--card);color:var(--ink);font:600 17px 'IBM Plex Mono',monospace;cursor:pointer;padding:0;}
  .vkb-k.fn{font:600 13px 'Source Sans 3',sans-serif;background:var(--gold-soft);}
  .vkb-k.done{background:var(--navy);color:#F4EFDF;border-color:var(--navy);}
  .vkb-k:active{transform:scale(.96);}
  body.kb-open .wrap{padding-bottom:360px;}
  body.kb-open .fab{display:none;}
  .tool-bar{display:flex;gap:8px;flex-wrap:wrap;margin:-4px 0 10px;}
  .tool-btn{min-height:36px;border:1.5px solid var(--gold);background:var(--gold-soft);color:var(--ink);border-radius:18px;padding:4px 12px;font:600 13.5px 'Source Sans 3',sans-serif;cursor:pointer;}
  .tool-panel{position:fixed;z-index:85;background:var(--card);border:1px solid var(--rule);border-radius:14px;box-shadow:0 10px 30px rgba(0,0,0,.25);display:none;}
  .tool-panel.show{display:block;}
  .tp-head{display:flex;align-items:center;gap:8px;padding:8px 10px;border-bottom:1px solid var(--rule);font:600 14px 'Source Sans 3',sans-serif;}
  .tp-note{font-size:12px;color:var(--ink-soft);font-weight:500;}
  .tp-x{margin-left:auto;border:1px solid var(--rule);background:var(--paper-2);color:var(--ink);border-radius:8px;min-height:32px;padding:2px 10px;cursor:pointer;font:600 13px 'Source Sans 3',sans-serif;}
  .tp-x + .tp-x{margin-left:0;}
  .calc{right:12px;bottom:84px;width:min(330px,calc(100vw - 24px));}
  body.calc-open .wrap{padding-bottom:440px;}
  body.calc-open .fab{display:none;}
  @media (max-width:640px){ .calc{left:6px;right:6px;width:auto;} .calc-keys button{min-height:36px;} }
  .calc-disp{padding:8px 12px;text-align:right;background:var(--paper-2);}
  .calc-expr{font:500 13px 'IBM Plex Mono',monospace;color:var(--ink-soft);min-height:18px;word-break:break-all;}
  .calc-res{font:600 24px 'IBM Plex Mono',monospace;color:var(--ink);word-break:break-all;}
  .calc-keys{display:grid;grid-template-columns:repeat(6,1fr);gap:5px;padding:8px;}
  .calc-keys button{min-height:40px;border:1px solid var(--rule);border-radius:8px;background:var(--card);color:var(--ink);font:600 14px 'IBM Plex Mono',monospace;cursor:pointer;padding:0;}
  .calc-keys button.fn{background:var(--gold-soft);font-family:'Source Sans 3',sans-serif;font-size:13px;}
  .calc-keys button.eq{grid-column:span 2;background:var(--navy);color:#F4EFDF;border-color:var(--navy);}
  .desmos{left:50%;top:50%;transform:translate(-50%,-50%);width:min(760px,calc(100vw - 16px));height:min(560px,calc(100vh - 90px));flex-direction:column;}
  .desmos.show{display:flex;}
  #desmosBox{flex:1;min-height:0;border-radius:0 0 14px 14px;overflow:hidden;}
  .desmos-msg{padding:24px;text-align:center;color:var(--ink-soft);}
  .chip[data-status="skipped"]{cursor:pointer;}
  .chip[data-status="answered"]{border-color:var(--accent-text);color:var(--accent-text);}


  button.crest-home{border:none;padding:0;position:relative;cursor:pointer;transition:transform .15s ease;}
  button.crest-home:hover,button.crest-home:focus-visible{transform:scale(1.06);outline:2px solid var(--gold);outline-offset:2px;}
  .crest-h{position:absolute;right:-7px;bottom:-7px;width:18px;height:18px;border-radius:50%;background:#F4EFDF;color:var(--navy);font:700 12px/18px 'Source Sans 3',sans-serif;text-align:center;box-shadow:0 1px 3px rgba(0,0,0,.3);}
  .brand .brand-row{position:relative;}
  .bmasw{position:absolute;left:50%;top:50%;transform:translate(-50%,-50%);display:flex;flex-shrink:0;white-space:nowrap;align-items:center;gap:6px;background:rgba(255,255,255,.12);border:1px solid rgba(255,255,255,.25);border-radius:99px;padding:5px 14px;color:#F4EFDF;}
  .bmasw-ic{font-size:16px;} .bmasw-t{font:600 20px 'IBM Plex Mono',monospace;letter-spacing:.02em;min-width:62px;text-align:center;}
  .bmasw-b{border:none;background:rgba(255,255,255,.18);color:#F4EFDF;border-radius:50%;width:30px;height:30px;cursor:pointer;font-size:13px;}
  .bmasw.off{display:none;}
  @media (max-width:560px){ .bmasw{position:static;transform:none;margin-left:auto;padding:4px 5px 4px 8px;gap:4px;} .bmasw-ic{display:none;} .bmasw-t{font-size:16px;min-width:48px;} .bmasw-b{width:26px;height:26px;} .brand .series-name{font-size:15px;} .brand .brand-name{font-size:10.5px;} .brand .brand-row>div:not(.bmasw){min-width:0;} }
  .bmasw-done{font:600 15px 'IBM Plex Mono',monospace;color:var(--accent-text);margin:4px 0 8px;}
  .sp-fab{position:fixed;left:14px;bottom:84px;z-index:60;border:1.5px solid var(--navy-2);background:var(--card);color:var(--ink);border-radius:99px;padding:9px 14px;font:700 14px 'Source Sans 3',sans-serif;box-shadow:0 4px 14px rgba(0,0,0,.15);cursor:pointer;}
  .sp-fab.on{background:var(--navy);color:#F4EFDF;}
  body.kb-open .sp-fab{display:none;}
  .sp-canvas{position:absolute;z-index:55;display:none;touch-action:none;cursor:crosshair;}
  .sp-canvas.passive{pointer-events:none;cursor:default;}
  .sp-bar{position:fixed;top:8px;left:8px;right:8px;margin:0 auto;width:max-content;z-index:90;display:none;align-items:center;gap:6px;background:var(--card);border:1px solid var(--rule);border-radius:14px;padding:6px 8px;box-shadow:0 6px 20px rgba(0,0,0,.2);max-width:calc(100vw - 16px);flex-wrap:wrap;justify-content:center;}
  .sp-lbl{font:700 13px 'Source Sans 3',sans-serif;color:var(--ink-soft);margin-right:2px;}
  .sp-pen,.sp-tool{width:38px;height:38px;border-radius:10px;border:1.5px solid var(--rule);background:var(--paper);cursor:pointer;display:inline-flex;align-items:center;justify-content:center;font-size:17px;padding:0;color:var(--ink);}
  .sp-pen i{width:20px;height:20px;border-radius:50%;display:block;}
  .sp-pen.on,.sp-tool.on{border-color:var(--navy-2);box-shadow:0 0 0 3px var(--gold-soft);}
  @media (max-width:560px){ .sp-lbl{display:none;} .sp-pen,.sp-tool{width:34px;height:34px;} .sp-fab span{display:none;} }

  /* larger reading sizes */
  .chapter-eyebrow{font-size:13.5px;}
  .chapter-title{font-size:36px;line-height:1.15;}
  .chapter-sub{font-size:16.5px;}
  .tab-btn{font-size:15.5px;}
  .sec-sub{font-size:15px;}
  .qtext{font-size:19px;line-height:1.55;}
  .qnum{width:36px;height:36px;font-size:16px;}
  .opt{font-size:17.5px;padding:12px 14px;}
  .step-line{font-size:17.5px;line-height:2;}
  .blank-input{font-size:16px;}
  .sol-line{font-size:16.5px;}
  .feedback{font-size:15px;}
  .note h2{font-size:28px;}
  .note h4{font-size:19px;}
  .note p,.note li{font-size:17.5px;line-height:1.65;}
  .note .lt{font-size:15.5px;}
  .ex .exh{font-size:18px;} .ex .exl{font-size:16.5px;}
  .keybox{font-size:16.5px;}
  .ttab{font-size:15.5px;}
  .hub-card h3{font-size:21px;} .hub-card p{font-size:15.5px;} .hub-btn{font-size:15px;}
  @media (max-width:480px){ .chapter-title{font-size:30px;} .qtext{font-size:18px;} .opt,.step-line{font-size:16.5px;} .note h2{font-size:24px;} .note p,.note li{font-size:16.5px;} }
</style>
</head>
<body>
<header class="brand">
  <div class="brand-row">
    <div class="crest">BM</div>
    <div>
      <div class="brand-name">Brain &amp; Mind Academy</div>
      <div class="series-name">Sopaan <span style="font-weight:400;font-size:14px;color:#CFD7EA;">Practice Series</span></div>
    </div>
  </div>
  <div class="chapter-eyebrow">Class 8 Mathematics · Chapter 11</div>
  <div class="chapter-title">Simple and Compound Interest</div>
  <div class="chapter-sub">Theory Notes · Practice by Learning Objective · Learning Assessment</div><div class="chapter-credit">Mixed multiple-choice and fill-in-the-blank practice · Chapter 11</div>
  <div class="chapter-progress">
    <div class="cp-track"><div class="cp-fill" id="cpFill"></div></div>
    <div class="cp-label" id="cpLabel">0% complete</div>
  </div>
  <div class="who-row"><button class="mode-pill" id="modePill" hidden>Choose a mode</button><span class="who" id="whoBar" hidden></span></div>
</header>

<nav class="tabbar"><div class="tabbar-inner" id="tabbar"></div></nav>
<div class="sec-sub" id="secSub"></div><div class="slide-progress"><div class="sp-track"><div class="sp-fill" id="spFill"></div></div><div class="sp-label" id="spLabel">Question 1 of 49</div></div>
<div class="wrap" id="wrap"></div>
<footer class="brandfoot">Brain &amp; Mind Academy · Sopaan Practice Series · Class 8 Mathematics · Chapter 11<br>Chapter follows the Class 8 mathematics syllabus (New Enjoying Mathematics, Class 8). Theory notes, questions, learning assessments and worked solutions are written by Brain &amp; Mind Academy.</footer>

<div class="navbar"><div class="navbar-inner" id="navbarInner"></div></div>
<button class="fab" id="paletteFab"><span>Questions</span><span class="fab-badge" id="fabBadge">0/49</span></button>

<div class="overlay" id="overlay">
  <div class="palette" role="dialog" aria-label="Question palette">
    <div class="palette-head"><h2 id="paletteTitle">Question palette</h2><button class="palette-close" id="paletteClose">&times;</button></div>
    <div class="palette-legend">
      <span><i class="dot current"></i>Current</span><span><i class="dot correct"></i>Correct</span>
      <span><i class="dot revealed"></i>Revealed</span><span><i class="dot skipped"></i>Skipped</span>
      <span><i class="dot locked"></i>Locked</span>
    </div>
    <div class="chip-grid" id="paletteBody"></div>
  </div>
</div>
<div class="toast" id="toast"></div>

<script>
(function(){
"use strict";

/* ================= audio ================= */
var audioCtx=null;
function ensureAudio(){ if(!audioCtx){ try{ audioCtx=new (window.AudioContext||window.webkitAudioContext)(); }catch(e){} } return audioCtx; }
function playTone(freqs,dur,type){
  var ctx=ensureAudio(); if(!ctx) return;
  try{
    var t0=ctx.currentTime;
    freqs.forEach(function(f,i){
      var o=ctx.createOscillator(), g=ctx.createGain();
      o.type=type||'sine'; o.frequency.value=f;
      var start=t0+i*dur;
      g.gain.setValueAtTime(0.0001,start);
      g.gain.exponentialRampToValueAtTime(0.16,start+0.02);
      g.gain.exponentialRampToValueAtTime(0.0001,start+dur);
      o.connect(g); g.connect(ctx.destination);
      o.start(start); o.stop(start+dur+0.02);
    });
  }catch(e){}
}
function playSuccess(){ playTone([523.25,659.25,783.99],0.11,'sine'); }
function playWrong(){ playTone([220,185],0.14,'square'); }
function playReveal(){ playTone([300,220],0.16,'triangle'); }

/* ================= helpers ================= */
function norm(s){
  return String(s===undefined||s===null?'':s).trim().toLowerCase().replace(/\s+/g,'')
    .replace(/[×∗*·]/g,'x').replace(/÷/g,'/').replace(/–|—|−/g,'-')
    .replace(/[²]/g,'^2').replace(/[³]/g,'^3').replace(/[⁴]/g,'^4').replace(/[⁵]/g,'^5')
    .replace(/[⁶]/g,'^6').replace(/[⁷]/g,'^7').replace(/[⁸]/g,'^8').replace(/[⁹]/g,'^9')
    .replace(/\^/g,'');
}
function parseNum(s){
  if(s===undefined||s===null) return null;
  var t=String(s).trim().replace(/,/g,'').replace(/[−–—]/g,'-').replace(/\s+/g,''); if(t==='') return null;
  var neg=false; if(t[0]==='-'){neg=true;t=t.slice(1);}
  var m=t.match(/^(\d+)\/(\d+)$/);
  if(m){ var v=parseInt(m[1],10)/parseInt(m[2],10); return neg?-v:v; }
  if(/^\d+(\.\d+)?$/.test(t)){ var v2=parseFloat(t); return neg?-v2:v2; }
  return null;
}
/* ---- expression checker: compares answers like (P-2w)/2 and P/2-w at random values ---- */
function exprPrep(s){
  return String(s).toLowerCase().replace(/\s+/g,'').replace(/^[a-z]\(x\)=/i,'').replace(/^y=/i,'').replace(/[×∗·]/g,'*').replace(/÷/g,'/').replace(/[−–—]/g,'-')
    .replace(/²/g,'^2').replace(/³/g,'^3').replace(/⁴/g,'^4').replace(/⁵/g,'^5').replace(/⁶/g,'^6').replace(/⁷/g,'^7').replace(/⁸/g,'^8').replace(/⁹/g,'^9').replace(/π/g,'#').replace(/pi/gi,'#').replace(/½/g,'(1/2)');
}
function exprCompile(src){
  var s=exprPrep(src), i=0, toks=[], absDepth=0;
  while(i<s.length){
    var ch=s[i];
    if(/[0-9.]/.test(ch)){ var j=i; while(j<s.length && /[0-9.]/.test(s[j])) j++; toks.push({k:'n',v:parseFloat(s.slice(i,j))}); i=j; continue; }
    if(/[a-zA-Z#]/.test(ch)){ toks.push({k:'v',v:ch}); i++; continue; }
    if(ch==='|'){ var pv=toks[toks.length-1]; var opn=(absDepth===0)||!pv||('+-*/^(['.indexOf(pv.k)>=0); if(opn){ absDepth++; toks.push({k:'['}); } else { absDepth--; toks.push({k:']'}); } i++; continue; }
    if('+-*/^()'.indexOf(ch)>=0){ toks.push({k:ch}); i++; continue; }
    return null;
  }
  var out=[];
  for(var t=0;t<toks.length;t++){
    var a=toks[t], b=out[out.length-1];
    if(b && (b.k==='n'||b.k==='v'||b.k===')'||b.k===']') && (a.k==='n'||a.k==='v'||a.k==='('||a.k==='[')) out.push({k:'&'});
    out.push(a);
  }
  var p=0;
  function peek(){ return out[p]; }
  function parseE(){ var n=parseT(); while(peek() && (peek().k==='+'||peek().k==='-')){ var o=out[p++].k, r=parseT(); n=(function(l,r,o){return function(e){ return o==='+'?l(e)+r(e):l(e)-r(e); };})(n,r,o); } return n; }
  function parseI(){ var n=parseU(); while(peek() && peek().k==='&'){ p++; var r=parseP(); n=(function(l,r){return function(e){ return l(e)*r(e); };})(n,r); } return n; }
  function parseT(){ var n=parseI(); while(peek() && (peek().k==='*'||peek().k==='/')){ var o=out[p++].k, r=parseI(); n=(function(l,r,o){return function(e){ return o==='*'?l(e)*r(e):l(e)/r(e); };})(n,r,o); } return n; }
  function parseU(){ if(peek() && peek().k==='-'){ p++; var u=parseU(); return function(e){ return -u(e); }; } if(peek() && peek().k==='+'){ p++; return parseU(); } return parseP(); }
  function parseP(){ var b=parseA(); if(peek() && peek().k==='^'){ p++; var x=parseU(); return function(e){ return Math.pow(b(e),x(e)); }; } return b; }
  function parseA(){
    var t=out[p++]; if(!t) throw 0;
    if(t.k==='n') return function(){ return t.v; };
    if(t.k==='v') return t.v==='#' ? function(){ return Math.PI; } : function(e){ return e[t.v]; };
    if(t.k==='('){ var n=parseE(); if(!peek()||peek().k!==')') throw 0; p++; return n; }
    if(t.k==='['){ var m=parseE(); if(!peek()||peek().k!==']') throw 0; p++; return function(e){ return Math.abs(m(e)); }; }
    throw 0;
  }
  try{ var f=parseE(); if(p!==out.length) return null; return f; }catch(e){ return null; }
}
function exprEqual(input,answer){
  var f=exprCompile(input), g=exprCompile(answer); if(!f||!g) return false;
  var hits=0;
  for(var trial=0;trial<8;trial++){
    var env={}; 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('').forEach(function(c){ env[c]=1.3+Math.random()*4.1; });
    var x=f(env), y=g(env);
    if(!isFinite(x)||!isFinite(y)) continue;
    if(Math.abs(x-y)>1e-7*Math.max(1,Math.abs(x),Math.abs(y))) return false;
    hits++;
  }
  return hits>=3;
}
function wordsNorm(s){ return String(s||'').toLowerCase().replace(/\band\b/g,' ').replace(/[^a-z]/g,''); }
function listNorm(s){ return (String(s||'').replace(/[−–—]/g,'-').replace(/(\d) (?=\d{3}\b)/g,'$1').match(/-?\d+(\.\d+)?/g)||[]).join(','); }
function powNorm(s){ return String(s||'').toLowerCase().replace(/\s+/g,'').replace(/[×∗*·.]/g,'x').replace(/[⁰¹²³⁴⁵⁶⁷⁸⁹]+/g,function(m){ return '^'+m.split('').map(function(c){ return '⁰¹²³⁴⁵⁶⁷⁸⁹'.indexOf(c); }).join(''); }).replace(/\^1(?!\d)/g,''); }
function fr(s){ return String(s).replace(/\{(\d+) (\d+)\/(\d+)\}/g,'<span class="mx">$1<span class="fq"><span>$2</span><span>$3</span></span></span>').replace(/\{(\d+)\/(\d+)\}/g,'<span class="fq"><span>$1</span><span>$2</span></span>'); }
function gcdI(a,b){ a=Math.abs(a); b=Math.abs(b); while(b){ var t=a%b; a=b; b=t; } return a; }
function fracParse(s){ s=String(s===undefined||s===null?'':s).trim().replace(/[\u2044\u2215\u00f7]/g,'/').replace(/\s+/g,' ').replace(/\s*\/\s*/g,'/'); var m;
  if((m=s.match(/^(-?\d+)$/))) return {v:+m[1],form:'int',n:+m[1],d:1};
  if((m=s.match(/^(-?\d+)\/(\d+)$/))){ if(+m[2]===0) return null; return {v:m[1]/m[2],form:'frac',n:+m[1],d:+m[2]}; }
  if((m=s.match(/^(-?)(\d+)(?: |\+)(\d+)\/(\d+)$/))){ if(+m[4]===0) return null; var sg=m[1]?-1:1; return {v:sg*(+m[2]+m[3]/m[4]),form:'mixed',w:sg*m[2],n:+m[3],d:+m[4]}; }
  if((m=s.match(/^-?\d*\.\d+$/))) return {v:parseFloat(s),form:'dec'};
  return null; }
function fracOK(mode,input,answer){
  if(mode==='flist'){ var A=String(input).split(/[,;]/).map(function(x){return x.trim();}).filter(Boolean), K=String(answer).split(/[,;]/).map(function(x){return x.trim();});
    if(A.length!==K.length) return false; return A.every(function(x,i){ var a=fracParse(x), k=fracParse(K[i]); return a&&k&&Math.abs(a.v-k.v)<1e-9; }); }
  var a=fracParse(input), k=fracParse(answer); if(!a||!k) return false;
  var same=Math.abs(a.v-k.v)<1e-9; if(!same) return false;
  if(mode==='fv') return true;
  if(mode==='dec') return a.form==='dec'||a.form==='int';
  if(mode==='fe') return (a.form==='frac'&&k.form==='frac'&&a.n===k.n&&a.d===k.d)||(a.form==='int'&&k.form==='int');
  if(mode==='fi') return a.form==='frac'||(a.form==='int'&&k.form==='int');
  if(mode==='fl') return a.form==='int'||(a.form==='frac'&&gcdI(a.n,a.d)===1)||(a.form==='mixed'&&a.n<a.d&&gcdI(a.n,a.d)===1);
  if(mode==='fm') return a.form==='int'||(a.form==='mixed'&&a.n>0&&a.n<a.d&&gcdI(a.n,a.d)===1);
  return false; }
function answerMatches(input,answer,accept,expr){
  if(expr==='dec'||expr==='fv'||expr==='fe'||expr==='fl'||expr==='fm'||expr==='fi'||expr==='flist'){ if(input===undefined||input===null||String(input).trim()==='') return false; return fracOK(expr,input,answer); }
  if(input===undefined||input===null||String(input).trim()==='') return false;
  if(expr==='words'){ return [answer].concat(accept||[]).some(function(a){ if(/\d/.test(a)) return norm(a)===norm(input); var w=wordsNorm(a); return w!=='' && w===wordsNorm(input); }); }
  if(expr==='list'){ return [answer].concat(accept||[]).some(function(a){ return listNorm(a)===listNorm(input); }); }
  if(expr==='pow'){ return [answer].concat(accept||[]).some(function(a){ return powNorm(a)===powNorm(input); }); }
  if(expr==='time'){ var tn=function(x){ var t=String(x).toLowerCase().replace(/[\s.]/g,'').replace(/[:h]/g,''); if(/^\d{3}(am|pm)?$/.test(t)) t='0'+t; return t; }; return [answer].concat(accept||[]).some(function(a){ return tn(a)===tn(input); }); }
  if(expr==='glist'){ var gn=function(x){ return String(x).toUpperCase().split(/[\s,;]+/).filter(Boolean).sort().join(','); }; return [answer].concat(accept||[]).some(function(a){ return gn(a)===gn(input); }); }
  if(expr==='coord'){ var cn=function(x){ return String(x).replace(/[\u2212\u2013\u2014]/g,'-').replace(/[\s()\[\]]/g,''); }; return [answer].concat(accept||[]).some(function(a){ return cn(a)===cn(input); }); }
  if(expr==='dlist'){ var dn=function(x){ return (String(x).replace(/[−–—]/g,'-').match(/-?\d*\.?\d+/g)||[]).map(Number).join(','); }; return [answer].concat(accept||[]).some(function(a){ return dn(a)===dn(input); }); }
  if(expr==='set'){ var sn=function(x){ return (String(x).match(/-?\d+/g)||[]).map(Number).sort(function(a,b){return a-b;}).join(','); }; return [answer].concat(accept||[]).some(function(a){ return sn(a)===sn(input); }); }
  if(expr==='primes'){ var pn=function(x){ var t=powNorm(x).replace(/[^0-9x^]/g,''); var out=[]; t.split('x').forEach(function(tok){ if(!tok) return; var m=tok.split('^'); var b=+m[0], e=m[1]?+m[1]:1; for(var i=0;i<e;i++) out.push(b); }); return out.sort(function(a,b){return a-b;}).join(','); }; return [answer].concat(accept||[]).some(function(a){ return pn(a)===pn(input); }); }
  if(expr==='angle'){ var an=function(x){ return String(x).toUpperCase().replace(/[^A-Z]/g,''); }; var k=an(answer), v=an(input); return v===k || v===k.split('').reverse().join(''); }
  if(expr==='trans'){ var tv=function(x){ var s=String(x).toLowerCase().replace(/[−–—]/g,'-').replace(/\b(units?|squares?|and|then|steps?|to|the|a)\b/g,' ').replace(/[,;.]/g,' '); var re=/(\d+)\s*(right|left|up|down|r|l|u|d)\b/g, m, dx=0, dy=0, n=0; while((m=re.exec(s))){ var v=+m[1], d=m[2][0]; if(d==='r')dx+=v; else if(d==='l')dx-=v; else if(d==='u')dy+=v; else dy-=v; n++; } if(!n||s.replace(re,'').replace(/\s+/g,'')!=='') return null; return dx+','+dy; }; var ti=tv(input); return ti!==null && [answer].concat(accept||[]).some(function(a){ return tv(a)===ti; }); }
  if(expr==='rot'){ var rv=function(x){ var s=String(x).toLowerCase().replace(/quarter[\s-]*turn/g,'90').replace(/half[\s-]*turn/g,'180').replace(/three[\s-]*quarter[\s-]*turn/g,'270'); var m=s.match(/\b(90|180|270)\b/); if(!m) return null; var a=+m[1]; if(a===180) return '180'; var dir=/anti|counter|acw|ccw/.test(s)?-1:(/clockwise|\bcw\b/.test(s)?1:0); if(!dir) return null; return String(((a*dir)%360+360)%360); }; var ri=rv(input); return ri!==null && ri===rv(answer); }
  if(expr==='expanded'){ var f=function(x){ return String(x).replace(/\s+/g,'').replace(/,/g,''); }; return [answer].concat(accept||[]).some(function(a){ return f(a)===f(input); }); }
  if(expr===true && input!==undefined && input!==null && String(input).trim()!==''){
    if(exprEqual(input,answer)) return true;
    var alt=String(input).replace(/\/\s*(\d+(?:\.\d+)?)\s*([a-zA-Z(])/g,'/$1*$2'); if(alt!==String(input) && exprEqual(alt,answer)) return true;
    return (accept||[]).some(function(a){ return exprEqual(input,a); });
  }
  if(input===undefined||input===null||String(input).trim()==='') return false;
  var n1=parseNum(input), n2=parseNum(answer);
  if(n1!==null && n2!==null){ if(Math.abs(n1-n2)<1e-3) return true; return (accept||[]).some(function(a){ var n3=parseNum(a); return n3!==null && Math.abs(n1-n3)<1e-3; }); }
  var cands=[answer].concat(accept||[]); var ni=norm(input);
  for(var i=0;i<cands.length;i++){ if(norm(cands[i])===ni) return true; }
  return false;
}
function esc(s){ return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;'); }

/* ================= DATA ================= */
var AR_OPTIONS = ["Both A and R are true, and R is the correct explanation of A","Both A and R are true, but R is NOT the correct explanation of A","A is true but R is false","A is false but R is true"];
var THEORY = "<div class=\"hub\"><div class=\"hub-card\"><h3>📖 Theory notes</h3><p>Explained notes for every part of the chapter, following the book, with the formulas, tables and solved examples.</p><div class=\"hub-btns\"><button class=\"hub-btn\" data-jump=\"n111\">11.1 notes</button><button class=\"hub-btn\" data-jump=\"n112\">11.2 notes</button><button class=\"hub-btn\" data-jump=\"n113\">11.3 notes</button><button class=\"hub-btn\" data-jump=\"n114\">11.4 notes</button><button class=\"hub-btn\" data-jump=\"n115\">11.5 notes</button><button class=\"hub-btn\" data-jump=\"n116\">11.6 notes</button><button class=\"hub-btn\" data-jump=\"n117\">11.7 notes</button></div></div><div class=\"hub-card\"><h3>🎯 Practice by learning objective</h3><p>Every Looking Back item, Example, Try This and Exercise question of the chapter, one sheet per objective, mixing multiple-choice and fill-in-the-blank questions. The bold tag shows where each question is in the book.</p><div class=\"hub-btns\"><button class=\"hub-btn\" data-go=\"s1\">11.1 · Simple interest and amount</button><button class=\"hub-btn\" data-go=\"s2\">11.2 · Finding principal, rate and time</button><button class=\"hub-btn\" data-go=\"s3\">11.3 · Compound interest year by year</button><button class=\"hub-btn\" data-go=\"s4\">11.4 · The compound interest formula</button><button class=\"hub-btn\" data-go=\"s5\">11.5 · Half-yearly and quarterly compounding</button><button class=\"hub-btn\" data-go=\"s6\">11.6 · Finding time, principal and rate</button><button class=\"hub-btn\" data-go=\"s7\">11.7 · Growth, appreciation and depreciation</button></div></div><div class=\"hub-card\"><h3>📝 Learning assessment</h3><p>Four short assessments built from the Chapter Check-up, one per skill area. Take them in Quiz mode and open the report to see your results as pie charts.</p><div class=\"hub-btns\"><button class=\"hub-btn\" data-go=\"s8\">A · Knowing and understanding</button><button class=\"hub-btn\" data-go=\"s9\">B · Investigating patterns</button><button class=\"hub-btn\" data-go=\"s10\">C · Communicating</button><button class=\"hub-btn\" data-go=\"s11\">D · Applying mathematics in real-life contexts</button><button class=\"hub-btn primary\" data-go=\"report\">📊 View my report</button></div></div></div><section class=\"note\" id=\"nintro\"><h2>About this chapter</h2><p>When we borrow money we pay extra money, called <b>interest</b>, for using it. When we deposit money in a bank, the bank pays us interest. In <b>simple interest</b> the interest is the same every year; in <b>compound interest</b> the interest of each period is added to the principal, so the interest grows every period.</p><p>The practice sheets contain <b>all</b> the questions of the chapter in book order. Each question starts with a tag such as <b>Looking Back · Q2</b>, <b>Example 7</b>, <b>Try This (p. 136) · a</b>, <b>Ex 11C · Q5</b> or <b>Check-up · MCQ 1</b>.</p><div class=\"tscroll\"><table class=\"ttab\"><tr><th>Assessment</th><th>Skill area</th><th>What it checks</th></tr><tr><td>A</td><td>Knowing and understanding</td><td>Using the SI and CI formulas correctly.</td></tr><tr><td>B</td><td>Investigating patterns</td><td>Doubling times, reverse problems and the CI − SI pattern.</td></tr><tr><td>C</td><td>Communicating</td><td>Choosing the right formula, explaining steps, spotting errors.</td></tr><tr><td>D</td><td>Applying mathematics in real-life contexts</td><td>Deposits, loans, populations, prices and depreciation.</td></tr></table></div><p><b>Tools:</b> ⏱ at the top times each tab (pause or reset it). ✏️ opens a scratchpad with four pens for rough work. Tap the BM badge to go back to the home page.</p><p><b>Typing answers:</b> money may be typed with or without ₹ and commas (<span class=\"mono\">8470</span>, <span class=\"mono\">₹8,470</span> and <span class=\"mono\">Rs 8470</span> are all accepted). Give paise as two decimal places, e.g. <span class=\"mono\">722.50</span>. When an answer is not exact the question says <b>to the nearest paisa</b> (two decimal places), as in the book; an answer rounded to one decimal place or to the nearest rupee is also accepted. Times in years may be typed as fractions, mixed numbers or decimals (<span class=\"mono\">5/2</span>, <span class=\"mono\">2 1/2</span> or <span class=\"mono\">2.5</span>).</p></section><section class=\"note\" id=\"n111\"><h2>11.1 Simple interest and amount</h2><p class=\"lt\"><b>Objective:</b> Recall principal, rate, time, interest and amount, and find the simple interest and the amount using SI = PRT/100 and A = P + SI.</p><p>The money borrowed or deposited is the <b>principal</b> (P). The extra money paid is the <b>interest</b> (I). The <b>rate</b> (R) is the interest on ₹100 for one year (per cent per annum, p.a.), and the <b>time</b> (T) is in years. The total paid back is the <b>amount</b> (A).</p><div class=\"tscroll\"><table class=\"ttab\"><tr><th>Relation</th><th>Formula</th></tr><tr><td>Amount</td><td>A = P + I</td></tr><tr><td>Principal</td><td>P = A − I</td></tr><tr><td>Interest</td><td>I = A − P</td></tr><tr><td>Simple interest</td><td>SI = <span class=\"fq\"><span>P × R × T</span><span>100</span></span></td></tr><tr><td>Amount in one step</td><td>A = P + <span class=\"fq\"><span>PRT</span><span>100</span></span> = P(1 + <span class=\"fq\"><span>RT</span><span>100</span></span>)</td></tr></table></div><div class=\"ex\"><div class=\"exh\">Book Example 2 · ₹7000 at 7% p.a. for 3 years</div><div class=\"exl\">SI = 7000 × 3 × 7 ÷ 100 = <b>₹1470</b>.<br>Amount = ₹7000 + ₹1470 = <b>₹8470</b>.</div></div><h4>Time in months and days</h4><p>Time must be in <b>years</b>: 8 months = {8/12} year, 1 year 8 months = {20/12} years, 73 days = {73/365} = {1/5} year (a year has 365 days).</p><div class=\"ex\"><div class=\"exh\">Book Example 3 · ₹600 at {7 1/2}% for 1 year 8 months</div><div class=\"exl\">R = {15/2}% and T = {20/12} years.<br>SI = 600 × {20/12} × {15/2} ÷ 100 = <b>₹75</b>; A = ₹600 + ₹75 = <b>₹675</b>.</div></div><div class=\"ex\"><div class=\"exh\">Book Example 7 · A = P(1 + RT/100)</div><div class=\"exl\">₹6000 at 6% for 3 years: A = 6000 × (1 + {18/100}) = 6000 × {118/100} = <b>₹7080</b>.</div></div><div class=\"keybox\"><b>Remember:</b> the rate is always <i>per annum</i>, so change months and days into years before using the formula.</div><div class=\"hub-btns\" style=\"margin-top:12px\"><button class=\"hub-btn primary\" data-go=\"s1\">Practise 11.1 →</button></div></section><section class=\"note\" id=\"n112\"><h2>11.2 Finding principal, rate and time</h2><p class=\"lt\"><b>Objective:</b> Rearrange the simple interest formula to find the principal, the rate or the time, including times given in days and months.</p><p>The formula SI = <span class=\"fq\"><span>P × R × T</span><span>100</span></span> can be rearranged to find any one of P, R and T when the other three are known.</p><div class=\"tscroll\"><table class=\"ttab\"><tr><th>To find</th><th>Formula</th></tr><tr><td>Principal</td><td>P = <span class=\"fq\"><span>SI × 100</span><span>R × T</span></span></td></tr><tr><td>Rate</td><td>R = <span class=\"fq\"><span>SI × 100</span><span>P × T</span></span></td></tr><tr><td>Time</td><td>T = <span class=\"fq\"><span>SI × 100</span><span>P × R</span></span></td></tr></table></div><div class=\"ex\"><div class=\"exh\">Book Example 4 · Principal</div><div class=\"exl\">R = {6 1/4}% = {25/4}%, T = 146 days = {146/365} year, SI = ₹30.<br>P = 30 × 100 × 4 × 365 ÷ (25 × 146) = <b>₹1200</b>.</div></div><div class=\"ex\"><div class=\"exh\">Book Example 5 · Rate</div><div class=\"exl\">SI = ₹15,315 − ₹15,000 = ₹315; T = 219 days = {3/5} year.<br>R = 315 × 100 × 5 ÷ (15000 × 3) = <b>3.5% p.a.</b></div></div><div class=\"ex\"><div class=\"exh\">Book Example 9 · Doubling and tripling</div><div class=\"exl\">Take P = ₹100. It doubles in 10 years, so SI = ₹100 and R = 100 × 100 ÷ (100 × 10) = 10%.<br>To triple, SI = ₹200: T = 100 × 200 ÷ (100 × 10) = <b>20 years</b>.</div></div><div class=\"keybox\"><b>When only the amount is given</b>, find SI = A − P first. When two amounts after different times are given, their difference is the interest for the extra years.</div><div class=\"hub-btns\" style=\"margin-top:12px\"><button class=\"hub-btn primary\" data-go=\"s2\">Practise 11.2 →</button></div></section><section class=\"note\" id=\"n113\"><h2>11.3 Compound interest year by year</h2><p class=\"lt\"><b>Objective:</b> Understand compound interest as interest on successive amounts, find it year by year and compare it with simple interest.</p><p>Abu invests ₹8000 at 10% p.a. <b>simple</b> interest for 3 years: SI = ₹2400 and he gets ₹10,400. Ali invests ₹8000 at 10% but at the end of each year the interest is <b>added to the principal</b>:</p><div class=\"tscroll\"><table class=\"ttab\"><tr><th>Year</th><th>Principal</th><th>Interest (10%)</th><th>Amount</th></tr><tr><td>1</td><td>₹8000</td><td>₹800</td><td>₹8800</td></tr><tr><td>2</td><td>₹8800</td><td>₹880</td><td>₹9680</td></tr><tr><td>3</td><td>₹9680</td><td>₹968</td><td>₹10,648</td></tr></table></div><p>Ali earns ₹2648, i.e. ₹248 more than Abu. <b>Interest calculated on the successive amounts is called compound interest (CI).</b> CI = final amount − original principal.</p><h4>Conversion period</h4><p>The time after which interest is added to the principal is the <b>conversion period</b>: one year (compounded annually), half a year (half-yearly / semi-annually) or three months (quarterly). <b>If no conversion period is given, it is one year.</b></p><div class=\"ex\"><div class=\"exh\">Book Example 10 · ₹3600 at 10% for 3 years, compounded annually</div><div class=\"exl\">Year 1: interest ₹360 → amount ₹3960.<br>Year 2: interest ₹396 → amount ₹4356.<br>Year 3: interest ₹435.60 → amount ₹4791.60.<br>CI = ₹4791.60 − ₹3600 = <b>₹1191.60</b>.</div></div><div class=\"keybox\"><b>CI is never less than SI</b> for the same P, R and T (more than one year): the interest earns interest.</div><div class=\"hub-btns\" style=\"margin-top:12px\"><button class=\"hub-btn primary\" data-go=\"s3\">Practise 11.3 →</button></div></section><section class=\"note\" id=\"n114\"><h2>11.4 The compound interest formula</h2><p class=\"lt\"><b>Objective:</b> Use A = P(1 + R/100)<sup>t</sup> and CI = A − P for interest compounded annually.</p><p>Each year the amount is multiplied by (1 + <span class=\"fq\"><span>R</span><span>100</span></span>). After t years:</p><div class=\"tscroll\"><table class=\"ttab\"><tr><th>Compounded annually</th><td>A = P(1 + <span class=\"fq\"><span>R</span><span>100</span></span>)<sup>t</sup></td></tr><tr><th>Compound interest</th><td>CI = A − P = P[(1 + <span class=\"fq\"><span>R</span><span>100</span></span>)<sup>t</sup> − 1]</td></tr></table></div><div class=\"ex\"><div class=\"exh\">Book · Sohan borrows ₹4000 at 15% for 3 years</div><div class=\"exl\">A = 4000 × ({115/100})<sup>3</sup> = 4000 × ({23/20})<sup>3</sup> = <b>₹6083.50</b>.<br>CI = ₹6083.50 − ₹4000 = <b>₹2083.50</b>.</div></div><div class=\"ex\"><div class=\"exh\">Book Example 13 · ₹7000 at 5% for 3 years</div><div class=\"exl\">A = 7000 × ({21/20})<sup>3</sup> = ₹8103.375 = <b>₹8103.38</b> (to the nearest paisa).<br>CI = ₹8103.38 − ₹7000 = <b>₹1103.38</b>.</div></div><h4>A fraction of a year</h4><p>For a time such as {2 1/2} years compounded annually, compound for the 2 whole years, then add simple interest for the remaining half year on that amount.</p><div class=\"keybox\"><b>Round only at the end</b> (to the nearest paisa, two decimal places) to avoid rounding errors.</div><div class=\"hub-btns\" style=\"margin-top:12px\"><button class=\"hub-btn primary\" data-go=\"s4\">Practise 11.4 →</button></div></section><section class=\"note\" id=\"n115\"><h2>11.5 Half-yearly and quarterly compounding</h2><p class=\"lt\"><b>Objective:</b> Find compound interest when the conversion period is a half-year or a quarter, by halving or quartering the rate and multiplying the number of periods.</p><p>If interest is compounded <b>half-yearly</b>, the rate per period is <span class=\"fq\"><span>R</span><span>2</span></span>% and the number of periods is 2t. If it is compounded <b>quarterly</b>, the rate per period is <span class=\"fq\"><span>R</span><span>4</span></span>% and there are 4t periods.</p><div class=\"tscroll\"><table class=\"ttab\"><tr><th>Half-yearly</th><td>A = P(1 + <span class=\"fq\"><span>R</span><span>200</span></span>)<sup>2t</sup></td></tr><tr><th>Quarterly</th><td>A = P(1 + <span class=\"fq\"><span>R</span><span>400</span></span>)<sup>4t</sup></td></tr></table></div><div class=\"ex\"><div class=\"exh\">Book Example 12 · ₹3000 for {1 1/2} years at 8% compounded semi-annually</div><div class=\"exl\">Three half-years, 4% each.<br>Interest ₹120 → ₹3120; interest ₹124.80 → ₹3244.80; interest ₹129.792 → ₹3374.592.<br>CI = ₹3374.592 − ₹3000 = <b>₹374.59</b> to the nearest paisa (the book rounds the last interest to ₹129.80 and gets ₹374.60).</div></div><div class=\"ex\"><div class=\"exh\">Book Example 14 · ₹5000 at 12% for {1 1/2} years, semi-annually</div><div class=\"exl\">Rate 6% per half-year, 3 periods: A = 5000 × ({106/100})<sup>3</sup> = ₹5955.08.<br>CI = <b>₹955.08</b>.</div></div><div class=\"keybox\"><b>Count periods, not years:</b> 9 months compounded quarterly = 3 periods; {1 1/2} years compounded half-yearly = 3 periods.</div><div class=\"hub-btns\" style=\"margin-top:12px\"><button class=\"hub-btn primary\" data-go=\"s5\">Practise 11.5 →</button></div></section><section class=\"note\" id=\"n116\"><h2>11.6 Finding time, principal and rate</h2><p class=\"lt\"><b>Objective:</b> Use the compound interest formula backwards to find the time, the principal or the rate, and link CI with SI on the same sum.</p><p>Put the known values into A = P(1 + <span class=\"fq\"><span>R</span><span>100</span></span>)<sup>t</sup> and work backwards.</p><ul><li><b>Time:</b> write A ÷ P as a power of (1 + R/100) and compare exponents.</li><li><b>Principal:</b> divide the amount by (1 + R/100)<sup>t</sup>.</li><li><b>Rate:</b> find (1 + R/100) as the t-th root of A ÷ P.</li></ul><div class=\"ex\"><div class=\"exh\">Book Example 15 · Time</div><div class=\"exl\">5324 = 4000 × ({11/10})<sup>t</sup> ⇒ {5324/4000} = {1331/1000} = ({11/10})<sup>3</sup>.<br>So <b>t = 3 years</b>.</div></div><div class=\"ex\"><div class=\"exh\">Book Example 17 · Rate</div><div class=\"exl\">{1800/1250} = {36/25} = ({6/5})<sup>2</sup> = (1 + R/100)<sup>2</sup>.<br>1 + R/100 = {6/5} ⇒ R/100 = {1/5} ⇒ <b>R = 20%</b>.</div></div><div class=\"ex\"><div class=\"exh\">Book Example 18 · CI given, SI wanted</div><div class=\"exl\">On ₹100 at 10% for 3 years, CI = ₹133.10 − ₹100 = ₹33.10.<br>CI ₹264.80 ⇒ P = 100 × 264.80 ÷ 33.10 = ₹800; SI = 800 × 3 × 10 ÷ 100 = <b>₹240</b>.</div></div><div class=\"keybox\"><b>Useful pattern:</b> for 2 years, CI − SI = P × (R/100)<sup>2</sup>. For ₹100 at 20%, the difference is ₹4.</div><div class=\"hub-btns\" style=\"margin-top:12px\"><button class=\"hub-btn primary\" data-go=\"s6\">Practise 11.6 →</button></div></section><section class=\"note\" id=\"n117\"><h2>11.7 Growth, appreciation and depreciation</h2><p class=\"lt\"><b>Objective:</b> Apply the compound interest formula to population growth and decay, and to the appreciation and depreciation of prices.</p><p>The CI formula works for anything that grows or decreases at a constant rate per year: population, prices of land (<b>appreciation</b>), values of cars and machines (<b>depreciation</b>).</p><div class=\"tscroll\"><table class=\"ttab\"><tr><th>Situation</th><th>Formula</th></tr><tr><td>Growth / appreciation at R% p.a.</td><td>A = P(1 + <span class=\"fq\"><span>R</span><span>100</span></span>)<sup>t</sup></td></tr><tr><td>Decay / depreciation at R% p.a.</td><td>A = P(1 − <span class=\"fq\"><span>R</span><span>100</span></span>)<sup>t</sup></td></tr><tr><td>Different rates R%, Q% each year</td><td>A = P(1 + <span class=\"fq\"><span>R</span><span>100</span></span>)(1 + <span class=\"fq\"><span>Q</span><span>100</span></span>)</td></tr></table></div><div class=\"ex\"><div class=\"exh\">Book Example 19 · Population</div><div class=\"exl\">3,20,000 × {105/100} × {105/100} = <b>3,52,800</b>.</div></div><div class=\"ex\"><div class=\"exh\">Book Example 23 · Depreciation</div><div class=\"exl\">TV ₹22,000 depreciating at 20%: 22000 × {80/100} × {80/100} = <b>₹14,080</b>.</div></div><div class=\"ex\"><div class=\"exh\">Book Example 25 · Going back in time</div><div class=\"exl\">Price now ₹14,400 after 20% appreciation for 2 years.<br>₹100 two years ago → ₹144 now, so the price two years ago = 14400 × 100 ÷ 144 = <b>₹10,000</b>.</div></div><div class=\"keybox\"><b>Shortcut (rule of 70):</b> the time to double at R% is about 70 ÷ R years: at 10% about 7 years, at 5% about 14 years. For depreciation, 70 ÷ R gives the time to halve.</div><div class=\"hub-btns\" style=\"margin-top:12px\"><button class=\"hub-btn primary\" data-go=\"s7\">Practise 11.7 →</button></div></section><section class=\"note\" id=\"nsum\"><h2>Chapter checklist</h2><ul><li>Recall principal, rate, time, interest and amount, and find the simple interest and the amount using SI = PRT/100 and A = P + SI.</li><li>Rearrange the simple interest formula to find the principal, the rate or the time, including times given in days and months.</li><li>Understand compound interest as interest on successive amounts, find it year by year and compare it with simple interest.</li><li>Use A = P(1 + R/100)<sup>t</sup> and CI = A − P for interest compounded annually.</li><li>Find compound interest when the conversion period is a half-year or a quarter, by halving or quartering the rate and multiplying the number of periods.</li><li>Use the compound interest formula backwards to find the time, the principal or the rate, and link CI with SI on the same sum.</li><li>Apply the compound interest formula to population growth and decay, and to the appreciation and depreciation of prices.</li></ul><div class=\"hub-btns\" style=\"margin-top:10px\"><button class=\"hub-btn\" data-go=\"s8\">Assessment A</button><button class=\"hub-btn\" data-go=\"s9\">Assessment B</button><button class=\"hub-btn\" data-go=\"s10\">Assessment C</button><button class=\"hub-btn\" data-go=\"s11\">Assessment D</button><button class=\"hub-btn primary\" data-go=\"report\">📊 Report</button></div></section>";
var REPORT = [["s8", "A", "Knowing and understanding"], ["s9", "B", "Investigating patterns"], ["s10", "C", "Communicating"], ["s11", "D", "Applying mathematics in real-life contexts"]];
var SECTIONS = [{"id": "s1", "label": "11.1 Simple interest", "sub": "Simple interest and amount", "slides": [{"kind": "blank", "p": "<b>Looking Back · Q1</b> · Find the simple interest on ₹4300 at 6% p.a. for 3 years.", "tag": "", "marks": "", "flat": [{"t": "SI = ₹__B1__", "a": {"B1": "774"}, "accept": ["774", "774.00", "inr774", "inr774.00", "rs.774", "rs.774.00", "rs774", "rs774.00", "₹774", "₹774.00"]}], "sol": "SI = P × R × T ÷ 100 = 4300 × 6 × 3 ÷ 100 = ₹774."}, {"kind": "mcq", "text": "<b>Looking Back · Q2</b> · ₹8000 is borrowed at 4% p.a. for 3 years. Find the interest and the amount at the end of 3 years.", "opts": ["Interest ₹960, amount ₹7040", "Interest ₹320, amount ₹8320", "Interest ₹96, amount ₹8096", "Interest ₹960, amount ₹8960"], "correct": 3, "tag": "", "sol": "SI = 8000 × 4 × 3 ÷ 100 = ₹960. Amount = ₹8000 + ₹960 = ₹8960."}, {"kind": "blank", "p": "<b>Example 1</b> · Find the principal, amount and interest in the following.", "tag": "", "marks": "", "flat": [{"t": "a) P = ₹5250, A = ₹6005: I = ₹__B1__", "a": {"B1": "755"}, "accept": ["755", "755.00", "inr755", "inr755.00", "rs.755", "rs.755.00", "rs755", "rs755.00", "₹755", "₹755.00"]}, {"t": "b) P = ₹7350, I = ₹750: A = ₹__B1__", "a": {"B1": "8100"}, "accept": ["8,100", "8,100.00", "8100", "8100.00", "inr8,100", "inr8,100.00", "inr8100", "inr8100.00", "rs.8,100", "rs.8,100.00", "rs.8100", "rs.8100.00", "rs8,100", "rs8,100.00", "rs8100", "rs8100.00", "₹8,100", "₹8,100.00", "₹8100", "₹8100.00"]}, {"t": "c) A = ₹9125, I = ₹625: P = ₹__B1__", "a": {"B1": "8500"}, "accept": ["8,500", "8,500.00", "8500", "8500.00", "inr8,500", "inr8,500.00", "inr8500", "inr8500.00", "rs.8,500", "rs.8,500.00", "rs.8500", "rs.8500.00", "rs8,500", "rs8,500.00", "rs8500", "rs8500.00", "₹8,500", "₹8,500.00", "₹8500", "₹8500.00"]}], "sol": "I = A − P = ₹6005 − ₹5250 = ₹755.\nA = P + I = ₹7350 + ₹750 = ₹8100.\nP = A − I = ₹9125 − ₹625 = ₹8500."}, {"kind": "blank", "p": "<b>Example 2</b> · Sarosh borrowed ₹7000 from the bank at 7% interest per annum for 3 years. Find the simple interest and the amount he had to pay.", "tag": "", "marks": "", "flat": [{"t": "SI = ₹__B1__", "a": {"B1": "1470"}, "accept": ["1,470", "1,470.00", "1470", "1470.00", "inr1,470", "inr1,470.00", "inr1470", "inr1470.00", "rs.1,470", "rs.1,470.00", "rs.1470", "rs.1470.00", "rs1,470", "rs1,470.00", "rs1470", "rs1470.00", "₹1,470", "₹1,470.00", "₹1470", "₹1470.00"]}, {"t": "Amount = ₹__B1__", "a": {"B1": "8470"}, "accept": ["8,470", "8,470.00", "8470", "8470.00", "inr8,470", "inr8,470.00", "inr8470", "inr8470.00", "rs.8,470", "rs.8,470.00", "rs.8470", "rs.8470.00", "rs8,470", "rs8,470.00", "rs8470", "rs8470.00", "₹8,470", "₹8,470.00", "₹8470", "₹8470.00"]}], "sol": "SI = 7000 × 3 × 7 ÷ 100 = ₹1470.\nAmount = ₹7000 + ₹1470 = ₹8470."}, {"kind": "mcq", "text": "<b>Example 3</b> · Find the simple interest and amount for ₹600 borrowed at a rate of {7 1/2}% per annum for 1 year 8 months.", "opts": ["SI ₹75, amount ₹675", "SI ₹90, amount ₹690", "SI ₹81, amount ₹681", "SI ₹45, amount ₹645"], "correct": 0, "tag": "", "sol": "R = {15/2}%, T = 1 year 8 months = {20/12} years. SI = 600 × {20/12} × {15/2} ÷ 100 = ₹75. Amount = ₹600 + ₹75 = ₹675. (₹90 uses T = 2 years; ₹45 uses T = 1 year; ₹81 uses T = 1.8 years.)"}, {"kind": "blank", "p": "<b>Example 7</b> · Farhan deposits ₹6000 in a bank at the rate of 6% per annum for 3 years at simple interest. Find the amount he will get back at the end of this period, using A = P(1 + RT/100).", "tag": "", "marks": "", "flat": [{"t": "1 + RT ÷ 100 = 1 + {18/100} = {x/100}: x = __B1__", "a": {"B1": "118"}, "expr": "fv"}, {"t": "Amount = ₹__B1__", "a": {"B1": "7080"}, "accept": ["7,080", "7,080.00", "7080", "7080.00", "inr7,080", "inr7,080.00", "inr7080", "inr7080.00", "rs.7,080", "rs.7,080.00", "rs.7080", "rs.7080.00", "rs7,080", "rs7,080.00", "rs7080", "rs7080.00", "₹7,080", "₹7,080.00", "₹7080", "₹7080.00"]}], "sol": "RT = 6 × 3 = 18, so 1 + {18/100} = {118/100}.\nA = 6000 × {118/100} = ₹7080."}, {"kind": "mcq", "text": "<b>Try This (p. 136) · a, b</b> · Find the missing value.  a) P = ₹7500, T = 2 years, R = 8% p.a., SI = ?   b) A = ₹13,000, I = ₹700, P = ?", "opts": ["a) ₹1200  b) ₹13,700", "a) ₹1200  b) ₹12,300", "a) ₹600  b) ₹12,300", "a) ₹120  b) ₹13,700"], "correct": 1, "tag": "", "sol": "a) SI = 7500 × 8 × 2 ÷ 100 = ₹1200. b) P = A − I = ₹13,000 − ₹700 = ₹12,300."}, {"kind": "blank", "p": "<b>Ex 11A · Q1(a–c)</b> · Find the missing figures.\na) Principal ₹3520, Interest ₹250, Amount ?\nb) Principal ₹5780, Interest ?, Amount ₹6240\nc) Principal ₹850, Interest ?, Amount ₹972", "tag": "", "marks": "", "flat": [{"t": "a) Amount = ₹__B1__", "a": {"B1": "3770"}, "accept": ["3,770", "3,770.00", "3770", "3770.00", "inr3,770", "inr3,770.00", "inr3770", "inr3770.00", "rs.3,770", "rs.3,770.00", "rs.3770", "rs.3770.00", "rs3,770", "rs3,770.00", "rs3770", "rs3770.00", "₹3,770", "₹3,770.00", "₹3770", "₹3770.00"]}, {"t": "b) Interest = ₹__B1__", "a": {"B1": "460"}, "accept": ["460", "460.00", "inr460", "inr460.00", "rs.460", "rs.460.00", "rs460", "rs460.00", "₹460", "₹460.00"]}, {"t": "c) Interest = ₹__B1__", "a": {"B1": "122"}, "accept": ["122", "122.00", "inr122", "inr122.00", "rs.122", "rs.122.00", "rs122", "rs122.00", "₹122", "₹122.00"]}], "sol": "A = P + I = 3520 + 250 = ₹3770.\nI = A − P = 6240 − 5780 = ₹460.\nI = 972 − 850 = ₹122."}, {"kind": "blank", "p": "<b>Ex 11A · Q1(d–f)</b> · Find the missing figures.\nd) Principal ₹9450, Interest ₹550, Amount ?\ne) Principal ?, Interest ₹72, Amount ₹672\nf) Principal ?, Interest ₹1233, Amount ₹7288", "tag": "", "marks": "", "flat": [{"t": "d) Amount = ₹__B1__", "a": {"B1": "10000"}, "accept": ["10,000", "10,000.00", "10000", "10000.00", "inr10,000", "inr10,000.00", "inr10000", "inr10000.00", "rs.10,000", "rs.10,000.00", "rs.10000", "rs.10000.00", "rs10,000", "rs10,000.00", "rs10000", "rs10000.00", "₹10,000", "₹10,000.00", "₹10000", "₹10000.00"]}, {"t": "e) Principal = ₹__B1__", "a": {"B1": "600"}, "accept": ["600", "600.00", "inr600", "inr600.00", "rs.600", "rs.600.00", "rs600", "rs600.00", "₹600", "₹600.00"]}, {"t": "f) Principal = ₹__B1__", "a": {"B1": "6055"}, "accept": ["6,055", "6,055.00", "6055", "6055.00", "inr6,055", "inr6,055.00", "inr6055", "inr6055.00", "rs.6,055", "rs.6,055.00", "rs.6055", "rs.6055.00", "rs6,055", "rs6,055.00", "rs6055", "rs6055.00", "₹6,055", "₹6,055.00", "₹6055", "₹6055.00"]}], "sol": "A = 9450 + 550 = ₹10,000.\nP = A − I = 672 − 72 = ₹600.\nP = 7288 − 1233 = ₹6055."}, {"kind": "mcq", "text": "<b>Ex 11A · Q2(a)</b> · Find the simple interest and the amount: principal ₹8500, rate 8.5% p.a., time 1 year.", "opts": ["SI ₹722.50, amount ₹7777.50", "SI ₹7225, amount ₹15,725", "SI ₹72.25, amount ₹8572.25", "SI ₹722.50, amount ₹9222.50"], "correct": 3, "tag": "", "sol": "SI = 8500 × 8.5 × 1 ÷ 100 = ₹722.50. Amount = ₹8500 + ₹722.50 = ₹9222.50."}, {"kind": "blank", "p": "<b>Ex 11A · Q2(b, c)</b> · Find the simple interest and the amount.\nb) Principal ₹4750, rate {12 1/2}% p.a., time 2 years\nc) Principal ₹160, rate 10% p.a., time {1/2} year", "tag": "", "marks": "", "flat": [{"t": "b) SI = ₹__B1__", "a": {"B1": "1187.50"}, "accept": ["1,187.5", "1,187.50", "1187.5", "1187.50", "inr1,187.5", "inr1,187.50", "inr1187.5", "inr1187.50", "rs.1,187.5", "rs.1,187.50", "rs.1187.5", "rs.1187.50", "rs1,187.5", "rs1,187.50", "rs1187.5", "rs1187.50", "₹1,187.5", "₹1,187.50", "₹1187.5", "₹1187.50"]}, {"t": "b) Amount = ₹__B1__", "a": {"B1": "5937.50"}, "accept": ["5,937.5", "5,937.50", "5937.5", "5937.50", "inr5,937.5", "inr5,937.50", "inr5937.5", "inr5937.50", "rs.5,937.5", "rs.5,937.50", "rs.5937.5", "rs.5937.50", "rs5,937.5", "rs5,937.50", "rs5937.5", "rs5937.50", "₹5,937.5", "₹5,937.50", "₹5937.5", "₹5937.50"]}, {"t": "c) SI = ₹__B1__", "a": {"B1": "8"}, "accept": ["8", "8.00", "inr8", "inr8.00", "rs.8", "rs.8.00", "rs8", "rs8.00", "₹8", "₹8.00"]}, {"t": "c) Amount = ₹__B1__", "a": {"B1": "168"}, "accept": ["168", "168.00", "inr168", "inr168.00", "rs.168", "rs.168.00", "rs168", "rs168.00", "₹168", "₹168.00"]}], "sol": "SI = 4750 × {25/2} × 2 ÷ 100 = ₹1187.50.\nA = 4750 + 1187.50 = ₹5937.50.\nSI = 160 × 10 × {1/2} ÷ 100 = ₹8.\nA = 160 + 8 = ₹168."}, {"kind": "blank", "p": "<b>Ex 11A · Q2(d, e)</b> · Find the simple interest and the amount.\nd) Principal ₹800, rate 3.5% p.a., time 4 years\ne) Principal ₹9600, rate 8% p.a., time 3 months", "tag": "", "marks": "", "flat": [{"t": "d) SI = ₹__B1__", "a": {"B1": "112"}, "accept": ["112", "112.00", "inr112", "inr112.00", "rs.112", "rs.112.00", "rs112", "rs112.00", "₹112", "₹112.00"]}, {"t": "d) Amount = ₹__B1__", "a": {"B1": "912"}, "accept": ["912", "912.00", "inr912", "inr912.00", "rs.912", "rs.912.00", "rs912", "rs912.00", "₹912", "₹912.00"]}, {"t": "e) SI = ₹__B1__", "a": {"B1": "192"}, "accept": ["192", "192.00", "inr192", "inr192.00", "rs.192", "rs.192.00", "rs192", "rs192.00", "₹192", "₹192.00"]}, {"t": "e) Amount = ₹__B1__", "a": {"B1": "9792"}, "accept": ["9,792", "9,792.00", "9792", "9792.00", "inr9,792", "inr9,792.00", "inr9792", "inr9792.00", "rs.9,792", "rs.9,792.00", "rs.9792", "rs.9792.00", "rs9,792", "rs9,792.00", "rs9792", "rs9792.00", "₹9,792", "₹9,792.00", "₹9792", "₹9792.00"]}], "sol": "SI = 800 × 3.5 × 4 ÷ 100 = ₹112.\nA = 800 + 112 = ₹912.\n3 months = {3/12} = {1/4} year: SI = 9600 × 8 × {1/4} ÷ 100 = ₹192.\nA = 9600 + 192 = ₹9792."}, {"kind": "mcq", "text": "<b>Ex 11A · Q6</b> · Susan deposited ₹8000 in a bank at the rate of 12 per cent per annum. She withdrew the money after 9 months. What is the simple interest she got? What was the amount she collected from the bank?", "opts": ["SI ₹864, amount ₹8864", "SI ₹720, amount ₹8720", "SI ₹8640, amount ₹16,640", "SI ₹960, amount ₹8960"], "correct": 1, "tag": "", "sol": "9 months = {9/12} = {3/4} year. SI = 8000 × 12 × {3/4} ÷ 100 = ₹720. Amount = ₹8000 + ₹720 = ₹8720. (₹8640 takes the time as 9 years, ₹960 as 1 year and ₹864 as 0.9 year.)"}, {"kind": "blank", "p": "<b>Ex 11A · Q13(a, b)</b> · Find the amount directly using the formula A = P(1 + RT/100).\na) Principal ₹5000, rate 10%, time 3 years\nb) Principal ₹450, rate 7%, time 5 years", "tag": "", "marks": "", "flat": [{"t": "a) A = ₹__B1__", "a": {"B1": "6500"}, "accept": ["6,500", "6,500.00", "6500", "6500.00", "inr6,500", "inr6,500.00", "inr6500", "inr6500.00", "rs.6,500", "rs.6,500.00", "rs.6500", "rs.6500.00", "rs6,500", "rs6,500.00", "rs6500", "rs6500.00", "₹6,500", "₹6,500.00", "₹6500", "₹6500.00"]}, {"t": "b) A = ₹__B1__", "a": {"B1": "607.50"}, "accept": ["607.5", "607.50", "inr607.5", "inr607.50", "rs.607.5", "rs.607.50", "rs607.5", "rs607.50", "₹607.5", "₹607.50"]}], "sol": "A = 5000 × (1 + {30/100}) = 5000 × {130/100} = ₹6500.\nA = 450 × (1 + {35/100}) = 450 × {135/100} = ₹607.50."}, {"kind": "mcq", "text": "<b>Ex 11A · Q13(c, d)</b> · Find the amount directly using A = P(1 + RT/100).  c) ₹3200 at 7.5% for 2 years   d) ₹720 at 8.5% for 3 years", "opts": ["c) ₹3680  d) ₹903.60", "c) ₹3680  d) ₹781.20", "c) ₹4800  d) ₹903.60", "c) ₹3440  d) ₹903.60"], "correct": 0, "tag": "", "sol": "c) RT = 7.5 × 2 = 15: A = 3200 × {115/100} = ₹3680. d) RT = 8.5 × 3 = 25.5: A = 720 × 125.5 ÷ 100 = ₹903.60."}]}, {"id": "s2", "label": "11.2 P, R and T", "sub": "Finding the principal, rate and time for simple interest", "slides": [{"kind": "blank", "p": "<b>Looking Back · Q3</b> · Find the principal if the interest is ₹2880 at 8% p.a. for 3 years.", "tag": "", "marks": "", "flat": [{"t": "P = ₹__B1__", "a": {"B1": "12000"}, "accept": ["12,000", "12,000.00", "12000", "12000.00", "inr12,000", "inr12,000.00", "inr12000", "inr12000.00", "rs.12,000", "rs.12,000.00", "rs.12000", "rs.12000.00", "rs12,000", "rs12,000.00", "rs12000", "rs12000.00", "₹12,000", "₹12,000.00", "₹12000", "₹12000.00"]}], "sol": "P = SI × 100 ÷ (R × T) = 2880 × 100 ÷ (8 × 3) = ₹12,000."}, {"kind": "mcq", "text": "<b>Looking Back · Q4</b> · Find the time in which ₹2700 will yield an interest of ₹324 at a rate of interest 4% p.a.", "opts": ["{1/3} year", "3 years", "2 years", "4 years"], "correct": 1, "tag": "", "sol": "T = SI × 100 ÷ (P × R) = 324 × 100 ÷ (2700 × 4) = 32400 ÷ 10800 = 3 years."}, {"kind": "blank", "p": "<b>Looking Back · Q5</b> · Find the rate of interest if the interest on ₹2200 for 3 years is ₹330.", "tag": "", "marks": "", "flat": [{"t": "R = __B1__ % p.a.", "a": {"B1": "5"}, "accept": ["5%", "5% p.a.", "5%p.a"]}], "sol": "R = SI × 100 ÷ (P × T) = 33000 ÷ 6600 = 5% p.a."}, {"kind": "blank", "p": "<b>Example 4</b> · Amit borrowed a sum of money from Hamid at {6 1/4}% p.a. for 146 days. If the simple interest paid is ₹30, how much money was borrowed by Amit?", "tag": "", "marks": "", "flat": [{"t": "Time = 146 days = __B1__ year (simplest form)", "a": {"B1": "2/5"}, "expr": "fl"}, {"t": "Principal = ₹__B1__", "a": {"B1": "1200"}, "accept": ["1,200", "1,200.00", "1200", "1200.00", "inr1,200", "inr1,200.00", "inr1200", "inr1200.00", "rs.1,200", "rs.1,200.00", "rs.1200", "rs.1200.00", "rs1,200", "rs1,200.00", "rs1200", "rs1200.00", "₹1,200", "₹1,200.00", "₹1200", "₹1200.00"]}], "sol": "146 days = {146/365} = {2/5} year.\nP = SI × 100 ÷ (R × T) = 30 × 100 × 4 × 365 ÷ (25 × 146) = ₹1200."}, {"kind": "mcq", "text": "<b>Example 5</b> · Sonia borrowed ₹15,000 from Friends’ Co-operative Bank and returned an amount of ₹15,315 with interest after 219 days. Find the simple interest paid and the rate of interest per annum.", "opts": ["SI ₹30,315, rate 3.5% p.a.", "SI ₹315, rate 7% p.a.", "SI ₹315, rate 2.1% p.a.", "SI ₹315, rate 3.5% p.a."], "correct": 3, "tag": "", "sol": "SI = ₹15,315 − ₹15,000 = ₹315. T = 219 days = {219/365} = {3/5} year. R = 315 × 100 × 5 ÷ (15000 × 3) = {7/2} = 3.5% p.a. (2.1% takes the time as 1 year instead of {3/5} year; 7% uses T = {3/10} year.)"}, {"kind": "blank", "p": "<b>Example 6</b> · Mala gave Rajiv ₹9000 at the rate of 5% per annum and received ₹90 as interest. For how long was Mala’s money kept with Rajiv?", "tag": "", "marks": "", "flat": [{"t": "Time = __B1__ year", "a": {"B1": "1/5"}, "expr": "fv"}, {"t": "= __B1__ days", "a": {"B1": "73"}, "accept": ["73 days"]}], "sol": "T = SI × 100 ÷ (P × R) = 90 × 100 ÷ (9000 × 5) = {1/5} year.\n{1/5} × 365 = 73 days."}, {"kind": "blank", "p": "<b>Example 8</b> · In how much time will the simple interest on ₹3500 at the rate of 9% per annum be the same as simple interest on ₹4000 at 10.5% per annum for 4 years?", "tag": "", "marks": "", "flat": [{"t": "SI on ₹4000 at 10.5% for 4 years = ₹__B1__", "a": {"B1": "1680"}, "accept": ["1,680", "1,680.00", "1680", "1680.00", "inr1,680", "inr1,680.00", "inr1680", "inr1680.00", "rs.1,680", "rs.1,680.00", "rs.1680", "rs.1680.00", "rs1,680", "rs1,680.00", "rs1680", "rs1680.00", "₹1,680", "₹1,680.00", "₹1680", "₹1680.00"]}, {"t": "t = __B1__ years (fraction or mixed number)", "a": {"B1": "16/3"}, "expr": "fv"}], "sol": "SI = 4000 × 10.5 × 4 ÷ 100 = ₹1680.\nt = 1680 × 100 ÷ (3500 × 9) = {16/3} = {5 1/3} years."}, {"kind": "mcq", "text": "<b>Example 9</b> · A sum of money invested at a certain rate doubles itself in 10 years. How much time will it take to triple itself at the same rate?", "opts": ["20 years", "25 years", "15 years", "30 years"], "correct": 0, "tag": "", "sol": "Let P = ₹100; doubling gives SI = ₹100 in 10 years, so R = 100 × 100 ÷ (100 × 10) = 10%. Tripling needs SI = ₹200: T = 100 × 200 ÷ (100 × 10) = 20 years."}, {"kind": "blank", "p": "<b>Try This (p. 136) · c</b> · Find the missing value: P = ₹10,000, R = 5% p.a., SI = ₹2000, T = ?", "tag": "", "marks": "", "flat": [{"t": "T = __B1__ years", "a": {"B1": "4"}, "accept": ["4 years", "4 year", "4 yrs", "4 yr"]}], "sol": "T = SI × 100 ÷ (P × R) = 200000 ÷ 50000 = 4 years."}, {"kind": "blank", "p": "<b>Ex 11A · Q3</b> · Find the principal.\na) SI ₹57, time 3 years, rate 5% p.a.\nb) SI ₹1904, time 5 years, rate 7% p.a.\nc) SI ₹60, time 73 days, rate 4% p.a.", "tag": "", "marks": "", "flat": [{"t": "a) P = ₹__B1__", "a": {"B1": "380"}, "accept": ["380", "380.00", "inr380", "inr380.00", "rs.380", "rs.380.00", "rs380", "rs380.00", "₹380", "₹380.00"]}, {"t": "b) P = ₹__B1__", "a": {"B1": "5440"}, "accept": ["5,440", "5,440.00", "5440", "5440.00", "inr5,440", "inr5,440.00", "inr5440", "inr5440.00", "rs.5,440", "rs.5,440.00", "rs.5440", "rs.5440.00", "rs5,440", "rs5,440.00", "rs5440", "rs5440.00", "₹5,440", "₹5,440.00", "₹5440", "₹5440.00"]}, {"t": "c) P = ₹__B1__", "a": {"B1": "7500"}, "accept": ["7,500", "7,500.00", "7500", "7500.00", "inr7,500", "inr7,500.00", "inr7500", "inr7500.00", "rs.7,500", "rs.7,500.00", "rs.7500", "rs.7500.00", "rs7,500", "rs7,500.00", "rs7500", "rs7500.00", "₹7,500", "₹7,500.00", "₹7500", "₹7500.00"]}], "sol": "P = 57 × 100 ÷ (5 × 3) = ₹380.\nP = 1904 × 100 ÷ (7 × 5) = ₹5440.\n73 days = {1/5} year: P = 60 × 100 ÷ (4 × {1/5}) = 6000 × 5 ÷ 4 = ₹7500."}, {"kind": "mcq", "text": "<b>Ex 11A · Q4(a)</b> · Find the SI and the interest rate: principal ₹20,000, amount ₹21,800, time 2 years.", "opts": ["SI ₹1800, rate 4.5% p.a.", "SI ₹1800, rate 9% p.a.", "SI ₹1800, rate 4% p.a.", "SI ₹41,800, rate 4.5% p.a."], "correct": 0, "tag": "", "sol": "SI = ₹21,800 − ₹20,000 = ₹1800. R = 1800 × 100 ÷ (20000 × 2) = 4.5% p.a."}, {"kind": "blank", "p": "<b>Ex 11A · Q4(b, c)</b> · Find the SI and the interest rate.\nb) Principal ₹7500, amount ₹8325, time 2 years\nc) Principal ₹625, amount ₹641.25, time 146 days", "tag": "", "marks": "", "flat": [{"t": "b) SI = ₹__B1__", "a": {"B1": "825"}, "accept": ["825", "825.00", "inr825", "inr825.00", "rs.825", "rs.825.00", "rs825", "rs825.00", "₹825", "₹825.00"]}, {"t": "b) Rate = __B1__ % p.a.", "a": {"B1": "5.5"}, "accept": ["5.5%", "5.5% p.a.", "5.5%p.a"]}, {"t": "c) SI = ₹__B1__", "a": {"B1": "16.25"}, "accept": ["16.25", "inr16.25", "rs.16.25", "rs16.25", "₹16.25"]}, {"t": "c) Rate = __B1__ % p.a.", "a": {"B1": "6.5"}, "accept": ["6.5%", "6.5% p.a.", "6.5%p.a"]}], "sol": "SI = 8325 − 7500 = ₹825.\nR = 825 × 100 ÷ (7500 × 2) = 5.5% p.a.\nSI = 641.25 − 625 = ₹16.25.\n146 days = {2/5} year: R = 16.25 × 100 ÷ (625 × {2/5}) = 1625 ÷ 250 = 6.5% p.a."}, {"kind": "blank", "p": "<b>Ex 11A · Q5</b> · Find the time (in years).\na) P ₹3500, SI ₹700, rate 5% p.a.\nb) P ₹4800, SI ₹900, rate 7.5% p.a.\nc) P ₹500, SI ₹31.25, rate 12.5% p.a.\nd) P ₹600, SI ₹12.60, rate 3.5% p.a.", "tag": "", "marks": "", "flat": [{"t": "a) T = __B1__ years", "a": {"B1": "4"}, "accept": ["4 years", "4 year", "4 yrs", "4 yr"]}, {"t": "b) T = __B1__ years", "a": {"B1": "5/2"}, "expr": "fv"}, {"t": "c) T = __B1__ year", "a": {"B1": "1/2"}, "expr": "fv"}, {"t": "d) T = __B1__ year", "a": {"B1": "3/5"}, "expr": "fv"}], "sol": "T = 700 × 100 ÷ (3500 × 5) = 4 years.\nT = 900 × 100 ÷ (4800 × 7.5) = 90000 ÷ 36000 = {5/2} = 2.5 years.\nT = 31.25 × 100 ÷ (500 × 12.5) = 3125 ÷ 6250 = {1/2} year.\nT = 12.60 × 100 ÷ (600 × 3.5) = 1260 ÷ 2100 = {3/5} year (= 0.6 year = 219 days)."}, {"kind": "mcq", "text": "<b>Ex 11A · Q7</b> · A borrowed amount of ₹4000 amounts to ₹5400 in 5 years. How much will ₹5600 amount to in 3 years at the same rate?", "opts": ["₹7560", "₹6776", "₹1176", "₹11,480"], "correct": 1, "tag": "", "sol": "SI = ₹5400 − ₹4000 = ₹1400, so R = 1400 × 100 ÷ (4000 × 5) = 7% p.a. On ₹5600 for 3 years: SI = 5600 × 7 × 3 ÷ 100 = ₹1176, amount = ₹5600 + ₹1176 = ₹6776. (₹1176 is only the interest; ₹7560 uses 5 years; ₹11,480 forgets to divide the rate by the 5 years, giving 35%.)"}, {"kind": "mcq", "text": "<b>Ex 11A · Q8</b> · Find the interest on a deposit of ₹3650 from 3 January 2020 at the rate of 10% p.a. up to 17 March 2020.", "opts": ["₹73", "₹75", "₹73.80", "₹74"], "correct": 3, "tag": "", "sol": "Count the days (leave out the day of deposit): January 28 (4 to 31), February 29 (2020 is a leap year), March 17: 28 + 29 + 17 = 74 days = {74/365} year. SI = 3650 × 10 × 74 ÷ (100 × 365) = ₹74. (₹73 forgets that February 2020 had 29 days.)"}, {"kind": "blank", "p": "<b>Ex 11A · Q9</b> · Sanju borrowed a sum of money from Simran at 8% interest per annum. After 4 years, Sanju had to give Simran ₹9900 to clear the debt. What was the amount Sanju borrowed originally?", "tag": "", "marks": "", "flat": [{"t": "Interest on ₹100 for 4 years = ₹__B1__", "a": {"B1": "32"}, "accept": ["₹32", "rs32"]}, {"t": "Amount borrowed = ₹__B1__", "a": {"B1": "7500"}, "accept": ["7,500", "7,500.00", "7500", "7500.00", "inr7,500", "inr7,500.00", "inr7500", "inr7500.00", "rs.7,500", "rs.7,500.00", "rs.7500", "rs.7500.00", "rs7,500", "rs7,500.00", "rs7500", "rs7500.00", "₹7,500", "₹7,500.00", "₹7500", "₹7500.00"]}], "sol": "On ₹100: SI = 100 × 8 × 4 ÷ 100 = ₹32, so ₹100 becomes ₹132.\nP = 9900 × 100 ÷ 132 = ₹7500."}, {"kind": "blank", "p": "<b>Ex 11A · Q10</b> · Rajinder lent a sum of ₹3200 to Suresh at the rate of 6% interest per annum. Suresh paid Rajinder ₹3680 to clear the debt. How long did Suresh use Rajinder’s money?", "tag": "", "marks": "", "flat": [{"t": "SI = ₹__B1__", "a": {"B1": "480"}, "accept": ["480", "480.00", "inr480", "inr480.00", "rs.480", "rs.480.00", "rs480", "rs480.00", "₹480", "₹480.00"]}, {"t": "Time = __B1__ years", "a": {"B1": "5/2"}, "expr": "fv"}], "sol": "SI = 3680 − 3200 = ₹480.\nT = 480 × 100 ÷ (3200 × 6) = {5/2} = {2 1/2} years."}, {"kind": "mcq", "text": "<b>Ex 11A · Q11</b> · Alok paid ₹6720 to clear a debt of ₹6000 to the bank after 1 year 6 months. What is the rate of interest charged by the bank?", "opts": ["6% p.a.", "8% p.a.", "7.2% p.a.", "12% p.a."], "correct": 1, "tag": "", "sol": "SI = ₹6720 − ₹6000 = ₹720; T = {3/2} years. R = 720 × 100 ÷ (6000 × {3/2}) = 72000 ÷ 9000 = 8% p.a."}, {"kind": "blank", "p": "<b>Ex 11A · Q12</b> · A certain amount of money amounts to ₹4400 in two years and to ₹4600 in three years. Find the principal and rate of interest. (Hint: one year’s interest is 4600 − 4400 = ₹200.)", "tag": "", "marks": "", "flat": [{"t": "Principal = ₹__B1__", "a": {"B1": "4000"}, "accept": ["4,000", "4,000.00", "4000", "4000.00", "inr4,000", "inr4,000.00", "inr4000", "inr4000.00", "rs.4,000", "rs.4,000.00", "rs.4000", "rs.4000.00", "rs4,000", "rs4,000.00", "rs4000", "rs4000.00", "₹4,000", "₹4,000.00", "₹4000", "₹4000.00"]}, {"t": "Rate = __B1__ % p.a.", "a": {"B1": "5"}, "accept": ["5%", "5% p.a.", "5%p.a"]}], "sol": "Interest for 2 years = 2 × 200 = ₹400, so P = 4400 − 400 = ₹4000.\nR = 200 × 100 ÷ (4000 × 1) = 5% p.a."}]}, {"id": "s3", "label": "11.3 CI year by year", "sub": "Compound interest calculated year by year", "slides": [{"kind": "blank", "p": "<b>Compound Interest (p. 138)</b> · Abu invested ₹8000 at 10% p.a. simple interest for 3 years. Ali invested ₹8000 at 10% p.a., but at the end of each year the interest was added to the principal.", "tag": "", "marks": "", "flat": [{"t": "Abu’s simple interest for 3 years = ₹__B1__", "a": {"B1": "2400"}, "accept": ["2,400", "2,400.00", "2400", "2400.00", "inr2,400", "inr2,400.00", "inr2400", "inr2400.00", "rs.2,400", "rs.2,400.00", "rs.2400", "rs.2400.00", "rs2,400", "rs2,400.00", "rs2400", "rs2400.00", "₹2,400", "₹2,400.00", "₹2400", "₹2400.00"]}, {"t": "Ali’s amount after 3 years = ₹__B1__", "a": {"B1": "10648"}, "accept": ["10,648", "10,648.00", "10648", "10648.00", "inr10,648", "inr10,648.00", "inr10648", "inr10648.00", "rs.10,648", "rs.10,648.00", "rs.10648", "rs.10648.00", "rs10,648", "rs10,648.00", "rs10648", "rs10648.00", "₹10,648", "₹10,648.00", "₹10648", "₹10648.00"]}, {"t": "Ali gets more interest than Abu by ₹__B1__", "a": {"B1": "248"}, "accept": ["248", "248.00", "inr248", "inr248.00", "rs.248", "rs.248.00", "rs248", "rs248.00", "₹248", "₹248.00"]}], "sol": "SI = 8000 × 10 × 3 ÷ 100 = ₹2400 (amount ₹10,400).\n8000 → 8800 → 9680 → 9680 + 968 = ₹10,648.\nAli’s interest = ₹2648; 2648 − 2400 = ₹248."}, {"kind": "mcq", "text": "<b>Conversion Period (p. 139)</b> · A sum is lent at R% per annum and the interest is added to the principal every six months. What is the conversion period and the rate per conversion period? (If no conversion period is specified, what is it taken as?)", "opts": ["Half a year at R/2 % per half-year; otherwise one year", "Half a year at 2R% per half-year; otherwise one year", "Three months at R/4 % per quarter; otherwise one year", "One year at R% per year; otherwise half a year"], "correct": 0, "tag": "", "sol": "Adding interest every six months means the conversion period is half a year and the rate is R/2 % per half-year. When no conversion period is given, it is taken as one year."}, {"kind": "blank", "p": "<b>Example 10</b> · Find the compound interest on ₹3600 at 10% p.a. for 3 years, compounded annually (year by year).", "tag": "", "marks": "", "flat": [{"t": "Interest for year 1 = ₹__B1__", "a": {"B1": "360"}, "accept": ["360", "360.00", "inr360", "inr360.00", "rs.360", "rs.360.00", "rs360", "rs360.00", "₹360", "₹360.00"]}, {"t": "Interest for year 2 (on ₹3960) = ₹__B1__", "a": {"B1": "396"}, "accept": ["396", "396.00", "inr396", "inr396.00", "rs.396", "rs.396.00", "rs396", "rs396.00", "₹396", "₹396.00"]}, {"t": "Amount after 3 years = ₹__B1__", "a": {"B1": "4791.60"}, "accept": ["4,791.6", "4,791.60", "4791.6", "4791.60", "inr4,791.6", "inr4,791.60", "inr4791.6", "inr4791.60", "rs.4,791.6", "rs.4,791.60", "rs.4791.6", "rs.4791.60", "rs4,791.6", "rs4,791.60", "rs4791.6", "rs4791.60", "₹4,791.6", "₹4,791.60", "₹4791.6", "₹4791.60"]}, {"t": "CI = ₹__B1__", "a": {"B1": "1191.60"}, "accept": ["1,191.6", "1,191.60", "1191.6", "1191.60", "inr1,191.6", "inr1,191.60", "inr1191.6", "inr1191.60", "rs.1,191.6", "rs.1,191.60", "rs.1191.6", "rs.1191.60", "rs1,191.6", "rs1,191.60", "rs1191.6", "rs1191.60", "₹1,191.6", "₹1,191.60", "₹1191.6", "₹1191.60"]}], "sol": "3600 × 10 × 1 ÷ 100 = ₹360; amount ₹3960.\n3960 × 10 ÷ 100 = ₹396; amount ₹4356.\nInterest for year 3 = 4356 × 10 ÷ 100 = ₹435.60; amount = ₹4791.60. (Method 2: 3600 × {110/100} × {110/100} × {110/100} gives the same.)\nCI = A − P = 4791.60 − 3600 = ₹1191.60."}, {"kind": "blank", "p": "<b>Example 11</b> · Find the difference between CI and SI on ₹15,000 at 12% p.a. for 3 years (compounded annually).", "tag": "", "marks": "", "flat": [{"t": "SI = ₹__B1__", "a": {"B1": "5400"}, "accept": ["5,400", "5,400.00", "5400", "5400.00", "inr5,400", "inr5,400.00", "inr5400", "inr5400.00", "rs.5,400", "rs.5,400.00", "rs.5400", "rs.5400.00", "rs5,400", "rs5,400.00", "rs5400", "rs5400.00", "₹5,400", "₹5,400.00", "₹5400", "₹5400.00"]}, {"t": "Amount after 2 years = ₹__B1__", "a": {"B1": "18816"}, "accept": ["18,816", "18,816.00", "18816", "18816.00", "inr18,816", "inr18,816.00", "inr18816", "inr18816.00", "rs.18,816", "rs.18,816.00", "rs.18816", "rs.18816.00", "rs18,816", "rs18,816.00", "rs18816", "rs18816.00", "₹18,816", "₹18,816.00", "₹18816", "₹18816.00"]}, {"t": "CI = ₹__B1__", "a": {"B1": "6073.92"}, "accept": ["6,073.92", "6073.92", "inr6,073.92", "inr6073.92", "rs.6,073.92", "rs.6073.92", "rs6,073.92", "rs6073.92", "₹6,073.92", "₹6073.92"]}, {"t": "CI − SI = ₹__B1__", "a": {"B1": "673.92"}, "accept": ["673.92", "inr673.92", "rs.673.92", "rs673.92", "₹673.92"]}], "sol": "SI = 15000 × 3 × 12 ÷ 100 = ₹5400.\n15000 × {112/100} = ₹16,800; 16800 × {112/100} = ₹18,816.\n18816 × {112/100} = ₹21,073.92; CI = 21073.92 − 15000 = ₹6073.92.\n6073.92 − 5400 = ₹673.92."}, {"kind": "mcq", "text": "<b>Try This (p. 140) · a</b> · Find the compound interest on a sum of ₹15,000 for one year at 5% per annum, compounded annually.", "opts": ["₹759.38", "₹1500", "₹750", "₹15,750"], "correct": 2, "tag": "", "sol": "For one year compounded annually, CI = SI = 15000 × 5 × 1 ÷ 100 = ₹750. (₹15,750 is the amount; ₹759.38 is for half-yearly compounding.)"}, {"kind": "blank", "p": "<b>Ex 11B · Q1</b> · What will a loan of ₹15,000 amount to in 3 years if compounded annually at the rate of 10% p.a.?", "tag": "", "marks": "", "flat": [{"t": "Amount after 1 year = ₹__B1__", "a": {"B1": "16500"}, "accept": ["16,500", "16,500.00", "16500", "16500.00", "inr16,500", "inr16,500.00", "inr16500", "inr16500.00", "rs.16,500", "rs.16,500.00", "rs.16500", "rs.16500.00", "rs16,500", "rs16,500.00", "rs16500", "rs16500.00", "₹16,500", "₹16,500.00", "₹16500", "₹16500.00"]}, {"t": "Amount after 2 years = ₹__B1__", "a": {"B1": "18150"}, "accept": ["18,150", "18,150.00", "18150", "18150.00", "inr18,150", "inr18,150.00", "inr18150", "inr18150.00", "rs.18,150", "rs.18,150.00", "rs.18150", "rs.18150.00", "rs18,150", "rs18,150.00", "rs18150", "rs18150.00", "₹18,150", "₹18,150.00", "₹18150", "₹18150.00"]}, {"t": "Amount after 3 years = ₹__B1__", "a": {"B1": "19965"}, "accept": ["19,965", "19,965.00", "19965", "19965.00", "inr19,965", "inr19,965.00", "inr19965", "inr19965.00", "rs.19,965", "rs.19,965.00", "rs.19965", "rs.19965.00", "rs19,965", "rs19,965.00", "rs19965", "rs19965.00", "₹19,965", "₹19,965.00", "₹19965", "₹19965.00"]}], "sol": "15000 + 1500 = ₹16,500.\n16500 + 1650 = ₹18,150.\n18150 + 1815 = ₹19,965."}, {"kind": "blank", "p": "<b>Ex 11B · Q2</b> · Find the difference between compound interest and simple interest on a sum of ₹12,000 at the rate of 12% p.a. for 2 years (compounded annually).", "tag": "", "marks": "", "flat": [{"t": "CI = ₹__B1__", "a": {"B1": "3052.80"}, "accept": ["3,052.8", "3,052.80", "3052.8", "3052.80", "inr3,052.8", "inr3,052.80", "inr3052.8", "inr3052.80", "rs.3,052.8", "rs.3,052.80", "rs.3052.8", "rs.3052.80", "rs3,052.8", "rs3,052.80", "rs3052.8", "rs3052.80", "₹3,052.8", "₹3,052.80", "₹3052.8", "₹3052.80"]}, {"t": "SI = ₹__B1__", "a": {"B1": "2880"}, "accept": ["2,880", "2,880.00", "2880", "2880.00", "inr2,880", "inr2,880.00", "inr2880", "inr2880.00", "rs.2,880", "rs.2,880.00", "rs.2880", "rs.2880.00", "rs2,880", "rs2,880.00", "rs2880", "rs2880.00", "₹2,880", "₹2,880.00", "₹2880", "₹2880.00"]}, {"t": "CI − SI = ₹__B1__", "a": {"B1": "172.80"}, "accept": ["172.8", "172.80", "inr172.8", "inr172.80", "rs.172.8", "rs.172.80", "rs172.8", "rs172.80", "₹172.8", "₹172.80"]}], "sol": "Year 1: 12000 × {112/100} = ₹13,440; year 2: 13440 × {112/100} = ₹15,052.80. CI = ₹3052.80.\nSI = 12000 × 12 × 2 ÷ 100 = ₹2880.\n3052.80 − 2880 = ₹172.80."}]}, {"id": "s4", "label": "11.4 CI formula", "sub": "Using A = P(1 + R/100)ᵗ for annual compounding", "slides": [{"kind": "blank", "p": "<b>Formula for CI (p. 140)</b> · Sohan borrowed ₹4000 at compound interest at the rate of 15% p.a. for three years. Find the amount he has to pay back at the end of three years and the CI.", "tag": "", "marks": "", "flat": [{"t": "Amount = ₹__B1__", "a": {"B1": "6083.50"}, "accept": ["6,083.5", "6,083.50", "6083.5", "6083.50", "inr6,083.5", "inr6,083.50", "inr6083.5", "inr6083.50", "rs.6,083.5", "rs.6,083.50", "rs.6083.5", "rs.6083.50", "rs6,083.5", "rs6,083.50", "rs6083.5", "rs6083.50", "₹6,083.5", "₹6,083.50", "₹6083.5", "₹6083.50"]}, {"t": "CI = ₹__B1__", "a": {"B1": "2083.50"}, "accept": ["2,083.5", "2,083.50", "2083.5", "2083.50", "inr2,083.5", "inr2,083.50", "inr2083.5", "inr2083.50", "rs.2,083.5", "rs.2,083.50", "rs.2083.5", "rs.2083.50", "rs2,083.5", "rs2,083.50", "rs2083.5", "rs2083.50", "₹2,083.5", "₹2,083.50", "₹2083.5", "₹2083.50"]}], "sol": "A = 4000 × ({115/100})<sup>3</sup> = 4000 × ({23/20})<sup>3</sup> = 4000 × {12167/8000} = ₹6083.50.\nCI = 6083.50 − 4000 = ₹2083.50."}, {"kind": "mcq", "text": "<b>Example 13</b> · Find the compound interest on ₹7000 for 3 years at 5% per annum compounded annually (to the nearest paisa).", "opts": ["₹1157.63", "₹1103.38", "₹1050", "₹8103.38"], "correct": 1, "tag": "", "sol": "A = 7000 × ({105/100})<sup>3</sup> = 7000 × ({21/20})<sup>3</sup> = ₹8103.375 = ₹8103.38. CI = ₹8103.38 − ₹7000 = ₹1103.38. (₹1050 is the simple interest.)"}, {"kind": "blank", "p": "<b>Ex 11C · Q1</b> · Find the compound interest on ₹20,000 at 15% per annum for 3 years.", "tag": "", "marks": "", "flat": [{"t": "Amount = ₹__B1__", "a": {"B1": "30417.50"}, "accept": ["30,417.5", "30,417.50", "30417.5", "30417.50", "inr30,417.5", "inr30,417.50", "inr30417.5", "inr30417.50", "rs.30,417.5", "rs.30,417.50", "rs.30417.5", "rs.30417.50", "rs30,417.5", "rs30,417.50", "rs30417.5", "rs30417.50", "₹30,417.5", "₹30,417.50", "₹30417.5", "₹30417.50"]}, {"t": "CI = ₹__B1__", "a": {"B1": "10417.50"}, "accept": ["10,417.5", "10,417.50", "10417.5", "10417.50", "inr10,417.5", "inr10,417.50", "inr10417.5", "inr10417.50", "rs.10,417.5", "rs.10,417.50", "rs.10417.5", "rs.10417.50", "rs10,417.5", "rs10,417.50", "rs10417.5", "rs10417.50", "₹10,417.5", "₹10,417.50", "₹10417.5", "₹10417.50"]}], "sol": "A = 20000 × ({23/20})<sup>3</sup> = 20000 × {12167/8000} = ₹30,417.50.\nCI = 30417.50 − 20000 = ₹10,417.50."}, {"kind": "blank", "p": "<b>Ex 11C · Q2</b> · Find the compound interest on ₹5000 at 8% per annum for 3 years.", "tag": "", "marks": "", "flat": [{"t": "Amount = ₹__B1__", "a": {"B1": "6298.56"}, "accept": ["6,298.56", "6298.56", "inr6,298.56", "inr6298.56", "rs.6,298.56", "rs.6298.56", "rs6,298.56", "rs6298.56", "₹6,298.56", "₹6298.56"]}, {"t": "CI = ₹__B1__", "a": {"B1": "1298.56"}, "accept": ["1,298.56", "1298.56", "inr1,298.56", "inr1298.56", "rs.1,298.56", "rs.1298.56", "rs1,298.56", "rs1298.56", "₹1,298.56", "₹1298.56"]}], "sol": "A = 5000 × ({27/25})<sup>3</sup> = 5000 × {19683/15625} = ₹6298.56.\nCI = 6298.56 − 5000 = ₹1298.56."}, {"kind": "mcq", "text": "<b>Ex 11C · Q3</b> · Find the compound interest on ₹8000 at 5% per annum for 3 years.", "opts": ["₹1260", "₹9261", "₹1200", "₹1261"], "correct": 3, "tag": "", "sol": "A = 8000 × ({21/20})<sup>3</sup> = 8000 × {9261/8000} = ₹9261. CI = 9261 − 8000 = ₹1261. (₹1200 is the SI.)"}, {"kind": "blank", "p": "<b>Ex 11C · Q4</b> · Find the amount and the compound interest on ₹2500 at 15% per annum for 2 years.", "tag": "", "marks": "", "flat": [{"t": "Amount = ₹__B1__", "a": {"B1": "3306.25"}, "accept": ["3,306.25", "3306.25", "inr3,306.25", "inr3306.25", "rs.3,306.25", "rs.3306.25", "rs3,306.25", "rs3306.25", "₹3,306.25", "₹3306.25"]}, {"t": "CI = ₹__B1__", "a": {"B1": "806.25"}, "accept": ["806.25", "inr806.25", "rs.806.25", "rs806.25", "₹806.25"]}], "sol": "A = 2500 × ({23/20})<sup>2</sup> = 2500 × {529/400} = ₹3306.25.\nCI = 3306.25 − 2500 = ₹806.25."}, {"kind": "blank", "p": "<b>Ex 11C · Q5</b> · Find the compound interest on ₹4000 for {2 1/2} years at 10% per annum (compounded annually).", "tag": "", "marks": "", "flat": [{"t": "Amount after 2 years = ₹__B1__", "a": {"B1": "4840"}, "accept": ["4,840", "4,840.00", "4840", "4840.00", "inr4,840", "inr4,840.00", "inr4840", "inr4840.00", "rs.4,840", "rs.4,840.00", "rs.4840", "rs.4840.00", "rs4,840", "rs4,840.00", "rs4840", "rs4840.00", "₹4,840", "₹4,840.00", "₹4840", "₹4840.00"]}, {"t": "Interest for the last {1/2} year = ₹__B1__", "a": {"B1": "242"}, "accept": ["242", "242.00", "inr242", "inr242.00", "rs.242", "rs.242.00", "rs242", "rs242.00", "₹242", "₹242.00"]}, {"t": "CI = ₹__B1__", "a": {"B1": "1082"}, "accept": ["1,082", "1,082.00", "1082", "1082.00", "inr1,082", "inr1,082.00", "inr1082", "inr1082.00", "rs.1,082", "rs.1,082.00", "rs.1082", "rs.1082.00", "rs1,082", "rs1,082.00", "rs1082", "rs1082.00", "₹1,082", "₹1,082.00", "₹1082", "₹1082.00"]}], "sol": "A = 4000 × ({11/10})<sup>2</sup> = ₹4840.\nThe last half year earns simple interest on ₹4840: 4840 × 10 × {1/2} ÷ 100 = ₹242. Amount = ₹5082.\nCI = 5082 − 4000 = ₹1082."}, {"kind": "mcq", "text": "<b>Ex 11C · Q6</b> · Find the compound interest on ₹5000 at 6% per annum for 3 years (to the nearest paisa).", "opts": ["₹955.08", "₹900", "₹954.08", "₹5955.08"], "correct": 0, "tag": "", "sol": "A = 5000 × ({106/100})<sup>3</sup> = 5000 × 1.191016 = ₹5955.08. CI = ₹955.08. (₹900 is the SI.)"}, {"kind": "blank", "p": "<b>Ex 11C · Q7</b> · Calculate the amount if ₹18,000 is invested at 15% p.a. compounded annually for 3 years.", "tag": "", "marks": "", "flat": [{"t": "Amount = ₹__B1__", "a": {"B1": "27375.75"}, "accept": ["27,375.75", "27375.75", "inr27,375.75", "inr27375.75", "rs.27,375.75", "rs.27375.75", "rs27,375.75", "rs27375.75", "₹27,375.75", "₹27375.75"]}], "sol": "A = 18000 × ({23/20})<sup>3</sup> = 18000 × {12167/8000} = ₹27,375.75."}, {"kind": "blank", "p": "<b>Ex 11C · Q8</b> · Calculate the amount if ₹12,000 is invested at 12% p.a. compounded annually for 2 years. Also, find the compound interest.", "tag": "", "marks": "", "flat": [{"t": "Amount = ₹__B1__", "a": {"B1": "15052.80"}, "accept": ["15,052.8", "15,052.80", "15052.8", "15052.80", "inr15,052.8", "inr15,052.80", "inr15052.8", "inr15052.80", "rs.15,052.8", "rs.15,052.80", "rs.15052.8", "rs.15052.80", "rs15,052.8", "rs15,052.80", "rs15052.8", "rs15052.80", "₹15,052.8", "₹15,052.80", "₹15052.8", "₹15052.80"]}, {"t": "CI = ₹__B1__", "a": {"B1": "3052.80"}, "accept": ["3,052.8", "3,052.80", "3052.8", "3052.80", "inr3,052.8", "inr3,052.80", "inr3052.8", "inr3052.80", "rs.3,052.8", "rs.3,052.80", "rs.3052.8", "rs.3052.80", "rs3,052.8", "rs3,052.80", "rs3052.8", "rs3052.80", "₹3,052.8", "₹3,052.80", "₹3052.8", "₹3052.80"]}], "sol": "A = 12000 × ({28/25})<sup>2</sup> = 12000 × {784/625} = ₹15,052.80.\nCI = 15052.80 − 12000 = ₹3052.80."}, {"kind": "mcq", "text": "<b>Ex 11C · Q13</b> · Seema invested ₹6400 for 3 years at 10% per annum compounded annually. Sonali invested the same amount at the same rate for the same time but on simple interest. Who gets more interest and by how much?", "opts": ["They get the same interest", "Seema, by ₹198.40", "Seema, by ₹640", "Sonali, by ₹198.40"], "correct": 1, "tag": "", "sol": "Seema: A = 6400 × ({11/10})<sup>3</sup> = ₹8518.40, CI = ₹2118.40. Sonali: SI = 6400 × 10 × 3 ÷ 100 = ₹1920. Seema gets ₹2118.40 − ₹1920 = ₹198.40 more."}]}, {"id": "s5", "label": "11.5 Half-yearly & quarterly", "sub": "Compound interest with half-yearly and quarterly conversion periods", "slides": [{"kind": "blank", "p": "<b>Example 12</b> · Find the compound interest on a sum of ₹3000 for {1 1/2} years at 8% p.a. compounded semi-annually.", "tag": "", "marks": "", "flat": [{"t": "Number of conversion periods = __B1__", "a": {"B1": "3"}}, {"t": "Interest for the first six months = ₹__B1__", "a": {"B1": "120"}, "accept": ["120", "120.00", "inr120", "inr120.00", "rs.120", "rs.120.00", "rs120", "rs120.00", "₹120", "₹120.00"]}, {"t": "Amount after 1 year = ₹__B1__", "a": {"B1": "3244.80"}, "accept": ["3,244.8", "3,244.80", "3244.8", "3244.80", "inr3,244.8", "inr3,244.80", "inr3244.8", "inr3244.80", "rs.3,244.8", "rs.3,244.80", "rs.3244.8", "rs.3244.80", "rs3,244.8", "rs3,244.80", "rs3244.8", "rs3244.80", "₹3,244.8", "₹3,244.80", "₹3244.8", "₹3244.80"]}, {"t": "Amount after {1 1/2} years = ₹__B1__ (to the nearest paisa)", "a": {"B1": "3374.59"}, "accept": ["3,374.59", "3,374.592", "3,374.6", "3,374.60", "3,375", "3,375.00", "3374.59", "3374.592", "3374.6", "3374.60", "3375", "3375.00", "inr3,374.59", "inr3,374.592", "inr3,374.6", "inr3,374.60", "inr3,375", "inr3,375.00", "inr3374.59", "inr3374.592", "inr3374.6", "inr3374.60", "inr3375", "inr3375.00", "rs.3,374.59", "rs.3,374.592", "rs.3,374.6", "rs.3,374.60", "rs.3,375", "rs.3,375.00", "rs.3374.59", "rs.3374.592", "rs.3374.6", "rs.3374.60", "rs.3375", "rs.3375.00", "rs3,374.59", "rs3,374.592", "rs3,374.6", "rs3,374.60", "rs3,375", "rs3,375.00", "rs3374.59", "rs3374.592", "rs3374.6", "rs3374.60", "rs3375", "rs3375.00", "₹3,374.59", "₹3,374.592", "₹3,374.6", "₹3,374.60", "₹3,375", "₹3,375.00", "₹3374.59", "₹3374.592", "₹3374.6", "₹3374.60", "₹3375", "₹3375.00"]}, {"t": "CI = ₹__B1__ (to the nearest paisa)", "a": {"B1": "374.59"}, "accept": ["374.59", "374.592", "374.6", "374.60", "375", "375.00", "inr374.59", "inr374.592", "inr374.6", "inr374.60", "inr375", "inr375.00", "rs.374.59", "rs.374.592", "rs.374.6", "rs.374.60", "rs.375", "rs.375.00", "rs374.59", "rs374.592", "rs374.6", "rs374.60", "rs375", "rs375.00", "₹374.59", "₹374.592", "₹374.6", "₹374.60", "₹375", "₹375.00"]}], "sol": "Interest is added every six months, so {1 1/2} years has 3 conversion periods.\n3000 × 8 × {1/2} ÷ 100 = ₹120; amount ₹3120.\nInterest 3120 × 8 × {1/2} ÷ 100 = ₹124.80; amount ₹3244.80.\nInterest 3244.80 × 8 × {1/2} ÷ 100 = 12979.20 ÷ 100 = ₹129.792 ≈ ₹129.79; amount = ₹3374.592 ≈ ₹3374.59. (Or: 4% per half-year for 3 half-years: 3000 × (1.04)<sup>3</sup> = ₹3374.592.) The book rounds the last interest to ₹129.80 and gets ₹3374.60, which is also accepted.\nCI = 3374.592 − 3000 = ₹374.592 ≈ ₹374.59 (book: ₹374.60)."}, {"kind": "mcq", "text": "<b>Example 14</b> · Find the compound interest on ₹5000 at 12% p.a. for {1 1/2} years, if the interest is compounded semi-annually.", "opts": ["₹955.08", "₹900", "₹1080", "₹955.80"], "correct": 0, "tag": "", "sol": "Rate per half-year = 6%, number of periods = 3. A = 5000 × ({106/100})<sup>3</sup> = {5955080/1000} = ₹5955.08. CI = ₹955.08. (₹900 is the SI.)"}, {"kind": "blank", "p": "<b>Try This (p. 140) · b</b> · Find the compound interest on a sum of ₹15,000 for one year at 5% per annum, compounded half-yearly (to the nearest paisa).", "tag": "", "marks": "", "flat": [{"t": "Rate per half-year = __B1__ %", "a": {"B1": "2.5"}, "accept": ["2.5%", "5/2"]}, {"t": "Amount = ₹__B1__", "a": {"B1": "15759.38"}, "accept": ["15,759", "15,759.00", "15,759.375", "15,759.38", "15,759.4", "15759", "15759.00", "15759.375", "15759.38", "15759.4", "inr15,759", "inr15,759.00", "inr15,759.375", "inr15,759.38", "inr15,759.4", "inr15759", "inr15759.00", "inr15759.375", "inr15759.38", "inr15759.4", "rs.15,759", "rs.15,759.00", "rs.15,759.375", "rs.15,759.38", "rs.15,759.4", "rs.15759", "rs.15759.00", "rs.15759.375", "rs.15759.38", "rs.15759.4", "rs15,759", "rs15,759.00", "rs15,759.375", "rs15,759.38", "rs15,759.4", "rs15759", "rs15759.00", "rs15759.375", "rs15759.38", "rs15759.4", "₹15,759", "₹15,759.00", "₹15,759.375", "₹15,759.38", "₹15,759.4", "₹15759", "₹15759.00", "₹15759.375", "₹15759.38", "₹15759.4"]}, {"t": "CI = ₹__B1__", "a": {"B1": "759.38"}, "accept": ["759", "759.00", "759.375", "759.38", "759.4", "inr759", "inr759.00", "inr759.375", "inr759.38", "inr759.4", "rs.759", "rs.759.00", "rs.759.375", "rs.759.38", "rs.759.4", "rs759", "rs759.00", "rs759.375", "rs759.38", "rs759.4", "₹759", "₹759.00", "₹759.375", "₹759.38", "₹759.4"]}], "sol": "5% p.a. = 2.5% per half-year; one year = 2 half-years.\nA = 15000 × ({41/40})<sup>2</sup> = ₹15,759.375 ≈ ₹15,759.38 (to the nearest paisa).\nCI = 15759.38 − 15000 = ₹759.38 (₹9.38 more than with annual compounding)."}, {"kind": "blank", "p": "<b>Ex 11B · Q3</b> · Find the compound interest on ₹5000 at the rate of 10% p.a. compounded semi-annually for {1 1/2} years (to the nearest paisa).", "tag": "", "marks": "", "flat": [{"t": "Amount = ₹__B1__", "a": {"B1": "5788.13"}, "accept": ["5,788", "5,788.00", "5,788.1", "5,788.125", "5,788.13", "5788", "5788.00", "5788.1", "5788.125", "5788.13", "inr5,788", "inr5,788.00", "inr5,788.1", "inr5,788.125", "inr5,788.13", "inr5788", "inr5788.00", "inr5788.1", "inr5788.125", "inr5788.13", "rs.5,788", "rs.5,788.00", "rs.5,788.1", "rs.5,788.125", "rs.5,788.13", "rs.5788", "rs.5788.00", "rs.5788.1", "rs.5788.125", "rs.5788.13", "rs5,788", "rs5,788.00", "rs5,788.1", "rs5,788.125", "rs5,788.13", "rs5788", "rs5788.00", "rs5788.1", "rs5788.125", "rs5788.13", "₹5,788", "₹5,788.00", "₹5,788.1", "₹5,788.125", "₹5,788.13", "₹5788", "₹5788.00", "₹5788.1", "₹5788.125", "₹5788.13"]}, {"t": "CI = ₹__B1__", "a": {"B1": "788.13"}, "accept": ["788", "788.00", "788.1", "788.125", "788.13", "inr788", "inr788.00", "inr788.1", "inr788.125", "inr788.13", "rs.788", "rs.788.00", "rs.788.1", "rs.788.125", "rs.788.13", "rs788", "rs788.00", "rs788.1", "rs788.125", "rs788.13", "₹788", "₹788.00", "₹788.1", "₹788.125", "₹788.13"]}], "sol": "5% per half-year, 3 half-years: 5000 → 5250 → 5512.50 → 5788.125 ≈ ₹5788.13.\nCI = 5788.13 − 5000 = ₹788.13."}, {"kind": "mcq", "text": "<b>Ex 11B · Q4</b> · Find the difference between compound interest and simple interest on a sum of ₹64,000 at the rate of 20% p.a. compounded semi-annually for {1 1/2} years.", "opts": ["₹21,184", "₹2984", "₹19,200", "₹1984"], "correct": 3, "tag": "", "sol": "10% per half-year, 3 half-years: A = 64000 × ({11/10})<sup>3</sup> = ₹85,184, CI = ₹21,184. SI = 64000 × 20 × {3/2} ÷ 100 = ₹19,200. Difference = 21184 − 19200 = ₹1984."}, {"kind": "blank", "p": "<b>Ex 11C · Q9</b> · Calculate the compound interest on ₹20,000 at 16% p.a. for 9 months compounded quarterly.", "tag": "", "marks": "", "flat": [{"t": "Rate per quarter = __B1__ %", "a": {"B1": "4"}, "accept": ["4%"]}, {"t": "Number of quarters = __B1__", "a": {"B1": "3"}}, {"t": "CI = ₹__B1__", "a": {"B1": "2497.28"}, "accept": ["2,497.28", "2497.28", "inr2,497.28", "inr2497.28", "rs.2,497.28", "rs.2497.28", "rs2,497.28", "rs2497.28", "₹2,497.28", "₹2497.28"]}], "sol": "16% ÷ 4 = 4% per quarter.\n9 months = 3 quarters.\nA = 20000 × ({26/25})<sup>3</sup> = ₹22,497.28; CI = ₹2497.28."}, {"kind": "blank", "p": "<b>Ex 11C · Q10</b> · Find the amount and CI on ₹24,000 compounded semi-annually for {1 1/2} years at the rate of 10% p.a.", "tag": "", "marks": "", "flat": [{"t": "Amount = ₹__B1__", "a": {"B1": "27783"}, "accept": ["27,783", "27,783.00", "27783", "27783.00", "inr27,783", "inr27,783.00", "inr27783", "inr27783.00", "rs.27,783", "rs.27,783.00", "rs.27783", "rs.27783.00", "rs27,783", "rs27,783.00", "rs27783", "rs27783.00", "₹27,783", "₹27,783.00", "₹27783", "₹27783.00"]}, {"t": "CI = ₹__B1__", "a": {"B1": "3783"}, "accept": ["3,783", "3,783.00", "3783", "3783.00", "inr3,783", "inr3,783.00", "inr3783", "inr3783.00", "rs.3,783", "rs.3,783.00", "rs.3783", "rs.3783.00", "rs3,783", "rs3,783.00", "rs3783", "rs3783.00", "₹3,783", "₹3,783.00", "₹3783", "₹3783.00"]}], "sol": "5% per half-year, 3 periods: A = 24000 × ({21/20})<sup>3</sup> = 24000 × {9261/8000} = ₹27,783.\nCI = 27783 − 24000 = ₹3783."}, {"kind": "mcq", "text": "<b>Ex 11C · Q11</b> · Find the amount and compound interest on ₹1,00,000 compounded semi-annually for {1 1/2} years at the rate of 8% p.a.", "opts": ["Amount ₹1,12,360, CI ₹12,360", "Amount ₹1,12,486.40, CI ₹12,486.40", "Amount ₹1,25,971.20, CI ₹25,971.20", "Amount ₹1,12,000, CI ₹12,000"], "correct": 1, "tag": "", "sol": "4% per half-year, 3 periods: A = 100000 × (1.04)<sup>3</sup> = 100000 × 1.124864 = ₹1,12,486.40; CI = ₹12,486.40. (₹1,25,971.20 uses 8% for 3 periods; ₹1,12,360 uses only 2 periods at 6%.)"}, {"kind": "blank", "p": "<b>Ex 11C · Q12</b> · Find the compound interest and amount on ₹35,000 for {1 1/2} years compounded semi-annually at the rate of 12% p.a. (to the nearest paisa).", "tag": "", "marks": "", "flat": [{"t": "Amount = ₹__B1__", "a": {"B1": "41685.56"}, "accept": ["41,685.556", "41,685.56", "41,685.6", "41,686", "41,686.00", "41685.556", "41685.56", "41685.6", "41686", "41686.00", "inr41,685.556", "inr41,685.56", "inr41,685.6", "inr41,686", "inr41,686.00", "inr41685.556", "inr41685.56", "inr41685.6", "inr41686", "inr41686.00", "rs.41,685.556", "rs.41,685.56", "rs.41,685.6", "rs.41,686", "rs.41,686.00", "rs.41685.556", "rs.41685.56", "rs.41685.6", "rs.41686", "rs.41686.00", "rs41,685.556", "rs41,685.56", "rs41,685.6", "rs41,686", "rs41,686.00", "rs41685.556", "rs41685.56", "rs41685.6", "rs41686", "rs41686.00", "₹41,685.556", "₹41,685.56", "₹41,685.6", "₹41,686", "₹41,686.00", "₹41685.556", "₹41685.56", "₹41685.6", "₹41686", "₹41686.00"]}, {"t": "CI = ₹__B1__", "a": {"B1": "6685.56"}, "accept": ["6,685.556", "6,685.56", "6,685.6", "6,686", "6,686.00", "6685.556", "6685.56", "6685.6", "6686", "6686.00", "inr6,685.556", "inr6,685.56", "inr6,685.6", "inr6,686", "inr6,686.00", "inr6685.556", "inr6685.56", "inr6685.6", "inr6686", "inr6686.00", "rs.6,685.556", "rs.6,685.56", "rs.6,685.6", "rs.6,686", "rs.6,686.00", "rs.6685.556", "rs.6685.56", "rs.6685.6", "rs.6686", "rs.6686.00", "rs6,685.556", "rs6,685.56", "rs6,685.6", "rs6,686", "rs6,686.00", "rs6685.556", "rs6685.56", "rs6685.6", "rs6686", "rs6686.00", "₹6,685.556", "₹6,685.56", "₹6,685.6", "₹6,686", "₹6,686.00", "₹6685.556", "₹6685.56", "₹6685.6", "₹6686", "₹6686.00"]}], "sol": "6% per half-year, 3 periods: 35000 → 37100 → 39326 → 41685.56 (35000 × 1.191016 = 41685.556).\nCI = 41685.56 − 35000 = ₹6685.56."}]}, {"id": "s6", "label": "11.6 Find t, P and R", "sub": "Finding time, principal and rate with compound interest", "slides": [{"kind": "blank", "p": "<b>Example 15</b> · In how many years will ₹4000 amount to ₹5324 at 10% p.a. compounded annually?", "tag": "", "marks": "", "flat": [{"t": "{5324/4000} in lowest terms = __B1__", "a": {"B1": "1331/1000"}, "expr": "fl"}, {"t": "({11/10})<sup>t</sup> = ({11/10})<sup>3</sup>, so t = __B1__ years", "a": {"B1": "3"}, "accept": ["3 years", "3 year", "3 yrs", "3 yr"]}], "sol": "{5324/4000} = {1331/1000} = ({11/10})<sup>3</sup>.\n5324 = 4000 × ({11/10})<sup>t</sup> ⇒ t = 3 years."}, {"kind": "mcq", "text": "<b>Example 16</b> · What sum of money will amount to ₹2508.80 at 12% p.a. compounded annually in two years’ time?", "opts": ["₹2200", "₹2240", "₹1999.04", "₹2000"], "correct": 3, "tag": "", "sol": "2508.80 = P × ({112/100})<sup>2</sup> = P × {784/625}. P = 2508.80 × 625 ÷ 784 = ₹2000."}, {"kind": "blank", "p": "<b>Example 17</b> · At what rate of compound interest p.a. will ₹1250 amount to ₹1800 in two years?", "tag": "", "marks": "", "flat": [{"t": "(1 + R/100)<sup>2</sup> = {1800/1250} = __B1__ (lowest terms)", "a": {"B1": "36/25"}, "expr": "fl"}, {"t": "1 + R/100 = __B1__", "a": {"B1": "6/5"}, "expr": "fv"}, {"t": "R = __B1__ % p.a.", "a": {"B1": "20"}, "accept": ["20%", "20% p.a.", "20%p.a"]}], "sol": "{1800/1250} = {36/25}.\n{36/25} = ({6/5})<sup>2</sup>, so 1 + R/100 = {6/5}.\nR/100 = {6/5} − 1 = {1/5} ⇒ R = 20% p.a."}, {"kind": "blank", "p": "<b>Example 18</b> · The compound interest on a sum of money for 3 years at 10% p.a. is ₹264.80. Find the simple interest for the same sum for the same time at the same rate.", "tag": "", "marks": "", "flat": [{"t": "CI on ₹100 for 3 years at 10% = ₹__B1__", "a": {"B1": "33.10"}, "accept": ["33.1", "33.10", "inr33.1", "inr33.10", "rs.33.1", "rs.33.10", "rs33.1", "rs33.10", "₹33.1", "₹33.10"]}, {"t": "Principal = ₹__B1__", "a": {"B1": "800"}, "accept": ["800", "800.00", "inr800", "inr800.00", "rs.800", "rs.800.00", "rs800", "rs800.00", "₹800", "₹800.00"]}, {"t": "SI = ₹__B1__", "a": {"B1": "240"}, "accept": ["240", "240.00", "inr240", "inr240.00", "rs.240", "rs.240.00", "rs240", "rs240.00", "₹240", "₹240.00"]}], "sol": "100 × {110/100} × {110/100} × {110/100} = ₹133.10; CI = ₹33.10.\nP = 100 × 264.80 ÷ 33.10 = ₹800.\nSI = 800 × 3 × 10 ÷ 100 = ₹240."}, {"kind": "mcq", "text": "<b>Try This (p. 143) · a</b> · Find the missing value if the interest is compounded annually: P = ₹13,500, A = ₹17,000, CI = ?", "opts": ["₹3500", "₹30,500", "₹4500", "₹3000"], "correct": 0, "tag": "", "sol": "CI = A − P = ₹17,000 − ₹13,500 = ₹3500."}, {"kind": "blank", "p": "<b>Try This (p. 143) · b, c</b> · Find the missing value if the interest is compounded annually.\nb) A = ₹3645, P = ₹3125, R = 8% p.a., t = ?\nc) A = ₹1000, P = ₹729, t = 3 years, R = ?", "tag": "", "marks": "", "flat": [{"t": "b) t = __B1__ years", "a": {"B1": "2"}, "accept": ["2 years", "2 year", "2 yrs", "2 yr"]}, {"t": "c) R = __B1__ % (type a fraction or mixed number)", "a": {"B1": "100/9"}, "expr": "fv"}], "sol": "{3645/3125} = {729/625} = ({27/25})<sup>2</sup> = (1 + {8/100})<sup>2</sup>, so t = 2 years.\n{1000/729} = ({10/9})<sup>3</sup>, so 1 + R/100 = {10/9}, R/100 = {1/9}, R = {100/9} = {11 1/9}% p.a."}, {"kind": "blank", "p": "<b>Ex 11D · Q1</b> · A sum of money invested at compound interest of 8% p.a. compounded annually amounts to ₹7290 in two years. Find the sum invested.", "tag": "", "marks": "", "flat": [{"t": "Sum invested = ₹__B1__", "a": {"B1": "6250"}, "accept": ["6,250", "6,250.00", "6250", "6250.00", "inr6,250", "inr6,250.00", "inr6250", "inr6250.00", "rs.6,250", "rs.6,250.00", "rs.6250", "rs.6250.00", "rs6,250", "rs6,250.00", "rs6250", "rs6250.00", "₹6,250", "₹6,250.00", "₹6250", "₹6250.00"]}], "sol": "P = 7290 ÷ ({27/25})<sup>2</sup> = 7290 × {625/729} = ₹6250."}, {"kind": "mcq", "text": "<b>Ex 11D · Q2</b> · An investment at the rate of 18% p.a. compounded annually amounts to ₹4177.20 in two years. What was the sum invested?", "opts": ["₹2900", "₹3100", "₹3000", "₹3540"], "correct": 2, "tag": "", "sol": "P = 4177.20 ÷ (1.18)<sup>2</sup> = 4177.20 ÷ 1.3924 = ₹3000."}, {"kind": "blank", "p": "<b>Ex 11D · Q3</b> · If the amount after 3 years at the rate of {12 1/2}% per annum compounded annually is ₹10,935, find the principal.", "tag": "", "marks": "", "flat": [{"t": "Principal = ₹__B1__", "a": {"B1": "7680"}, "accept": ["7,680", "7,680.00", "7680", "7680.00", "inr7,680", "inr7,680.00", "inr7680", "inr7680.00", "rs.7,680", "rs.7,680.00", "rs.7680", "rs.7680.00", "rs7,680", "rs7,680.00", "rs7680", "rs7680.00", "₹7,680", "₹7,680.00", "₹7680", "₹7680.00"]}], "sol": "1 + {25/200} = {9/8}. P = 10935 ÷ ({9/8})<sup>3</sup> = 10935 × {512/729} = ₹7680."}, {"kind": "blank", "p": "<b>Ex 11D · Q4</b> · If a sum of ₹40,000 at compound interest of 5% p.a. amounts to ₹44,100, find the time for which the money was invested.", "tag": "", "marks": "", "flat": [{"t": "t = __B1__ years", "a": {"B1": "2"}, "accept": ["2 years", "2 year", "2 yrs", "2 yr"]}], "sol": "{44100/40000} = {441/400} = ({21/20})<sup>2</sup>, so t = 2 years."}, {"kind": "mcq", "text": "<b>Ex 11D · Q5</b> · In how many years will ₹6750 amount to ₹8192 at {6 2/3}% p.a. compounded annually?", "opts": ["{2 1/2} years", "3 years", "4 years", "2 years"], "correct": 1, "tag": "", "sol": "1 + {20/300} = {16/15}. {8192/6750} = {4096/3375} = ({16/15})<sup>3</sup>, so t = 3 years."}, {"kind": "blank", "p": "<b>Ex 11D · Q6</b> · In how many years will ₹2000 amount to ₹2163.20 at 4% p.a. compounded annually?", "tag": "", "marks": "", "flat": [{"t": "t = __B1__ years", "a": {"B1": "2"}, "accept": ["2 years", "2 year", "2 yrs", "2 yr"]}], "sol": "2163.20 ÷ 2000 = 1.0816 = (1.04)<sup>2</sup>, so t = 2 years."}, {"kind": "blank", "p": "<b>Ex 11D · Q7</b> · Find the difference between simple interest and compound interest on ₹2400 for 2 years at 5% per annum compounded annually.", "tag": "", "marks": "", "flat": [{"t": "SI = ₹__B1__", "a": {"B1": "240"}, "accept": ["240", "240.00", "inr240", "inr240.00", "rs.240", "rs.240.00", "rs240", "rs240.00", "₹240", "₹240.00"]}, {"t": "CI = ₹__B1__", "a": {"B1": "246"}, "accept": ["246", "246.00", "inr246", "inr246.00", "rs.246", "rs.246.00", "rs246", "rs246.00", "₹246", "₹246.00"]}, {"t": "Difference = ₹__B1__", "a": {"B1": "6"}, "accept": ["6", "6.00", "inr6", "inr6.00", "rs.6", "rs.6.00", "rs6", "rs6.00", "₹6", "₹6.00"]}], "sol": "SI = 2400 × 5 × 2 ÷ 100 = ₹240.\nA = 2400 × ({21/20})<sup>2</sup> = ₹2646; CI = ₹246.\n246 − 240 = ₹6."}, {"kind": "mcq", "text": "<b>Ex 11D · Q8</b> · Find the difference between simple interest and compound interest on ₹6400 for 2 years at {6 1/4}% p.a. compounded annually.", "opts": ["₹20", "₹825", "₹800", "₹25"], "correct": 3, "tag": "", "sol": "SI = 6400 × {25/4} × 2 ÷ 100 = ₹800. A = 6400 × ({17/16})<sup>2</sup> = ₹7225, CI = ₹825. Difference = ₹25."}, {"kind": "blank", "p": "<b>Ex 11D · Q9</b> · The CI for a sum of money for 2 years at the rate of 10% per annum compounded annually is ₹315. Find the simple interest for the same sum for the same period at the same rate.", "tag": "", "marks": "", "flat": [{"t": "Principal = ₹__B1__", "a": {"B1": "1500"}, "accept": ["1,500", "1,500.00", "1500", "1500.00", "inr1,500", "inr1,500.00", "inr1500", "inr1500.00", "rs.1,500", "rs.1,500.00", "rs.1500", "rs.1500.00", "rs1,500", "rs1,500.00", "rs1500", "rs1500.00", "₹1,500", "₹1,500.00", "₹1500", "₹1500.00"]}, {"t": "SI = ₹__B1__", "a": {"B1": "300"}, "accept": ["300", "300.00", "inr300", "inr300.00", "rs.300", "rs.300.00", "rs300", "rs300.00", "₹300", "₹300.00"]}], "sol": "On ₹100, CI = 121 − 100 = ₹21. P = 100 × 315 ÷ 21 = ₹1500.\nSI = 1500 × 10 × 2 ÷ 100 = ₹300."}, {"kind": "blank", "p": "<b>Ex 11D · Q10</b> · The difference between SI and CI of a certain sum of money is ₹48 at 20% p.a. for 2 years. Find the principal. (Hint: assume the principal as ₹100.)", "tag": "", "marks": "", "flat": [{"t": "On ₹100: CI − SI = ₹__B1__", "a": {"B1": "4"}, "accept": ["4", "4.00", "inr4", "inr4.00", "rs.4", "rs.4.00", "rs4", "rs4.00", "₹4", "₹4.00"]}, {"t": "Principal = ₹__B1__", "a": {"B1": "1200"}, "accept": ["1,200", "1,200.00", "1200", "1200.00", "inr1,200", "inr1,200.00", "inr1200", "inr1200.00", "rs.1,200", "rs.1,200.00", "rs.1200", "rs.1200.00", "rs1,200", "rs1,200.00", "rs1200", "rs1200.00", "₹1,200", "₹1,200.00", "₹1200", "₹1200.00"]}], "sol": "On ₹100: CI = 144 − 100 = ₹44, SI = ₹40, difference ₹4.\nP = 100 × 48 ÷ 4 = ₹1200."}, {"kind": "mcq", "text": "<b>Ex 11D · Q11</b> · In how many years will a sum of ₹6400 compounded semi-annually at 5% p.a. amount to ₹6560?", "opts": ["{1 1/2} years", "2 years", "{1/2} year", "1 year"], "correct": 2, "tag": "", "sol": "Rate per half-year = 2.5%. {6560/6400} = {41/40} = 1 + 0.025 for one period, so the time is one half-year = {1/2} year."}, {"kind": "blank", "p": "<b>Ex 11D · Q12</b> · What sum invested for {1 1/2} years compounded half-yearly at the rate of 4% p.a. amounts to ₹1,32,651?", "tag": "", "marks": "", "flat": [{"t": "Rate per half-year = __B1__ %", "a": {"B1": "2"}, "accept": ["2%"]}, {"t": "Sum invested = ₹__B1__", "a": {"B1": "125000"}, "accept": ["1,25,000", "1,25,000.00", "125,000", "125,000.00", "125000", "125000.00", "inr1,25,000", "inr1,25,000.00", "inr125,000", "inr125,000.00", "inr125000", "inr125000.00", "rs.1,25,000", "rs.1,25,000.00", "rs.125,000", "rs.125,000.00", "rs.125000", "rs.125000.00", "rs1,25,000", "rs1,25,000.00", "rs125,000", "rs125,000.00", "rs125000", "rs125000.00", "₹1,25,000", "₹1,25,000.00", "₹125,000", "₹125,000.00", "₹125000", "₹125000.00"]}], "sol": "4% ÷ 2 = 2% per half-year, 3 periods.\nP = 132651 ÷ ({51/50})<sup>3</sup> = 132651 × {125000/132651} = ₹1,25,000."}]}, {"id": "s7", "label": "11.7 Growth & depreciation", "sub": "Population growth and decay, appreciation and depreciation", "slides": [{"kind": "blank", "p": "<b>Example 19</b> · The present population of a town is 3,20,000. If it increases at the rate of 5% p.a., what will be the population after two years?", "tag": "", "marks": "", "flat": [{"t": "Population after two years = __B1__", "a": {"B1": "352800"}}], "sol": "3,20,000 × {105/100} × {105/100} = 3,52,800."}, {"kind": "mcq", "text": "<b>Example 20</b> · The population of a village has a constant growth of 5% p.a. If its present population is 33,075, what was the population two years ago?", "opts": ["36,465", "31,500", "30,000", "29,768"], "correct": 2, "tag": "", "sol": "P × ({105/100})<sup>2</sup> = 33075 ⇒ P = 33075 × 100 × 100 ÷ (105 × 105) = 30,000. (29,768 takes 10% off 33,075; 31,500 goes back only one year; 36,465 grows forward instead of going back.)"}, {"kind": "blank", "p": "<b>Example 21</b> · The population of a town increases 4% during the first year and 5% during the second year. At the end of the second year, the population is 1,04,832. What was the population at the beginning?", "tag": "", "marks": "", "flat": [{"t": "Population at the beginning = __B1__", "a": {"B1": "96000"}}], "sol": "P × {104/100} × {105/100} = 104832 ⇒ P = 104832 × 100 × 100 ÷ (104 × 105) = 96,000."}, {"kind": "blank", "p": "<b>Example 22</b> · People from a village are migrating to nearby cities. The population of the village two years ago was 6000. The migration is taking place at the rate of 5% p.a. Find the present population.", "tag": "", "marks": "", "flat": [{"t": "Present population = __B1__", "a": {"B1": "5415"}}], "sol": "6000 × (1 − {5/100})<sup>2</sup> = 6000 × {95/100} × {95/100} = 5415."}, {"kind": "mcq", "text": "<b>Example 23</b> · The cost of a new television set is ₹22,000. Its value depreciates every year at the rate of 20%. What will be the depreciated price after two years?", "opts": ["₹31,680", "₹14,080", "₹13,200", "₹17,600"], "correct": 1, "tag": "", "sol": "22000 × (1 − {20/100})<sup>2</sup> = 22000 × {80/100} × {80/100} = ₹14,080. (₹13,200 takes off 20% of ₹22,000 twice; ₹17,600 is after one year.)"}, {"kind": "blank", "p": "<b>Example 24</b> · The present cost of land per sq. metre is ₹16,000. In the past two years the price increased at the rate of 20% per annum and it is expected to increase at the same rate for the coming two years. What will be the appreciated price after two years?", "tag": "", "marks": "", "flat": [{"t": "Price after two years = ₹__B1__ per m²", "a": {"B1": "23040"}, "accept": ["23,040", "23,040.00", "23040", "23040.00", "inr23,040", "inr23,040.00", "inr23040", "inr23040.00", "rs.23,040", "rs.23,040.00", "rs.23040", "rs.23040.00", "rs23,040", "rs23,040.00", "rs23040", "rs23040.00", "₹23,040", "₹23,040.00", "₹23040", "₹23040.00"]}], "sol": "16000 × ({120/100})<sup>2</sup> = 160 × 12 × 12 = ₹23,040."}, {"kind": "blank", "p": "<b>Example 25</b> · The price of a plot has appreciated at the rate of 20% p.a. during the past two years. Now it costs ₹14,400 per square metre. What was its cost two years ago?", "tag": "", "marks": "", "flat": [{"t": "₹100 two years ago is worth ₹__B1__ now", "a": {"B1": "144"}, "accept": ["144", "144.00", "inr144", "inr144.00", "rs.144", "rs.144.00", "rs144", "rs144.00", "₹144", "₹144.00"]}, {"t": "Cost two years ago = ₹__B1__ per m²", "a": {"B1": "10000"}, "accept": ["10,000", "10,000.00", "10000", "10000.00", "inr10,000", "inr10,000.00", "inr10000", "inr10000.00", "rs.10,000", "rs.10,000.00", "rs.10000", "rs.10000.00", "rs10,000", "rs10,000.00", "rs10000", "rs10000.00", "₹10,000", "₹10,000.00", "₹10000", "₹10000.00"]}], "sol": "100 × 120 × 120 ÷ (100 × 100) = ₹144.\n14400 × 100 ÷ 144 = ₹10,000."}, {"kind": "mcq", "text": "<b>Ex 11E · Q1</b> · The population of a city increases every year at the rate of 10%. If the population now is 12,50,000, what will be the population after 4 years?", "opts": ["18,03,125", "18,30,125", "17,50,000", "16,63,750"], "correct": 1, "tag": "", "sol": "12,50,000 × (1.1)<sup>4</sup> = 12,50,000 × 1.4641 = 18,30,125. (17,50,000 is 10% simple growth; 16,63,750 is after 3 years.)"}, {"kind": "blank", "p": "<b>Ex 11E · Q2</b> · A fast growing town has now about 30,000 cattle. During the last few years, the number of cattle was depleting at the rate of 20% as these were taken to the suburbs. If depletion continues at this rate, what will be the cattle population after three years?", "tag": "", "marks": "", "flat": [{"t": "Cattle after three years = __B1__", "a": {"B1": "15360"}}], "sol": "30000 × ({80/100})<sup>3</sup> = 30000 × 0.512 = 15,360."}, {"kind": "blank", "p": "<b>Ex 11E · Q3</b> · Two years ago, a village had 16,000 people. In the next year, the population increased by 10%. But the next year, due to drought, many people left the village and the population decreased by 18%. What is the present population?", "tag": "", "marks": "", "flat": [{"t": "After the first year: __B1__", "a": {"B1": "17600"}}, {"t": "Present population = __B1__", "a": {"B1": "14432"}}], "sol": "16000 × {110/100} = 17,600.\n17600 × {82/100} = 14,432."}, {"kind": "mcq", "text": "<b>Ex 11E · Q4</b> · The population of a town increases at the rate of 7% every year. If the present population is 90,000, what will it be after two years?", "opts": ["96,300", "1,03,041", "1,02,600", "1,03,410"], "correct": 1, "tag": "", "sol": "90000 × (1.07)<sup>2</sup> = 90000 × 1.1449 = 1,03,041. (1,02,600 uses simple growth.)"}, {"kind": "blank", "p": "<b>Ex 11E · Q5</b> · A village had a population of 25,000 three years ago. During the first, second and third year, the population increased at the rates of 5%, 6% and 8%, respectively. What is the present population of the village?", "tag": "", "marks": "", "flat": [{"t": "Present population = __B1__", "a": {"B1": "30051"}}], "sol": "25000 × {105/100} × {106/100} × {108/100} = 26250 × 1.06 × 1.08 = 27825 × 1.08 = 30,051."}, {"kind": "blank", "p": "<b>Ex 11E · Q6</b> · The population of a village was decreasing every year due to migration, poverty and unemployment. The present population is 3,15,840. Last year the migration rate was 4% and the year before that it was 6%. What was the population two years ago?", "tag": "", "marks": "", "flat": [{"t": "Population two years ago = __B1__", "a": {"B1": "350000"}}], "sol": "P × {94/100} × {96/100} = 315840 ⇒ P = 315840 ÷ 0.9024 = 3,50,000."}, {"kind": "mcq", "text": "<b>Ex 11E · Q7</b> · The price of a plot increases at a constant rate of 5% every year. Find its expected price after 3 years if the present price is ₹2,00,000.", "opts": ["₹2,30,000", "₹2,20,500", "₹2,31,000", "₹2,31,525"], "correct": 3, "tag": "", "sol": "200000 × (1.05)<sup>3</sup> = 200000 × 1.157625 = ₹2,31,525."}, {"kind": "blank", "p": "<b>Ex 11E · Q8</b> · The price of a piece of land increases by 9% every year. If the present price is ₹11,881, what was its price two years ago?", "tag": "", "marks": "", "flat": [{"t": "Price two years ago = ₹__B1__", "a": {"B1": "10000"}, "accept": ["10,000", "10,000.00", "10000", "10000.00", "inr10,000", "inr10,000.00", "inr10000", "inr10000.00", "rs.10,000", "rs.10,000.00", "rs.10000", "rs.10000.00", "rs10,000", "rs10,000.00", "rs10000", "rs10000.00", "₹10,000", "₹10,000.00", "₹10000", "₹10000.00"]}], "sol": "P × ({109/100})<sup>2</sup> = 11881 ⇒ P = 11881 × 10000 ÷ 11881 = ₹10,000."}, {"kind": "blank", "p": "<b>Ex 11E · Q9</b> · A car which costs ₹2,50,000 depreciates by 10% every year. What will the car be worth after three years?", "tag": "", "marks": "", "flat": [{"t": "Value after three years = ₹__B1__", "a": {"B1": "182250"}, "accept": ["1,82,250", "1,82,250.00", "182,250", "182,250.00", "182250", "182250.00", "inr1,82,250", "inr1,82,250.00", "inr182,250", "inr182,250.00", "inr182250", "inr182250.00", "rs.1,82,250", "rs.1,82,250.00", "rs.182,250", "rs.182,250.00", "rs.182250", "rs.182250.00", "rs1,82,250", "rs1,82,250.00", "rs182,250", "rs182,250.00", "rs182250", "rs182250.00", "₹1,82,250", "₹1,82,250.00", "₹182,250", "₹182,250.00", "₹182250", "₹182250.00"]}], "sol": "250000 × ({90/100})<sup>3</sup> = 250000 × 0.729 = ₹1,82,250."}, {"kind": "mcq", "text": "<b>Ex 11E · Q10</b> · A new computer costs ₹60,000. The depreciation is 40% every year. Find the price of the computer after two years.", "opts": ["₹21,600", "₹36,000", "₹12,000", "₹24,000"], "correct": 0, "tag": "", "sol": "60000 × ({60/100})<sup>2</sup> = 60000 × 0.36 = ₹21,600. (₹12,000 takes 40% of ₹60,000 off twice.)"}]}, {"id": "s8", "label": "Assessment A", "sub": "Knowing and understanding", "slides": [{"kind": "mcq", "text": "<b>Check-up · MCQ 1</b> · The compound interest on ₹50,000 at 4% per annum for 2 years compounded annually is ______.", "opts": ["₹4080", "₹4000", "₹4280", "₹4050"], "correct": 0, "tag": "", "sol": "A = 50000 × (1.04)<sup>2</sup> = 50000 × 1.0816 = ₹54,080. CI = ₹4080."}, {"kind": "mcq", "text": "<b>Check-up · MCQ 2</b> · A sum is taken for two years at 16% p.a. If interest is compounded after every three months, the number of times for which interest is charged in 1 year is ______.", "opts": ["9", "8", "6", "4"], "correct": 3, "tag": "", "sol": "Every three months means 12 ÷ 3 = 4 times a year (quarterly). (8 is the number of times in two years.)"}, {"kind": "blank", "p": "<b>Check-up · Q3</b> · Find the simple interest and the amount.\na) ₹560 at 4% p.a. for 73 days\nb) ₹2700 at 9% p.a. for 146 days\nc) ₹10,000 at 12% p.a. for 3.25 years", "tag": "", "marks": "", "flat": [{"t": "a) SI = ₹__B1__", "a": {"B1": "4.48"}, "accept": ["4.48", "inr4.48", "rs.4.48", "rs4.48", "₹4.48"]}, {"t": "a) Amount = ₹__B1__", "a": {"B1": "564.48"}, "accept": ["564.48", "inr564.48", "rs.564.48", "rs564.48", "₹564.48"]}, {"t": "b) SI = ₹__B1__", "a": {"B1": "97.20"}, "accept": ["97.2", "97.20", "inr97.2", "inr97.20", "rs.97.2", "rs.97.20", "rs97.2", "rs97.20", "₹97.2", "₹97.20"]}, {"t": "b) Amount = ₹__B1__", "a": {"B1": "2797.20"}, "accept": ["2,797.2", "2,797.20", "2797.2", "2797.20", "inr2,797.2", "inr2,797.20", "inr2797.2", "inr2797.20", "rs.2,797.2", "rs.2,797.20", "rs.2797.2", "rs.2797.20", "rs2,797.2", "rs2,797.20", "rs2797.2", "rs2797.20", "₹2,797.2", "₹2,797.20", "₹2797.2", "₹2797.20"]}, {"t": "c) SI = ₹__B1__", "a": {"B1": "3900"}, "accept": ["3,900", "3,900.00", "3900", "3900.00", "inr3,900", "inr3,900.00", "inr3900", "inr3900.00", "rs.3,900", "rs.3,900.00", "rs.3900", "rs.3900.00", "rs3,900", "rs3,900.00", "rs3900", "rs3900.00", "₹3,900", "₹3,900.00", "₹3900", "₹3900.00"]}, {"t": "c) Amount = ₹__B1__", "a": {"B1": "13900"}, "accept": ["13,900", "13,900.00", "13900", "13900.00", "inr13,900", "inr13,900.00", "inr13900", "inr13900.00", "rs.13,900", "rs.13,900.00", "rs.13900", "rs.13900.00", "rs13,900", "rs13,900.00", "rs13900", "rs13900.00", "₹13,900", "₹13,900.00", "₹13900", "₹13900.00"]}], "sol": "73 days = {1/5} year: SI = 560 × 4 × {1/5} ÷ 100 = ₹4.48.\nA = 560 + 4.48 = ₹564.48.\n146 days = {2/5} year: SI = 2700 × 9 × {2/5} ÷ 100 = ₹97.20.\nA = 2700 + 97.20 = ₹2797.20.\nSI = 10000 × 12 × 3.25 ÷ 100 = ₹3900.\nA = 10000 + 3900 = ₹13,900."}, {"kind": "blank", "p": "<b>Check-up · Q4</b> · Find the principal.\na) SI ₹392, time 3.5 years, rate 3.5% p.a.\nb) SI ₹4.50, time 5 months, rate 4.5% p.a.", "tag": "", "marks": "", "flat": [{"t": "a) P = ₹__B1__", "a": {"B1": "3200"}, "accept": ["3,200", "3,200.00", "3200", "3200.00", "inr3,200", "inr3,200.00", "inr3200", "inr3200.00", "rs.3,200", "rs.3,200.00", "rs.3200", "rs.3200.00", "rs3,200", "rs3,200.00", "rs3200", "rs3200.00", "₹3,200", "₹3,200.00", "₹3200", "₹3200.00"]}, {"t": "b) P = ₹__B1__", "a": {"B1": "240"}, "accept": ["240", "240.00", "inr240", "inr240.00", "rs.240", "rs.240.00", "rs240", "rs240.00", "₹240", "₹240.00"]}], "sol": "P = 392 × 100 ÷ (3.5 × 3.5) = 39200 ÷ 12.25 = ₹3200.\n5 months = {5/12} year: P = 4.50 × 100 ÷ (4.5 × {5/12}) = 450 × 12 ÷ 22.5 = ₹240."}, {"kind": "mcq", "text": "<b>Check-up · Q5</b> · Find the simple interest and the rate per cent: principal ₹10,000, amount ₹11,800, time 2 years.", "opts": ["SI ₹21,800, rate 9%", "SI ₹1800, rate 18%", "SI ₹1800, rate 8%", "SI ₹1800, rate 9%"], "correct": 3, "tag": "", "sol": "SI = ₹11,800 − ₹10,000 = ₹1800. R = 1800 × 100 ÷ (10000 × 2) = 9%."}, {"kind": "blank", "p": "<b>Check-up · Q6</b> · Find the amount and compound interest (compounded annually; to the nearest paisa).\na) ₹72,000 at 6% p.a. for 3 years\nb) ₹5000 at 9% p.a. for 2 years", "tag": "", "marks": "", "flat": [{"t": "a) Amount = ₹__B1__", "a": {"B1": "85753.15"}, "accept": ["85,753", "85,753.00", "85,753.15", "85,753.152", "85,753.2", "85753", "85753.00", "85753.15", "85753.152", "85753.2", "inr85,753", "inr85,753.00", "inr85,753.15", "inr85,753.152", "inr85,753.2", "inr85753", "inr85753.00", "inr85753.15", "inr85753.152", "inr85753.2", "rs.85,753", "rs.85,753.00", "rs.85,753.15", "rs.85,753.152", "rs.85,753.2", "rs.85753", "rs.85753.00", "rs.85753.15", "rs.85753.152", "rs.85753.2", "rs85,753", "rs85,753.00", "rs85,753.15", "rs85,753.152", "rs85,753.2", "rs85753", "rs85753.00", "rs85753.15", "rs85753.152", "rs85753.2", "₹85,753", "₹85,753.00", "₹85,753.15", "₹85,753.152", "₹85,753.2", "₹85753", "₹85753.00", "₹85753.15", "₹85753.152", "₹85753.2"]}, {"t": "a) CI = ₹__B1__", "a": {"B1": "13753.15"}, "accept": ["13,753", "13,753.00", "13,753.15", "13,753.152", "13,753.2", "13753", "13753.00", "13753.15", "13753.152", "13753.2", "inr13,753", "inr13,753.00", "inr13,753.15", "inr13,753.152", "inr13,753.2", "inr13753", "inr13753.00", "inr13753.15", "inr13753.152", "inr13753.2", "rs.13,753", "rs.13,753.00", "rs.13,753.15", "rs.13,753.152", "rs.13,753.2", "rs.13753", "rs.13753.00", "rs.13753.15", "rs.13753.152", "rs.13753.2", "rs13,753", "rs13,753.00", "rs13,753.15", "rs13,753.152", "rs13,753.2", "rs13753", "rs13753.00", "rs13753.15", "rs13753.152", "rs13753.2", "₹13,753", "₹13,753.00", "₹13,753.15", "₹13,753.152", "₹13,753.2", "₹13753", "₹13753.00", "₹13753.15", "₹13753.152", "₹13753.2"]}, {"t": "b) Amount = ₹__B1__", "a": {"B1": "5940.50"}, "accept": ["5,940.5", "5,940.50", "5940.5", "5940.50", "inr5,940.5", "inr5,940.50", "inr5940.5", "inr5940.50", "rs.5,940.5", "rs.5,940.50", "rs.5940.5", "rs.5940.50", "rs5,940.5", "rs5,940.50", "rs5940.5", "rs5940.50", "₹5,940.5", "₹5,940.50", "₹5940.5", "₹5940.50"]}, {"t": "b) CI = ₹__B1__", "a": {"B1": "940.50"}, "accept": ["940.5", "940.50", "inr940.5", "inr940.50", "rs.940.5", "rs.940.50", "rs940.5", "rs940.50", "₹940.5", "₹940.50"]}], "sol": "A = 72000 × (1.06)<sup>3</sup> = 72000 × 1.191016 = ₹85,753.152 ≈ ₹85,753.15.\nCI = 85753.15 − 72000 = ₹13,753.15.\nA = 5000 × (1.09)<sup>2</sup> = 5000 × 1.1881 = ₹5940.50.\nCI = 5940.50 − 5000 = ₹940.50."}, {"kind": "mcq", "text": "<b>Check-up · Q7(a)</b> · Find the CI on ₹7000 at 10% p.a. compounded annually for 4 years.", "opts": ["₹10,248.70", "₹2800", "₹2317", "₹3248.70"], "correct": 3, "tag": "", "sol": "A = 7000 × (1.1)<sup>4</sup> = 7000 × 1.4641 = ₹10,248.70. CI = ₹3248.70. (₹2800 is the SI; ₹2317 is the CI for 3 years.)"}, {"kind": "blank", "p": "<b>Check-up · Q7(b)</b> · Find the CI on ₹30,000 at 12% p.a. compounded half-yearly for 2 years (to the nearest paisa).", "tag": "", "marks": "", "flat": [{"t": "Number of half-years = __B1__", "a": {"B1": "4"}}, {"t": "Amount = ₹__B1__", "a": {"B1": "37874.31"}, "accept": ["37,874", "37,874.00", "37,874.3", "37,874.3088", "37,874.31", "37874", "37874.00", "37874.3", "37874.3088", "37874.31", "inr37,874", "inr37,874.00", "inr37,874.3", "inr37,874.3088", "inr37,874.31", "inr37874", "inr37874.00", "inr37874.3", "inr37874.3088", "inr37874.31", "rs.37,874", "rs.37,874.00", "rs.37,874.3", "rs.37,874.3088", "rs.37,874.31", "rs.37874", "rs.37874.00", "rs.37874.3", "rs.37874.3088", "rs.37874.31", "rs37,874", "rs37,874.00", "rs37,874.3", "rs37,874.3088", "rs37,874.31", "rs37874", "rs37874.00", "rs37874.3", "rs37874.3088", "rs37874.31", "₹37,874", "₹37,874.00", "₹37,874.3", "₹37,874.3088", "₹37,874.31", "₹37874", "₹37874.00", "₹37874.3", "₹37874.3088", "₹37874.31"]}, {"t": "CI = ₹__B1__", "a": {"B1": "7874.31"}, "accept": ["7,874", "7,874.00", "7,874.3", "7,874.3088", "7,874.31", "7874", "7874.00", "7874.3", "7874.3088", "7874.31", "inr7,874", "inr7,874.00", "inr7,874.3", "inr7,874.3088", "inr7,874.31", "inr7874", "inr7874.00", "inr7874.3", "inr7874.3088", "inr7874.31", "rs.7,874", "rs.7,874.00", "rs.7,874.3", "rs.7,874.3088", "rs.7,874.31", "rs.7874", "rs.7874.00", "rs.7874.3", "rs.7874.3088", "rs.7874.31", "rs7,874", "rs7,874.00", "rs7,874.3", "rs7,874.3088", "rs7,874.31", "rs7874", "rs7874.00", "rs7874.3", "rs7874.3088", "rs7874.31", "₹7,874", "₹7,874.00", "₹7,874.3", "₹7,874.3088", "₹7,874.31", "₹7874", "₹7874.00", "₹7874.3", "₹7874.3088", "₹7874.31"]}], "sol": "2 years = 4 half-years at 6% each.\nA = 30000 × (1.06)<sup>4</sup> = 30000 × 1.26247696 = ₹37,874.3088 ≈ ₹37,874.31.\nCI = 37874.31 − 30000 = ₹7874.31."}]}, {"id": "s9", "label": "Assessment B", "sub": "Investigating patterns", "slides": [{"kind": "blank", "p": "<b>Check-up · Q8</b> · A sum of money amounts to ₹780 in two years and ₹1230 in seven years. Find the principal and rate of simple interest.", "tag": "", "marks": "", "flat": [{"t": "Interest for one year = ₹__B1__", "a": {"B1": "90"}, "accept": ["90", "90.00", "inr90", "inr90.00", "rs.90", "rs.90.00", "rs90", "rs90.00", "₹90", "₹90.00"]}, {"t": "Principal = ₹__B1__", "a": {"B1": "600"}, "accept": ["600", "600.00", "inr600", "inr600.00", "rs.600", "rs.600.00", "rs600", "rs600.00", "₹600", "₹600.00"]}, {"t": "Rate = __B1__ % p.a.", "a": {"B1": "15"}, "accept": ["15%", "15% p.a.", "15%p.a"]}], "sol": "Interest for 7 − 2 = 5 years = 1230 − 780 = ₹450, so ₹90 a year.\nP = 780 − 2 × 90 = ₹600.\nR = 90 × 100 ÷ 600 = 15% p.a."}, {"kind": "mcq", "text": "<b>Check-up · Q9</b> · In how much time will a sum of money double itself if invested at 8% simple interest per annum? (Hint: let the principal be ₹100; the interest will also be ₹100.)", "opts": ["9 years", "{12 1/2} years", "8 years", "{12 1/2} months"], "correct": 1, "tag": "", "sol": "T = SI × 100 ÷ (P × R) = 100 × 100 ÷ (100 × 8) = {25/2} = {12 1/2} years."}, {"kind": "blank", "p": "<b>Check-up · Q13</b> · In how many years will ₹8800 amount to ₹10,648 at 10% p.a. compounded annually?", "tag": "", "marks": "", "flat": [{"t": "{10648/8800} = __B1__ (lowest terms)", "a": {"B1": "121/100"}, "expr": "fl"}, {"t": "t = __B1__ years", "a": {"B1": "2"}, "accept": ["2 years", "2 year", "2 yrs", "2 yr"]}], "sol": "{10648/8800} = {121/100}.\n{121/100} = ({11/10})<sup>2</sup>, so t = 2 years."}, {"kind": "blank", "p": "<b>Check-up · Q14</b> · At what rate % of CI will ₹4000 amount to ₹5324 in three years?", "tag": "", "marks": "", "flat": [{"t": "1 + R/100 = __B1__", "a": {"B1": "11/10"}, "expr": "fv"}, {"t": "R = __B1__ %", "a": {"B1": "10"}, "accept": ["10%", "10% p.a.", "10%p.a"]}], "sol": "{5324/4000} = {1331/1000} = ({11/10})<sup>3</sup>, so 1 + R/100 = {11/10}.\nR/100 = {1/10} ⇒ R = 10% p.a."}, {"kind": "mcq", "text": "<b>Check-up · Q19</b> · A sum of ₹15625 invested at 8% p.a. compounded semi-annually amounts to ₹18279.04. Find the time period.", "opts": ["3 years", "4 years", "{1 1/2} years", "2 years"], "correct": 3, "tag": "", "sol": "Rate per half-year = 4%. 18279.04 ÷ 15625 = 1.16985856 = (1.04)<sup>4</sup>, so there are 4 half-years = 2 years. (4 years mistakes half-years for years.)"}, {"kind": "blank", "p": "<b>Check-up · HOTS 2</b> · In a fixed deposit, a bank gives 10% interest compounded annually for senior citizens. How many complete years will it take for a sum of money to be more than double?", "tag": "", "marks": "", "flat": [{"t": "(1.1)<sup>7</sup> ≈ 1.95 and (1.1)<sup>8</sup> ≈ __B1__ (2 decimal places)", "a": {"B1": "2.14"}}, {"t": "Number of complete years = __B1__", "a": {"B1": "8"}, "accept": ["8 years", "8 year", "8 yrs", "8 yr"]}], "sol": "(1.1)<sup>8</sup> = 2.14358881 ≈ 2.14.\nAfter 7 years the money is 1.9487 times, still less than double; after 8 years it is 2.1436 times, more than double. So 8 years."}, {"kind": "mcq", "text": "<b>Check-up · HOTS 3</b> · The difference between the simple interest and compound interest at the rate of 10% for two years is ₹1. What is the principal?", "opts": ["₹1000", "₹100", "₹10", "₹200"], "correct": 1, "tag": "", "sol": "For 2 years, CI − SI = P × (R/100)<sup>2</sup> = P × {1/100}. P × {1/100} = 1 ⇒ P = ₹100."}, {"kind": "blank", "p": "<b>Shortcut (p. 146)</b> · Rule of 70: the time to double a sum at compound interest is about 70 ÷ rate.", "tag": "", "marks": "", "flat": [{"t": "At 10% p.a., the time to double ≈ __B1__ years", "a": {"B1": "7"}, "accept": ["7 years", "7 year", "7 yrs", "7 yr"]}, {"t": "At 5% p.a., the time to double ≈ __B1__ years", "a": {"B1": "14"}, "accept": ["14 years", "14 year", "14 yrs", "14 yr"]}, {"t": "A machine depreciating at 7% p.a. halves its value in about __B1__ years", "a": {"B1": "10"}, "accept": ["10 years", "10 year", "10 yrs", "10 yr"]}], "sol": "70 ÷ 10 = 7 years (check: 1.1<sup>7</sup> ≈ 1.95).\n70 ÷ 5 = 14 years.\nFor depreciation divide 70 by the rate of depreciation: 70 ÷ 7 = 10 years."}, {"kind": "blank", "p": "Look at how ₹1000 grows at 10% p.a. compounded annually.", "tag": "", "marks": "", "flat": [{"t": "After 1 year: ₹__B1__", "a": {"B1": "1100"}, "accept": ["1,100", "1,100.00", "1100", "1100.00", "inr1,100", "inr1,100.00", "inr1100", "inr1100.00", "rs.1,100", "rs.1,100.00", "rs.1100", "rs.1100.00", "rs1,100", "rs1,100.00", "rs1100", "rs1100.00", "₹1,100", "₹1,100.00", "₹1100", "₹1100.00"]}, {"t": "After 2 years: ₹__B1__", "a": {"B1": "1210"}, "accept": ["1,210", "1,210.00", "1210", "1210.00", "inr1,210", "inr1,210.00", "inr1210", "inr1210.00", "rs.1,210", "rs.1,210.00", "rs.1210", "rs.1210.00", "rs1,210", "rs1,210.00", "rs1210", "rs1210.00", "₹1,210", "₹1,210.00", "₹1210", "₹1210.00"]}, {"t": "After 3 years: ₹__B1__", "a": {"B1": "1331"}, "accept": ["1,331", "1,331.00", "1331", "1331.00", "inr1,331", "inr1,331.00", "inr1331", "inr1331.00", "rs.1,331", "rs.1,331.00", "rs.1331", "rs.1331.00", "rs1,331", "rs1,331.00", "rs1331", "rs1331.00", "₹1,331", "₹1,331.00", "₹1331", "₹1331.00"]}, {"t": "Each amount is the previous amount multiplied by __B1__", "a": {"B1": "1.1"}, "accept": ["11/10"]}], "sol": "1000 × 1.1 = ₹1100.\n1100 × 1.1 = ₹1210.\n1210 × 1.1 = ₹1331.\nThe multiplier 1 + {10/100} = 1.1 is the same every year: this is why A = P(1 + R/100)<sup>t</sup>."}]}, {"id": "s10", "label": "Assessment C", "sub": "Communicating", "slides": [{"kind": "blank", "p": "<b>Check-up · Q10</b> · Rajan borrowed ₹5000 at 8% p.a. for 3 years. Find the difference between compound interest and simple interest, assuming compounded annually.", "tag": "", "marks": "", "flat": [{"t": "SI = ₹__B1__", "a": {"B1": "1200"}, "accept": ["1,200", "1,200.00", "1200", "1200.00", "inr1,200", "inr1,200.00", "inr1200", "inr1200.00", "rs.1,200", "rs.1,200.00", "rs.1200", "rs.1200.00", "rs1,200", "rs1,200.00", "rs1200", "rs1200.00", "₹1,200", "₹1,200.00", "₹1200", "₹1200.00"]}, {"t": "CI = ₹__B1__", "a": {"B1": "1298.56"}, "accept": ["1,298.56", "1298.56", "inr1,298.56", "inr1298.56", "rs.1,298.56", "rs.1298.56", "rs1,298.56", "rs1298.56", "₹1,298.56", "₹1298.56"]}, {"t": "Difference = ₹__B1__", "a": {"B1": "98.56"}, "accept": ["98.56", "inr98.56", "rs.98.56", "rs98.56", "₹98.56"]}], "sol": "SI = 5000 × 8 × 3 ÷ 100 = ₹1200.\nA = 5000 × (1.08)<sup>3</sup> = ₹6298.56; CI = ₹1298.56.\n1298.56 − 1200 = ₹98.56."}, {"kind": "mcq", "text": "<b>Check-up · Q15</b> · Calculate the compound interest on ₹20,000 for {1 1/2} years at the rate of 10% per annum compounded semi-annually. Which working is correct?", "opts": ["10% per half-year for 3 periods: 20000 × (1.1)<sup>3</sup> − 20000 = ₹6620", "5% per half-year for 3 periods: 20000 × (1.05)<sup>3</sup> − 20000 = ₹3152.50", "5% per half-year for 2 periods: 20000 × (1.05)<sup>2</sup> − 20000 = ₹2050", "10% for {1 1/2} years simple: 20000 × 10 × 1.5 ÷ 100 = ₹3000"], "correct": 1, "tag": "", "sol": "Half-yearly: halve the rate (5%) and double the time (3 half-years). A = 20000 × 1.157625 = ₹23,152.50, so CI = ₹3152.50."}, {"kind": "blank", "p": "<b>Check-up · Q16</b> · Find the compound interest on ₹1,60,000 for 2 years at 10% per annum, compounded semi-annually.", "tag": "", "marks": "", "flat": [{"t": "Rate per half-year = __B1__ % and number of periods = __B2__", "a": {"B1": "5", "B2": "4"}}, {"t": "CI = ₹__B1__", "a": {"B1": "34481"}, "accept": ["34,481", "34,481.00", "34481", "34481.00", "inr34,481", "inr34,481.00", "inr34481", "inr34481.00", "rs.34,481", "rs.34,481.00", "rs.34481", "rs.34481.00", "rs34,481", "rs34,481.00", "rs34481", "rs34481.00", "₹34,481", "₹34,481.00", "₹34481", "₹34481.00"]}], "sol": "10% ÷ 2 = 5% per half-year; 2 years = 4 half-years.\nA = 160000 × (1.05)<sup>4</sup> = 160000 × 1.21550625 = ₹1,94,481; CI = ₹34,481."}, {"kind": "mcq", "text": "Ravi works out the compound interest on ₹5000 at 8% p.a. for 2 years as 5000 × 8 × 2 ÷ 100 = ₹800. What is wrong?", "opts": ["Nothing is wrong; for 2 years CI and SI are always equal, so CI = ₹800", "He should divide by 200 instead of 100, so CI = ₹400", "He should use 4% for 4 half-years, so CI = 5000 × 1.04⁴ − ₹5000 = ₹849.29", "He found SI; the second year’s interest is on ₹5400, so CI = ₹832"], "correct": 3, "tag": "", "sol": "The second year’s interest is on ₹5400: 5400 × 8 ÷ 100 = ₹432. CI = 400 + 432 = ₹832 (= 5000 × 1.08² − 5000). CI and SI are equal only for the first conversion period."}, {"kind": "blank", "p": "Explain the compound interest formula for depreciation. A machine worth ₹P loses R% of its value every year.", "tag": "", "marks": "", "flat": [{"t": "Each year the value is multiplied by (1 __B1__ R/100) (type + or −).", "a": {"B1": "−"}, "accept": ["-", "minus"]}, {"t": "A machine worth ₹50,000 depreciating at 10% p.a. is worth ₹__B1__ after 2 years", "a": {"B1": "40500"}, "accept": ["40,500", "40,500.00", "40500", "40500.00", "inr40,500", "inr40,500.00", "inr40500", "inr40500.00", "rs.40,500", "rs.40,500.00", "rs.40500", "rs.40500.00", "rs40,500", "rs40,500.00", "rs40500", "rs40500.00", "₹40,500", "₹40,500.00", "₹40500", "₹40500.00"]}], "sol": "Depreciation lowers the value, so the factor is (1 − R/100).\n50000 × 0.9 × 0.9 = ₹40,500."}, {"kind": "mcq", "text": "<b>Check-up · Being Indian (c)</b> · Blood donation is a noble cause. Is it important to donate blood? Why?", "opts": ["Yes: blood cannot be manufactured, so accident and surgery patients depend on donors", "Yes, but only because every donor is paid a large amount of money for it", "No: a healthy donor’s body can never replace the blood that is given", "No: hospitals can manufacture enough blood in factories whenever they need it"], "correct": 0, "tag": "", "sol": "Blood cannot be manufactured; patients in accidents, surgeries, childbirth and illnesses such as thalassaemia depend on donors. A healthy adult’s body replaces the donated blood within weeks."}, {"kind": "mcq", "text": "Which statement about compound interest is correct?", "opts": ["CI is always less than SI", "For the first conversion period, CI equals SI; after that CI is greater", "CI and SI are equal for every time period", "CI is greater than SI even for the first conversion period"], "correct": 1, "tag": "", "sol": "In the first period both are interest on the same principal. After that, compound interest also earns interest on the earlier interest, so it is larger."}, {"kind": "blank", "p": "For 2 years at R% compounded annually, CI − SI = P × (R/100)<sup>2</sup>. Use it for ₹5000 at 10%.", "tag": "", "marks": "", "flat": [{"t": "CI − SI = ₹__B1__", "a": {"B1": "50"}, "accept": ["50", "50.00", "inr50", "inr50.00", "rs.50", "rs.50.00", "rs50", "rs50.00", "₹50", "₹50.00"]}, {"t": "Check: CI = ₹__B1__", "a": {"B1": "1050"}, "accept": ["1,050", "1,050.00", "1050", "1050.00", "inr1,050", "inr1,050.00", "inr1050", "inr1050.00", "rs.1,050", "rs.1,050.00", "rs.1050", "rs.1050.00", "rs1,050", "rs1,050.00", "rs1050", "rs1050.00", "₹1,050", "₹1,050.00", "₹1050", "₹1050.00"]}], "sol": "5000 × ({10/100})<sup>2</sup> = 5000 × {1/100} = ₹50.\nA = 5000 × 1.21 = ₹6050, CI = ₹1050 and SI = ₹1000; the difference is ₹50."}]}, {"id": "s11", "label": "Assessment D", "sub": "Applying mathematics in real-life contexts", "slides": [{"kind": "blank", "p": "<b>Check-up · Q11</b> · Aashna deposited ₹12,000 in a bank for 2 years. It is compounded annually at 9% p.a. What amount will she receive on maturity (at the end of 2 years)?", "tag": "", "marks": "", "flat": [{"t": "Amount = ₹__B1__", "a": {"B1": "14257.20"}, "accept": ["14,257.2", "14,257.20", "14257.2", "14257.20", "inr14,257.2", "inr14,257.20", "inr14257.2", "inr14257.20", "rs.14,257.2", "rs.14,257.20", "rs.14257.2", "rs.14257.20", "rs14,257.2", "rs14,257.20", "rs14257.2", "rs14257.20", "₹14,257.2", "₹14,257.20", "₹14257.2", "₹14257.20"]}], "sol": "A = 12000 × (1.09)<sup>2</sup> = 12000 × 1.1881 = ₹14,257.20."}, {"kind": "mcq", "text": "<b>Check-up · Q12</b> · Find the principal if it amounts to ₹16,335 compounded annually at the rate of 10% p.a. in two years.", "opts": ["₹13,500", "₹13,612.50", "₹13,200", "₹14,850"], "correct": 0, "tag": "", "sol": "P = 16335 ÷ (1.1)<sup>2</sup> = 16335 ÷ 1.21 = ₹13,500. (₹13,612.50 uses simple interest.)"}, {"kind": "blank", "p": "<b>Check-up · Q17</b> · The population of a town increases 4% annually. If the present population is 54,080, what was the population two years ago?", "tag": "", "marks": "", "flat": [{"t": "Population two years ago = __B1__", "a": {"B1": "50000"}}], "sol": "P × (1.04)<sup>2</sup> = 54080 ⇒ P = 54080 ÷ 1.0816 = 50,000."}, {"kind": "blank", "p": "<b>Check-up · Q18</b> · In the year 2019, the number of malaria patients admitted in the hospitals of a state was 4375. Every year this number decreases by 8%. Find the number of patients in 2021.", "tag": "", "marks": "", "flat": [{"t": "Patients in 2021 = __B1__", "a": {"B1": "3703"}}], "sol": "2019 to 2021 is 2 years: 4375 × (0.92)<sup>2</sup> = 4375 × 0.8464 = 3703."}, {"kind": "mcq", "text": "<b>Check-up · Case Study Q20(a)</b> · Meera bought a used sewing machine for ₹8664. According to the original bill it was purchased for ₹9600. If the sewing machine is 2 years old, then its value depreciated at", "opts": ["7% p.a.", "5% p.a.", "6.2% p.a.", "4.5% p.a."], "correct": 1, "tag": "", "sol": "9600 × (1 − R/100)<sup>2</sup> = 8664 ⇒ (1 − R/100)<sup>2</sup> = {8664/9600} = 0.9025 = (0.95)<sup>2</sup> ⇒ R = 5%."}, {"kind": "mcq", "text": "<b>Check-up · Case Study Q20(b)</b> · Meera (bought the machine for ₹8664; original price ₹9600 two years earlier) sold the sewing machine after one year. If the rate of depreciation remains the same, then Meera lost ______ on the transaction.", "opts": ["₹866.40", "₹433.20", "₹1020.55", "₹768.50"], "correct": 1, "tag": "", "sol": "Value after one more year = 8664 × 0.95 = ₹8230.80. Loss = 8664 − 8230.80 = ₹433.20. (The rate from part a: (1 − R/100)<sup>2</sup> = {8664/9600} = 0.9025 = (0.95)<sup>2</sup>, so R = 5%.)"}, {"kind": "blank", "p": "<b>Check-up · Everyday Maths Q21</b> · The population of a town is 50,000. If the annual emigration rate is 6% and the annual immigration rate is 4%, calculate the population after two years.", "tag": "", "marks": "", "flat": [{"t": "Net change each year = __B1__ % (use − for a decrease)", "a": {"B1": "-2"}, "accept": ["-2%", "−2%", "−2"]}, {"t": "Population after two years = __B1__", "a": {"B1": "48020"}}], "sol": "6% leave and 4% arrive: a net decrease of 2% a year.\n50000 × (1 − {2/100})<sup>2</sup> = 50000 × 0.9604 = 48,020."}, {"kind": "mcq", "text": "<b>Check-up · HOTS 1</b> · The value of a car depreciates at the rate of 10% per year. A car which was bought three years back is now worth ₹4,73,850. What was its original price?", "opts": ["₹6,76,929", "₹6,50,000", "₹6,16,005", "₹5,85,000"], "correct": 1, "tag": "", "sol": "P × (0.9)<sup>3</sup> = 473850 ⇒ P = 473850 ÷ 0.729 = ₹6,50,000. (₹6,16,005 just adds 30% to today’s value; ₹6,76,929 divides by 0.7 as if the loss were simple; ₹5,85,000 goes back only 2 years.)"}, {"kind": "blank", "p": "<b>Check-up · Everyday Maths Q22</b> · The present cost of a mobile phone is ₹15000. If its value decreases every year by 5%, find its cost 2 years ago (to the nearest paisa).", "tag": "", "marks": "", "flat": [{"t": "Cost 2 years ago = ₹__B1__", "a": {"B1": "16620.50"}, "accept": ["16,620", "16,620.00", "16,620.498", "16,620.4986", "16,620.5", "16,620.50", "16620", "16620.00", "16620.498", "16620.4986", "16620.5", "16620.50", "inr16,620", "inr16,620.00", "inr16,620.498", "inr16,620.4986", "inr16,620.5", "inr16,620.50", "inr16620", "inr16620.00", "inr16620.498", "inr16620.4986", "inr16620.5", "inr16620.50", "rs.16,620", "rs.16,620.00", "rs.16,620.498", "rs.16,620.4986", "rs.16,620.5", "rs.16,620.50", "rs.16620", "rs.16620.00", "rs.16620.498", "rs.16620.4986", "rs.16620.5", "rs.16620.50", "rs16,620", "rs16,620.00", "rs16,620.498", "rs16,620.4986", "rs16,620.5", "rs16,620.50", "rs16620", "rs16620.00", "rs16620.498", "rs16620.4986", "rs16620.5", "rs16620.50", "₹16,620", "₹16,620.00", "₹16,620.498", "₹16,620.4986", "₹16,620.5", "₹16,620.50", "₹16620", "₹16620.00", "₹16620.498", "₹16620.4986", "₹16620.5", "₹16620.50"]}], "sol": "P × (0.95)<sup>2</sup> = 15000 ⇒ P = 15000 ÷ 0.9025 = ₹16,620.4986… ≈ ₹16,620.50."}, {"kind": "blank", "p": "<b>Check-up · Being Indian (a, b)</b> · At a blood donation camp in an area, 1500 people donated blood last year.", "tag": "", "marks": "", "flat": [{"t": "a) If the number increased by 5% this year, donors this year = __B1__", "a": {"B1": "1575"}}, {"t": "b) If it rises by 8% next year, donors next year = __B1__", "a": {"B1": "1701"}}], "sol": "1500 × {105/100} = 1575.\n1575 × {108/100} = 1701."}]}];
/* ================= build slide lists ================= */
var SLIDES = {}; SECTIONS.forEach(function(sec){ SLIDES[sec.id]=sec.slides; });
var TAB_DEFS = SECTIONS.map(function(sec){ return {id:sec.id, label:sec.label, sub:sec.sub}; });

/* ================= state ================= */
function blankItem(slide){
  if(slide.kind==='mcq'||slide.kind==='ar'){
    return {status:'unanswered', attempts:0, choice:undefined};
  }
  return {status:'unanswered', curStep:0, stepStates: slide.flat.map(function(){ return {status:'unanswered', attempts:0, inputs:{}}; })};
}
function defaultState(){
  var s={tabs:{}};
  TAB_DEFS.forEach(function(td){
    s.tabs[td.id] = { idx:0, maxReached:0, items: SLIDES[td.id].map(function(sl){ return blankItem(sl); }) };
  });
  return s;
}
var appState = {mode:null, learning:null, quiz:null};
var state = null;      // alias for appState[appState.mode]
var MODE = null;
var activeTab=TAB_DEFS[0].id;

function setMode(m){
  appState.mode = m;
  if(!appState[m]) appState[m] = defaultState();
  state = appState[m];
  MODE = m;
}
/* ================= student accounts (saved on this device) ================= */
var SHEET_KEY='sopaan-c8-ch11';
var ACC_KEY='sopaan-students-v1';
var storageOK=true;
var MEM={};
function lsGet(k){ var r=null; try{ r=localStorage.getItem(k); }catch(e){ storageOK=false; }
  if(r===null||r===undefined) r=MEM[k]||null; try{ return r?JSON.parse(r):null; }catch(e){ return null; } }
function lsSet(k,v){ var j=JSON.stringify(v); MEM[k]=j; try{ localStorage.setItem(k,j); return true; }catch(e){ storageOK=false; return false; } }
try{ localStorage.setItem('sopaan-probe','1'); localStorage.removeItem('sopaan-probe'); }catch(e){ storageOK=false; }
function hashPin(pin,salt){ var h=2166136261, str=salt+'|'+pin; for(var i=0;i<str.length;i++){ h^=str.charCodeAt(i); h=Math.imul(h,16777619)>>>0; } return h.toString(36); }
function accKey(name,roll){ return (name.trim().toLowerCase().replace(/\s+/g,' ')+'#'+roll.trim().toLowerCase()); }
function accounts(){ return lsGet(ACC_KEY)||{students:{}}; }
var student=null; // {key,name,roll}
var records=[];   // finished-tab history for this student on this sheet
function progKey(){ return SHEET_KEY+'::'+student.key; }

function loadState(){
  appState = {mode:null, learning:null, quiz:null}; records=[]; activeTab=TAB_DEFS[0].id;
  var saved=lsGet(progKey());
  if(!saved) return;
  try{
    ['learning','quiz'].forEach(function(m){
      if(saved[m] && saved[m].tabs){
        var fresh = defaultState();
        TAB_DEFS.forEach(function(td){
          if(saved[m].tabs[td.id] && saved[m].tabs[td.id].items && saved[m].tabs[td.id].items.length===SLIDES[td.id].length){
            fresh.tabs[td.id] = saved[m].tabs[td.id];
          }
        });
        appState[m] = fresh;
      }
    });
    if(saved.mode==='learning' || saved.mode==='quiz') appState.mode = saved.mode;
    if(saved.activeTab && TAB_DEFS.some(function(t){ return t.id===saved.activeTab; })) activeTab = saved.activeTab;
    if(Array.isArray(saved.records)) records = saved.records;
  }catch(e){}
}
function saveState(){
  if(!student) return;
  lsSet(progKey(), {mode:appState.mode, learning:appState.learning, quiz:appState.quiz, activeTab:activeTab, records:records, updated:Date.now()});
  var acc=accounts(); if(acc.students[student.key]){ acc.students[student.key].last=Date.now(); lsSet(ACC_KEY,acc); }
}
function addRecord(mode, tabId, correct, revealed, skipped, total){
  records.unshift({at:Date.now(), mode:mode, tab:tabId, correct:correct, revealed:revealed, skipped:skipped, total:total});
  if(records.length>60) records.length=60;
  saveState();
}
function fmtDate(ms){ try{ return new Date(ms).toLocaleString(undefined,{day:'numeric',month:'short',hour:'2-digit',minute:'2-digit'}); }catch(e){ return ''; } }

function renderWho(){
  var el=document.getElementById('whoBar');
  if(!student){ el.hidden=true; el.innerHTML=''; return; }
  el.hidden=false;
  el.innerHTML='Signed in as <b>'+esc(student.name)+'</b> · Roll '+esc(student.roll)+
    ' <button id="btnRecord">My record</button> <button id="btnSignOut">Sign out</button>';
  document.getElementById('btnRecord').addEventListener('click', renderRecord);
  document.getElementById('btnSignOut').addEventListener('click', signOut);
}
function signOut(){
  saveState(); student=null; state=null; MODE=null;
  var acc=accounts(); delete acc.current; lsSet(ACC_KEY,acc);
  document.getElementById('modePill').hidden=true;
  renderWho(); renderLogin();
}
function signIn(key){
  var acc=accounts(); var st=acc.students[key]; if(!st) return;
  student={key:key, name:st.name, roll:st.roll};
  acc.current=key; st.last=Date.now(); lsSet(ACC_KEY,acc);
  loadState(); renderWho();
  if(appState.mode==='learning' || appState.mode==='quiz'){
    setMode(appState.mode); document.getElementById('modePill').hidden=false; updateModePill();
    showChrome(true); buildTabbar(); renderSlide();
    showToast('Welcome back, '+st.name.split(' ')[0]+'. Picking up where you left off.');
  } else {
    renderModePicker();
  }
}
function renderLogin(msg){
  showChrome(false);
  var acc=accounts(); var keys=Object.keys(acc.students).sort(function(a,b){ return (acc.students[b].last||0)-(acc.students[a].last||0); });
  var h='<div class="login-card"><h2>Student sign-in</h2>'+
    '<p class="lead">Sign in to save your answers, see your record and continue where you left off next time.</p>';
  if(!storageOK) h+='<div class="login-err">This browser is blocking saved data (for example, a private window). You can still practise, but progress will not be kept after you close the page.</div>';
  if(msg) h+='<div class="login-err">'+esc(msg)+'</div>';
  if(keys.length){
    h+='<div class="known"><span class="known-label">Continue as</span>';
    keys.slice(0,6).forEach(function(k){ var st=acc.students[k];
      h+='<button class="known-btn" data-k="'+esc(k)+'"><span>'+esc(st.name)+' <small>· Roll '+esc(st.roll)+'</small></span><small>'+(st.last?'Last active '+fmtDate(st.last):'')+'</small></button>'; });
    h+='</div>';
  }
  h+='<form id="loginForm" novalidate>'+
    '<div class="fld"><label for="lgName">Full name</label><input id="lgName" autocomplete="name" required></div>'+
    '<div class="fld-row"><div class="fld"><label for="lgRoll">Roll no.</label><input id="lgRoll" required></div>'+
    '<div class="fld"><label for="lgPin">4-digit PIN</label><input id="lgPin" type="password" inputmode="numeric" maxlength="4" autocomplete="off" required></div></div>'+
    '<button class="btn btn-primary" type="submit" style="width:100%;">Sign in</button>'+
    '<p class="login-note">New here? Enter your name, roll no. and a PIN you will remember, and your profile is created. Progress is saved on this device, so use the same device and browser to continue.</p>'+
    '</form></div>';
  var wrap=document.getElementById('wrap'); wrap.innerHTML=h;
  wrap.querySelectorAll('.known-btn').forEach(function(b){
    b.addEventListener('click', function(){
      var st=accounts().students[b.dataset.k];
      document.getElementById('lgName').value=st.name; document.getElementById('lgRoll').value=st.roll;
      document.getElementById('lgPin').focus();
    });
  });
  document.getElementById('loginForm').addEventListener('submit', function(e){
    e.preventDefault();
    var name=document.getElementById('lgName').value.trim(), roll=document.getElementById('lgRoll').value.trim(), pin=document.getElementById('lgPin').value.trim();
    if(!name||!roll){ renderLoginErr('Enter your name and roll no.'); return; }
    if(!/^\d{4}$/.test(pin)){ renderLoginErr('Your PIN must be exactly 4 digits.'); return; }
    var k=accKey(name,roll); var acc=accounts();
    if(acc.students[k]){
      if(acc.students[k].pin!==hashPin(pin,k)){ renderLoginErr('That PIN does not match this name and roll no. Try again.'); return; }
    } else {
      acc.students[k]={name:name.replace(/\s+/g,' '), roll:roll, pin:hashPin(pin,k), created:Date.now()};
      lsSet(ACC_KEY,acc);
    }
    signIn(k);
  });
}
function renderLoginErr(m){
  var n=document.getElementById('lgName').value, r=document.getElementById('lgRoll').value;
  renderLogin(m); document.getElementById('lgName').value=n; document.getElementById('lgRoll').value=r; document.getElementById('lgPin').focus();
}
function tabSummary(m){
  var st=appState[m]; if(!st) return null;
  return TAB_DEFS.map(function(td){
    var items=st.tabs[td.id].items, n=items.length;
    var c=items.filter(function(i){return i.status==='correct';}).length;
    var done=items.filter(function(i){return i.status!=='unanswered';}).length;
    return {label:td.label, n:n, done:done, correct:c};
  });
}
function renderRecord(){
  showChrome(false);
  var tabLabel=function(id){ var t=TAB_DEFS.find(function(x){return x.id===id;}); return t?t.label:id; };
  var h='<div class="rec-card"><h2>'+esc(student.name)+'’s record</h2><p class="rec-empty" style="margin:0 0 12px;">Roll '+esc(student.roll)+' · Simple and Compound Interest</p>';
  ['learning','quiz'].forEach(function(m){
    var sum=tabSummary(m);
    h+='<h3>'+(m==='learning'?'📘 Learning Sheet':'📝 Quiz Mode')+'</h3>';
    if(!sum){ h+='<p class="rec-empty">Not started yet.</p>'; return; }
    h+='<div class="rec-table-wrap"><table class="rec-table"><thead><tr><th>Section</th><th>Progress</th><th>Correct first time</th></tr></thead><tbody>';
    sum.forEach(function(r){ var pct=Math.round(r.done/r.n*100);
      h+='<tr><td>'+r.label+'</td><td><span class="rec-bar"><i style="width:'+pct+'%"></i></span>'+r.done+' / '+r.n+'</td><td>'+(m==='quiz'?'—':r.correct+' / '+r.n)+'</td></tr>'; });
    h+='</tbody></table></div>';
  });
  h+='</div><div class="rec-card"><h3>Finished sections</h3>';
  if(!records.length){ h+='<p class="rec-empty">No sections finished yet. Each time you finish a tab, your score is recorded here.</p>'; }
  else {
    h+='<div class="rec-table-wrap"><table class="rec-table"><thead><tr><th>When</th><th>Mode</th><th>Section</th><th>Score</th></tr></thead><tbody>';
    records.forEach(function(r){ h+='<tr><td>'+fmtDate(r.at)+'</td><td>'+(r.mode==='quiz'?'Quiz':'Learning')+'</td><td>'+tabLabel(r.tab)+'</td><td>'+r.correct+' / '+r.total+(r.mode==='learning'?' <span class="rec-empty">('+r.revealed+' revealed, '+r.skipped+' skipped)</span>':'')+'</td></tr>'; });
    h+='</tbody></table></div>';
  }
  h+='</div><button class="btn btn-primary" id="btnBack">'+(MODE?'Back to practice':'Choose a mode')+'</button>';
  document.getElementById('wrap').innerHTML=h;
  document.getElementById('btnBack').addEventListener('click', function(){
    if(MODE){ showChrome(true); buildTabbar(); renderSlide(); } else renderModePicker();
  });
  window.scrollTo({top:0});
}

/* ================= tab bar ================= */
function buildTabbar(){
  var el=document.getElementById('tabbar');
  el.innerHTML = '<button class="tab-btn'+(activeTab==='theory'?' active':'')+'" data-tab="theory">Theory<span class="tab-count">notes</span></button>' + TAB_DEFS.map(function(t){
    return '<button class="tab-btn'+(t.id===activeTab?' active':'')+'" data-tab="'+t.id+'">'+t.label+'<span class="tab-count">'+SLIDES[t.id].length+'</span></button>';
  }).join('') + '<button class="tab-btn'+(activeTab==='report'?' active':'')+'" data-tab="report">📊 Report<span class="tab-count">pie</span></button>';
  el.querySelectorAll('.tab-btn').forEach(function(btn){
    btn.addEventListener('click', function(){ activeTab=btn.dataset.tab; buildTabbar(); renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); });
  });
}

/* ================= rendering ================= */
function canProceed(item){ return item.status==='correct'||item.status==='revealed'||item.status==='skipped'; }

function renderSlide(){
  if(!state.tabs[activeTab]){ activeTab=TAB_DEFS[0].id; }
  var ts = state.tabs[activeTab];
  var slides = SLIDES[activeTab];
  if(ts.idx>=slides.length||ts.idx<0) ts.idx=0;
  var idx = ts.idx;
  var slide = slides[idx];
  var item = ts.items[idx];

  var tdef=TAB_DEFS.find(function(t){return t.id===activeTab;});
  document.getElementById('spLabel').textContent = tdef.label+' · Question '+(idx+1)+' of '+slides.length;
  document.getElementById('secSub').textContent = tdef.label+' — '+tdef.sub;
  document.getElementById('spFill').style.width = Math.round(((idx)/(Math.max(slides.length-1,1)))*100)+'%';

  var h='<div class="qcard">';
  if(slide.kind==='mcq' || slide.kind==='ar'){
    h += renderChoiceBody(slide, item, idx);
  } else {
    h += renderBlankBody(slide, item, idx);
  }
  h += '<div class="feedback" id="feedbackBox"></div>';
  if(MODE==='learning' && (item.status==='correct'||item.status==='revealed')) h += solutionHTML(slide);
  h += '</div>';

  document.getElementById('wrap').innerHTML = h;
  wireSlideEvents(slide, item, idx);
  restoreFeedback(item);
  renderNavbar(item);
  updateFab();
  saveState();
}

function solutionHTML(slide){
  if(!slide.sol) return '';
  return '<div class="solution"><div class="sol-h">Solution</div>'+slide.sol.split('\n').map(function(l){ return '<div class="sol-line">'+fr(esc(l))+'</div>'; }).join('')+'</div>';
}
var LETTERS=['a','b','c','d','e','f'];
function chosenHTML(slide,item){
  var opts = slide.kind==='mcq' ? slide.opts : AR_OPTIONS;
  if(item.choice===undefined) return '';
  var ok=item.choice===slide.correct;
  var h='<div class="chosen '+(ok?'ok':'bad')+'"><b>Your answer:</b> ('+LETTERS[item.choice]+') '+fr(esc(opts[item.choice]))+(ok?' ✓':' ✗')+'</div>';
  if(!ok) h+='<div class="chosen ok"><b>Correct answer:</b> ('+LETTERS[slide.correct]+') '+fr(esc(opts[slide.correct]))+'</div>';
  return h;
}
function renderChoiceBody(slide, item, idx){
  var h='<div class="qhead"><div class="qnum">'+(idx+1)+'</div>';
  if(slide.kind==='mcq'){
    h += '<div class="qtext">'+fr(esc(slide.text))+(slide.tag?'<span class="qtag">'+esc(slide.tag)+'</span>':'')+'</div>';
  } else {
    h += '<div class="qtext"><span class="qtag" style="margin-left:0;margin-right:6px;">A / R</span>Assertion (A): '+fr(esc(slide.a))+'<br>Reason (R): '+fr(esc(slide.r))+(slide.tag?'<span class="qtag">'+esc(slide.tag)+'</span>':'')+'</div>';
  }
  h += '</div>';
  if(slide.fig) h += '<div class="fig">'+slide.fig+'</div>';
  var opts = slide.kind==='mcq' ? slide.opts : AR_OPTIONS;
  if(MODE==='quiz') h += '<div class="quiz-hint">Quiz mode — pick an option. The correct answer is revealed once you finish this tab.</div>';
  var locked = MODE==='learning' && (item.status==='correct' || item.status==='revealed');
  h += '<div class="options">';
  opts.forEach(function(opt,i){
    var cls='opt';
    if(locked){
      if(i===slide.correct) cls+=' is-correct';
      else if(item.choice===i) cls+=' is-wrong';
      cls+=' locked';
    }
    if(item.choice===i) cls+=' is-chosen';
    h += '<label class="'+cls+'"><input type="radio" name="choice" value="'+i+'" '+(item.choice===i?'checked':'')+' '+(locked?'disabled':'')+'> <span class="opt-l">('+LETTERS[i]+')</span> <span class="opt-t">'+fr(esc(opt))+'</span>'+(item.choice===i?'<span class="opt-tag">'+(locked?(i===slide.correct?'Your answer ✓':'Your answer ✗'):'Selected')+'</span>':'')+'</label>';
  });
  h += '</div>';
  if(locked) h += chosenHTML(slide,item);
  return h;
}

function renderBlankBody(slide, item, idx){
  var h='<div class="qhead"><div class="qnum">'+(idx+1)+'</div><div class="qtext">';
  if(slide.kind==='case'){ h += '<b>'+esc(slide.title)+'.</b> '+esc(slide.body); }
  else { var pp=fr(esc(slide.p)).split('\n'); h += pp[0]+pp.slice(1).map(function(x){return '<span class="datline">'+x+'</span>';}).join(''); }
  h += (slide.tag?'<span class="qtag">'+esc(slide.tag)+'</span>':'')+'</div>';
  if(slide.marks) h += '<div class="marks-pill">'+slide.marks+'</div>';
  h += '</div>';
  if(slide.fig) h += '<div class="fig">'+slide.fig+'</div>';

  var total = slide.flat.length;
  var hasExpr = slide.flat.some(function(s){ return s.expr===true; });
  var hasFrac = slide.flat.some(function(s){ return ['fv','fe','fl','fm','fi','flist'].indexOf(s.expr)>=0; });
  var blankCount=0; slide.flat.forEach(function(s){ blankCount+=Object.keys(s.a).length; });

  if(MODE==='quiz'){
    h += '<div class="step-badge">'+blankCount+' blank'+(blankCount===1?'':'s')+' in this question</div>';
    h += '<div class="quiz-hint">Quiz mode — fill in what you can. Correct answers are revealed once you finish this tab.</div>';
    if(hasFrac) h += '<div class="quiz-hint">Type fractions like <b>3/4</b> and mixed numbers like <b>2 3/4</b> (whole number, space, fraction).</div>';
    if(hasExpr) h += '<div class="quiz-hint">Type answers like <b>2x-5</b>, <b>x^2-4</b> or <b>3+2i</b>. Use ^ for powers, | | for absolute value and pi for π. Any equivalent form is accepted.</div>';
    h += '<div class="steps">';
    for(var qi=0; qi<total; qi++){
      var qstep = slide.flat[qi];
      var qss = item.stepStates[qi];
      if(qstep.partLabel) h += '<div class="subpart-label">'+esc(qstep.partLabel)+'</div>';
      if(qstep.orDivider) h += '<div class="or-divider">OR</div>';
      var qline = fr(qstep.t);
      Object.keys(qstep.a).forEach(function(bkey){
        var val = qss.inputs[bkey]||'';
        var inp='<input class="blank-input'+(['fv','fe','fl','fm','fi','dec'].indexOf(qstep.expr)>=0?' fr':(qstep.expr==='flist'||qstep.expr==='dlist'||qstep.expr==='glist')?' wide':qstep.expr===true?' expr':(qstep.expr==='words'||qstep.expr==='list'||qstep.expr==='expanded'||qstep.expr==='set'||qstep.expr==='primes'||qstep.expr==='trans'||qstep.expr==='rot'?' wide':''))+'" data-step="'+qi+'" data-bkey="'+bkey+'" value="'+esc(val)+'">';
        qline = qline.replace('__'+bkey+'__', inp);
      });
      if(qstep.fig) h += '<div class="fig">'+qstep.fig+'</div>';
      h += '<div class="step-line">'+qline+'</div>';
    }
    h += '</div>';
    return h;
  }

  if(hasFrac) h += '<div class="quiz-hint">Type fractions like <b>3/4</b> and mixed numbers like <b>2 3/4</b> (whole number, space, fraction).</div>';
  if(hasExpr) h += '<div class="quiz-hint">Type answers like <b>2x-5</b>, <b>x^2-4</b> or <b>3+2i</b>. Use ^ for powers, | | for absolute value and pi for π. Any equivalent form is accepted.</div>';
  var locked = item.status==='correct' || item.status==='revealed';
  var upto = locked ? total-1 : item.curStep;
  h += '<div class="step-badge">Step '+(Math.min(item.curStep,total-1)+1)+' of '+total+'</div>';
  h += '<div class="steps">';
  for(var i=0;i<=upto;i++){
    var step = slide.flat[i];
    var ss = item.stepStates[i];
    if(step.partLabel) h += '<div class="subpart-label">'+esc(step.partLabel)+'</div>';
    if(step.orDivider) h += '<div class="or-divider">OR</div>';
    var resolved = ss.status==='correct' || ss.status==='revealed';
    var line = fr(step.t);
    Object.keys(step.a).forEach(function(bkey){
      var fs = ss.inputs['fs_'+bkey];
      var cls = fs==='correct'?'is-correct':(fs==='wrong'?'is-wrong':'');
      var val = ss.inputs[bkey]||'';
      var dis = resolved ? 'disabled':'';
      var inp='<input class="blank-input '+cls+(['fv','fe','fl','fm','fi','dec'].indexOf(step.expr)>=0?' fr':(step.expr==='flist'||step.expr==='dlist'||step.expr==='glist')?' wide':step.expr===true?' expr':(step.expr==='words'||step.expr==='list'||step.expr==='expanded'||step.expr==='set'||step.expr==='primes'||step.expr==='trans'||step.expr==='rot'?' wide':''))+'" data-step="'+i+'" data-bkey="'+bkey+'" value="'+esc(val)+'" '+dis+'>';
      line = line.replace('__'+bkey+'__', inp);
    });
    if(step.fig) h += '<div class="fig">'+step.fig+'</div>';
    h += '<div class="step-line'+(resolved?' resolved':'')+'">'+line+'</div>';
    if(ss.status==='revealed'){
      var reveals=[];
      Object.keys(step.a).forEach(function(bkey){ reveals.push(bkey+' = '+esc(step.a[bkey])); });
      h += '<div class="reveal-note">correct: '+reveals.join(', ')+'</div>';
    }
  }
  h += '</div>';
  return h;
}

var __flash=null;
function restoreFeedback(item){
  var fb=document.getElementById('feedbackBox'); if(!fb) return;
  if(__flash){ fb.className='feedback show '+__flash.c; fb.innerHTML=__flash.h; __flash=null; return; }
  if(MODE==='quiz'){ fb.className='feedback'; fb.innerHTML=''; return; }
  if(item.status==='correct'){ fb.className='feedback show ok'; fb.innerHTML='<b>All done — correct!</b>'; }
  else if(item.status==='revealed'){ fb.className='feedback show reveal'; fb.innerHTML='<b>Answer revealed above.</b> Move on whenever you’re ready.'; }
  else if(item.status==='skipped'){ fb.className='feedback show retry'; fb.innerHTML='Skipped — you can answer it now and press <b>Check</b>, or come back later from the Question Palette.'; }
  else { fb.className='feedback'; fb.innerHTML=''; }
}

function slideIsAnswered(slide,item){
  if(slide.kind==='mcq'||slide.kind==='ar') return item.choice!==undefined;
  return item.stepStates.some(function(ss){ return Object.keys(ss.inputs).some(function(k){ return k.indexOf('fs_')!==0 && ss.inputs[k] && String(ss.inputs[k]).trim()!==''; }); });
}
function renderNavbar(item){
  var ts = state.tabs[activeTab];
  var slides = SLIDES[activeTab];
  var slide = slides[ts.idx];
  var isLast = ts.idx === slides.length-1;
  var h='';
  h += '<button class="btn" id="btnPrev" '+(ts.idx===0?'disabled':'')+'>&larr; Previous</button>';

  if(MODE==='quiz'){
    h += '<button class="btn" id="btnSkip">Skip</button>';
    h += '<span class="spacer"></span>';
    h += '<button class="btn btn-primary" id="btnNext">'+(isLast?'Finish':'Next →')+'</button>';
  } else {
    h += '<button class="btn" id="btnSkip" '+(item.status!=='unanswered'?'disabled':'')+'>Skip</button>';
    h += '<span class="spacer"></span>';
    h += '<button class="btn btn-primary" id="btnCheck" '+((item.status!=='unanswered'&&item.status!=='skipped')?'disabled':'')+'>Check</button>';
    h += '<button class="btn btn-primary" id="btnNext" '+(canProceed(item)?'':'disabled')+'>'+(isLast?'Finish':'Next →')+'</button>';
  }
  document.getElementById('navbarInner').innerHTML = h;

  document.getElementById('btnPrev').addEventListener('click', function(){ if(ts.idx>0){ ts.idx--; renderSlide(); } });

  if(MODE==='quiz'){
    document.getElementById('btnSkip').addEventListener('click', function(){
      item.status='skipped';
      advanceQuiz(ts, slides);
    });
    document.getElementById('btnNext').addEventListener('click', function(){
      item.status = slideIsAnswered(slide,item) ? 'answered' : 'unanswered';
      advanceQuiz(ts, slides);
    });
  } else {
    document.getElementById('btnSkip').addEventListener('click', function(){
      if(item.status==='unanswered'){ item.status='skipped'; renderSlide(); }
    });
    document.getElementById('btnNext').addEventListener('click', function(){
      if(!canProceed(item)) return;
      if(ts.idx < slides.length-1){ ts.idx++; ts.maxReached=Math.max(ts.maxReached, ts.idx); renderSlide(); }
      else { renderFinished(); }
    });
    document.getElementById('btnCheck').addEventListener('click', function(){ handleCheck(); });
  }
}
function advanceQuiz(ts, slides){
  if(ts.idx < slides.length-1){ ts.idx++; ts.maxReached=Math.max(ts.maxReached, ts.idx); renderSlide(); }
  else { renderFinished(); }
}

function wireSlideEvents(slide, item, idx){
  document.querySelectorAll('input[type="radio"][name="choice"]').forEach(function(r){
    r.addEventListener('change', function(){ item.choice=parseInt(r.value,10); saveState();
      document.querySelectorAll('.opt').forEach(function(l){ l.classList.remove('is-chosen'); var t=l.querySelector('.opt-tag'); if(t) t.remove(); });
      var lab=r.closest('.opt'); lab.classList.add('is-chosen'); var tg=document.createElement('span'); tg.className='opt-tag'; tg.textContent='Selected'; lab.appendChild(tg); });
  });
  document.querySelectorAll('.blank-input').forEach(function(inp){
    inp.addEventListener('input', function(){
      var si=parseInt(inp.dataset.step,10), bk=inp.dataset.bkey;
      item.stepStates[si].inputs[bk]=inp.value;
      saveState();
    });
  });
}

function handleCheck(){
  var ts = state.tabs[activeTab];
  var slide = SLIDES[activeTab][ts.idx];
  var item = ts.items[ts.idx];
  if(item.status==='skipped') item.status='unanswered';
  var fb = document.getElementById('feedbackBox');

  if(slide.kind==='mcq' || slide.kind==='ar'){
    if(item.choice===undefined){ fb.className='feedback show err'; fb.innerHTML='Please choose an option first.'; return; }
    var ok = item.choice===slide.correct;
    if(ok){
      item.status='correct'; playSuccess();
      fb.className='feedback show ok'; fb.innerHTML='<b>Correct!</b>';
    } else {
      item.attempts=(item.attempts||0)+1;
      if(item.attempts>=2){ item.status='revealed'; playReveal(); }
      else { playWrong(); fb.className='feedback show retry'; fb.innerHTML='<b>Not quite — try again</b> (attempt 1 of 2) <span class="attempts-dots"><span class="used"></span><span></span></span>'; __flash={c:'retry',h:'<b>Not quite — try again</b> (attempt 1 of 2) <span class="attempts-dots"><span class="used"></span><span></span></span>'}; }
    }
    renderSlide();
    return;
  }

  // blank / case
  var step = slide.flat[item.curStep];
  var ss = item.stepStates[item.curStep];
  var blanks = Object.keys(step.a);
  var missing = blanks.some(function(k){ return !ss.inputs[k] || String(ss.inputs[k]).trim()===''; });
  if(missing){ fb.className='feedback show err'; fb.innerHTML='Fill in every blank in this step before checking.'; return; }

  var allGood=true;
  blanks.forEach(function(k){
    var good=answerMatches(ss.inputs[k], step.a[k], step.accept, step.expr);
    ss.inputs['fs_'+k]=good?'correct':'wrong';
    if(!good) allGood=false;
  });

  if(allGood){
    ss.status='correct'; playSuccess();
    advanceStepOrFinish(item, slide);
  } else {
    ss.attempts=(ss.attempts||0)+1;
    if(ss.attempts>=2){
      ss.status='revealed'; playReveal();
      advanceStepOrFinish(item, slide);
    } else {
      playWrong();
      fb.className='feedback show retry';
      fb.innerHTML='<b>Not quite — try again</b> (attempt 1 of 2) <span class="attempts-dots"><span class="used"></span><span></span></span>'; __flash={c:'retry',h:'<b>Not quite — try again</b> (attempt 1 of 2) <span class="attempts-dots"><span class="used"></span><span></span></span>'};
      renderSlide();
      return;
    }
  }
  renderSlide();
}

function advanceStepOrFinish(item, slide){
  var total = slide.flat.length;
  var hasExpr = slide.flat.some(function(s){ return s.expr===true; });
  var hasFrac = slide.flat.some(function(s){ return ['fv','fe','fl','fm','fi','flist'].indexOf(s.expr)>=0; });
  if(item.curStep < total-1){
    item.curStep++;
  } else {
    var anyRevealed = item.stepStates.some(function(ss){ return ss.status==='revealed'; });
    item.status = anyRevealed ? 'revealed' : 'correct';
  }
}

/* ================= palette ================= */
var overlay=document.getElementById('overlay');
function statusOf(tabId,i){
  var ts=state.tabs[tabId];
  if(i>ts.maxReached) return 'locked';
  if(i===ts.idx) return 'current';
  return ts.items[i].status==='unanswered' ? 'locked' : ts.items[i].status;
}
function buildPalette(){
  var slides=SLIDES[activeTab];
  document.getElementById('paletteTitle').textContent = TAB_DEFS.find(function(t){return t.id===activeTab;}).label+' · Question palette';
  var body=document.getElementById('paletteBody');
  var html='';
  for(var i=0;i<slides.length;i++){
    html += '<div class="chip" data-status="'+statusOf(activeTab,i)+'" data-idx="'+i+'">'+(i+1)+'</div>';
  }
  body.innerHTML = html;
  body.querySelectorAll('.chip').forEach(function(chip){
    chip.addEventListener('click', function(){
      var i=parseInt(chip.dataset.idx,10);
      var ts=state.tabs[activeTab];
      if(i>ts.maxReached){ showToast('Finish the earlier questions to unlock this one.'); return; }
      ts.idx=i; closePalette(); renderSlide();
    });
  });
}
function openPalette(){ buildPalette(); overlay.classList.add('show'); }
function closePalette(){ overlay.classList.remove('show'); }
var toastTimer;
function showToast(msg){
  var t=document.getElementById('toast'); t.textContent=msg; t.classList.add('show');
  clearTimeout(toastTimer); toastTimer=setTimeout(function(){ t.classList.remove('show'); },2200);
}
document.getElementById('paletteFab').addEventListener('click', openPalette);
document.getElementById('paletteClose').addEventListener('click', closePalette);
overlay.addEventListener('click', function(e){ if(e.target===overlay) closePalette(); });

function updateFab(){
  var slides=SLIDES[activeTab];
  var done=state.tabs[activeTab].items.filter(function(it){ return it.status==='correct'||it.status==='revealed'||it.status==='skipped'; }).length;
  document.getElementById('fabBadge').textContent = done+'/'+slides.length;
}

/* ================= overall progress + finish ================= */
function updateChapterProgress(){
  var total=0, done=0;
  TAB_DEFS.forEach(function(td){
    state.tabs[td.id].items.forEach(function(it){
      total++;
      if(it.status==='correct'||it.status==='revealed'||it.status==='skipped') done++;
    });
  });
  var pct = total>0 ? Math.round((done/total)*100) : 0;
  document.getElementById('cpFill').style.width=pct+'%';
  document.getElementById('cpLabel').textContent=pct+'% complete';
}
function isSlideCorrect(tabId,i){
  var slide=SLIDES[tabId][i], item=state.tabs[tabId].items[i];
  if(slide.kind==='mcq'||slide.kind==='ar') return item.choice===slide.correct;
  return slide.flat.every(function(step,si){
    var ss=item.stepStates[si];
    return Object.keys(step.a).every(function(k){ return answerMatches(ss.inputs[k], step.a[k], step.accept, step.expr); });
  });
}
function isSlideAttempted(tabId,i){
  var slide=SLIDES[tabId][i], item=state.tabs[tabId].items[i];
  if(slide.kind==='mcq'||slide.kind==='ar') return item.choice!==undefined;
  return slide.flat.some(function(step,si){
    var ss=item.stepStates[si];
    return Object.keys(step.a).some(function(k){ return ss.inputs[k] && String(ss.inputs[k]).trim()!==''; });
  });
}
function slideLabel(slide){
  var t = slide.kind==='case' ? slide.title : (slide.kind==='ar' ? slide.a : (slide.p||slide.text||''));
  t = String(t);
  return t.length>90 ? t.slice(0,90)+'…' : t;
}
function slideAnswerText(slide, item, correctSide){
  if(slide.kind==='mcq'||slide.kind==='ar'){
    var opts = slide.kind==='mcq' ? slide.opts : AR_OPTIONS;
    if(correctSide) return '('+LETTERS[slide.correct]+') '+opts[slide.correct];
    return item.choice!==undefined ? '('+LETTERS[item.choice]+') '+opts[item.choice] : '— not attempted —';
  }
  return slide.flat.map(function(step,si){
    var ss=item.stepStates[si];
    return Object.keys(step.a).map(function(k){
      return correctSide ? step.a[k] : (ss.inputs[k] || '—');
    }).join(', ');
  }).join('  |  ');
}

function renderFinished(){
  if(MODE==='quiz'){ renderQuizResults(); return; }
  var ts=state.tabs[activeTab];
  var correct=ts.items.filter(function(i){return i.status==='correct';}).length;
  var revealed=ts.items.filter(function(i){return i.status==='revealed';}).length;
  var skipped=ts.items.filter(function(i){return i.status==='skipped';}).length;
  var h='<div class="qcard done-card"><div class="big">✨</div><h2>Tab complete</h2>';
  h+='<p style="color:var(--ink-soft);font-size:14px;">You worked through all '+ts.items.length+' questions in this tab.</p>';
  if(!ts.recorded){ ts.recorded=true; addRecord('learning', activeTab, correct, revealed, skipped, ts.items.length); }
  h+='<div class="score-pills">'+
     '<span class="score-pill" style="background:var(--success-soft);color:var(--success);">'+correct+' correct</span>'+
     '<span class="score-pill" style="background:var(--danger-soft);color:var(--danger);">'+revealed+' revealed</span>'+
     '<span class="score-pill" style="background:var(--gold-soft);color:var(--retry-text);">'+skipped+' skipped</span></div>'+
     '<button class="btn btn-primary" id="btnReview">Review from question 1</button></div>';
  document.getElementById('wrap').innerHTML=h;
  document.getElementById('navbarInner').innerHTML='';
  document.getElementById('btnReview').addEventListener('click', function(){ ts.idx=0; ts.recorded=false; renderSlide(); });
  updateChapterProgress(); saveState();
}

function renderQuizResults(){
  var ts=state.tabs[activeTab];
  var slides=SLIDES[activeTab];
  var correctCount=0, attemptedCount=0;
  var rowsHtml = slides.map(function(slide,i){
    var item=ts.items[i];
    var ok=isSlideCorrect(activeTab,i);
    var att=isSlideAttempted(activeTab,i);
    if(ok) correctCount++;
    if(att) attemptedCount++;
    var tagCls = ok?'ok':(att?'bad':'na');
    var tagText = ok?'Correct':(att?'Incorrect':'Not attempted');
    var row='<div class="review-row">';
    row+='<span class="review-tag '+tagCls+'">Q'+(i+1)+' · '+tagText+'</span>';
    row+='<div class="review-q">'+fr(esc(slideLabel(slide)))+'</div>';
    row+='<div class="review-ans"><b>Your answer:</b> '+fr(esc(slideAnswerText(slide,item,false)))+'</div>';
    if(!ok) row+='<div class="review-ans" style="color:var(--success);"><b>Correct answer:</b> '+fr(esc(slideAnswerText(slide,item,true)))+'</div>';
    if(slide.sol) row+='<details class="rev-sol"><summary>Show solution</summary>'+solutionHTML(slide)+'</details>';
    row+='</div>';
    return row;
  }).join('');

  addRecord('quiz', activeTab, correctCount, 0, 0, slides.length);
  var h='<div class="qcard done-card" style="text-align:left;">';
  h+='<div style="text-align:center;"><div class="big">🏁</div><h2>Quiz complete</h2>';
  h+='<p style="color:var(--ink-soft);font-size:14px;">'+correctCount+' / '+slides.length+' correct · '+attemptedCount+' attempted</p></div>';
  h+='<div style="margin-top:16px;">'+rowsHtml+'</div>';
  h+='<div style="text-align:center;margin-top:6px;"><button class="btn btn-primary" id="btnReview">Review from question 1</button></div>';
  h+='</div>';
  document.getElementById('wrap').innerHTML=h;
  document.getElementById('navbarInner').innerHTML='';
  document.getElementById('btnReview').addEventListener('click', function(){ ts.idx=0; renderSlide(); });
  playSuccess();
  updateChapterProgress(); saveState();
}

/* ================= mode picker ================= */
function updateModePill(){
  var btn=document.getElementById('modePill');
  if(!btn) return;
  btn.textContent = MODE==='quiz' ? '📝 Quiz Mode · switch' : '📘 Learning Sheet · switch';
}
function showChrome(show){
  document.querySelector('.tabbar').style.display = show?'':'none';
  document.querySelector('.slide-progress').style.display = show?'':'none';
  document.querySelector('.navbar').style.display = show?'':'none';
  document.getElementById('paletteFab').style.display = show?'':'none';
}
function renderModePicker(){
  showChrome(false);
  var wrap=document.getElementById('wrap');
  wrap.innerHTML =
    '<div class="mode-pick">'+
      '<div class="mode-card" data-pick="learning"><div class="mode-icon">📘</div><h3>Learning Sheet</h3>'+
      '<p>Work through each question step by step with instant feedback — two tries, then the correct value is revealed right there so you can keep moving.</p></div>'+
      '<div class="mode-card" data-pick="quiz"><div class="mode-icon">📝</div><h3>Quiz Mode</h3>'+
      '<p>Attempt every question with no hints along the way. Your score and the full answer key are shown together once you finish the tab — just like the real exam.</p></div>'+
    '</div>';
  wrap.querySelectorAll('[data-pick]').forEach(function(card){
    card.addEventListener('click', function(){
      setMode(card.dataset.pick); activeTab='theory';
      document.getElementById('modePill').hidden=false;
      updateModePill();
      showChrome(true);
      buildTabbar();
      renderSlide();
    });
  });
}
document.getElementById('modePill').addEventListener('click', function(){
  if(!appState.mode){ return; }
  setMode(appState.mode==='quiz' ? 'learning' : 'quiz');
  updateModePill();
  showChrome(true);
  buildTabbar();
  renderSlide();
});

/* ================= boot ================= */
var _origRenderSlide = renderSlide;
renderSlide = function(){ _origRenderSlide(); updateChapterProgress(); updateModePill(); };


/* ================= theory tab ================= */
function renderTheory(){
  var wrap=document.getElementById('wrap');
  wrap.innerHTML='<div class="theory">'+fr(THEORY)+'</div>';
  document.querySelector('.slide-progress').style.display='none';
  document.querySelector('.navbar').style.display='none';
  document.getElementById('paletteFab').style.display='none';
  document.getElementById('secSub').textContent='Theory — notes, key ideas and worked examples';
  wrap.querySelectorAll('[data-go]').forEach(function(b){ b.addEventListener('click',function(){ activeTab=b.dataset.go; buildTabbar(); renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); }); });
  wrap.querySelectorAll('[data-jump]').forEach(function(b){ b.addEventListener('click',function(){ var t=document.getElementById(b.dataset.jump); if(t) t.scrollIntoView({behavior:'smooth',block:'start'}); }); });
}
var _rsTheory = renderSlide;
renderSlide = function(){
  if(activeTab==='theory'){ renderTheory(); buildTabbar(); updateChapterProgress(); updateModePill(); saveState(); return; }
  document.querySelector('.slide-progress').style.display='';
  document.querySelector('.navbar').style.display='';
  document.getElementById('paletteFab').style.display='';
  _rsTheory();
};


/* ================= MYP criterion report ================= */
var CRIT_COL={A:'var(--accent-text)',B:'var(--gold)',C:'#8A6FC4',D:'#2F9AA0'};
function critStats(){
  return REPORT.map(function(r){
    var tabId=r[0], slides=SLIDES[tabId], ts=state&&state.tabs[tabId];
    var c=0,w=0,n=0;
    slides.forEach(function(sl,i){
      if(!ts||!ts.items[i]){ n++; return; }
      var it=ts.items[i];
      if(MODE==='learning'){
        if(it.status==='correct') c++; else if(it.status==='revealed') w++; else n++;
      } else {
        if(isSlideCorrect(tabId,i)) c++; else if(isSlideAttempted(tabId,i)) w++; else n++;
      }
    });
    var tot=slides.length, pct=tot?Math.round(c/tot*100):0;
    var lvl=Math.round(c/Math.max(tot,1)*8);
    return {tab:tabId,letter:r[1],name:r[2],c:c,w:w,n:n,tot:tot,pct:pct,lvl:lvl};
  });
}
function arcPath(cx,cy,r,a0,a1){
  if(a1-a0>=Math.PI*2-1e-6){ return 'M'+(cx-r)+','+cy+' a'+r+','+r+' 0 1,0 '+(2*r)+',0 a'+r+','+r+' 0 1,0 '+(-2*r)+',0 Z'; }
  var x0=cx+r*Math.sin(a0), y0=cy-r*Math.cos(a0), x1=cx+r*Math.sin(a1), y1=cy-r*Math.cos(a1);
  return 'M'+cx+','+cy+' L'+x0.toFixed(2)+','+y0.toFixed(2)+' A'+r+','+r+' 0 '+((a1-a0)>Math.PI?1:0)+',1 '+x1.toFixed(2)+','+y1.toFixed(2)+' Z';
}
function pieSVG(parts,size,hole,center,sub){
  var tot=parts.reduce(function(s,p){return s+p.v;},0), cx=size/2, cy=size/2, r=size/2-4, a=0, h='';
  if(!tot){ h+='<circle cx="'+cx+'" cy="'+cy+'" r="'+r+'" style="fill:var(--paper-2);stroke:var(--rule)"/>'; }
  parts.forEach(function(p){ if(!p.v) return; var b=a+p.v/tot*Math.PI*2; h+='<path d="'+arcPath(cx,cy,r,a,b)+'" style="fill:'+p.col+';stroke:var(--card);stroke-width:2"><title>'+esc(p.label)+': '+p.v+'</title></path>'; a=b; });
  if(hole) h+='<circle cx="'+cx+'" cy="'+cy+'" r="'+(r*hole)+'" style="fill:var(--card)"/>';
  if(center) h+='<text x="'+cx+'" y="'+(cy-(sub?4:0))+'" text-anchor="middle" dominant-baseline="middle" style="fill:var(--ink);font:700 '+(size>150?22:15)+'px Fraunces,serif">'+center+'</text>';
  if(sub) h+='<text x="'+cx+'" y="'+(cy+16)+'" text-anchor="middle" style="fill:var(--ink-soft);font:600 11px \'Source Sans 3\',sans-serif">'+sub+'</text>';
  return '<svg viewBox="0 0 '+size+' '+size+'" width="'+size+'" height="'+size+'" role="img">'+h+'</svg>';
}
function band(l){ return l===0?'0':(l<=2?'1–2':(l<=4?'3–4':(l<=6?'5–6':'7–8'))); }
function renderReport(){
  var st=critStats(), totC=0, totQ=0;
  st.forEach(function(s){ totC+=s.c; totQ+=s.tot; });
  var h='<div class="theory">';
  h+='<section class="note"><h2>Chapter test report</h2><p class="lt">'+(MODE==='quiz'?'<b>Quiz mode</b> results: answers are marked when you finish each test tab.':'<b>Learning mode</b> results: a question counts as correct only if you got it without the answer being revealed. Switch to Quiz mode for an exam-style score.')+'</p>';
  h+='<div class="rep-top"><div class="rep-pie">'+pieSVG(st.map(function(s){return {v:s.c,col:CRIT_COL[s.letter],label:'Criterion '+s.letter};}),200,0.55,totC+'/'+totQ,'correct')+'</div>';
  h+='<div class="rep-legend"><div class="rep-cap">Marks earned, by criterion</div>'+st.map(function(s){ return '<div class="rep-li"><span class="sw" style="background:'+CRIT_COL[s.letter]+'"></span><b>'+s.letter+'</b>&nbsp;'+esc(s.name)+'<span class="rep-n">'+s.c+' / '+s.tot+'</span></div>'; }).join('')+'</div></div></section>';
  h+='<div class="rep-grid">'+st.map(function(s){
    return '<div class="rep-card"><div class="rep-h"><span class="crit" style="background:'+CRIT_COL[s.letter]+'">'+s.letter+'</span>'+esc(s.name)+'</div>'+
      '<div class="rep-row">'+pieSVG([{v:s.c,col:'var(--success)',label:'Correct'},{v:s.w,col:'var(--danger)',label:'Incorrect'},{v:s.n,col:'var(--locked)',label:'Not attempted'}],120,0.5,s.pct+'%')+
      '<div class="rep-stats"><div><span class="sw" style="background:var(--success)"></span>Correct <b>'+s.c+'</b></div><div><span class="sw" style="background:var(--danger)"></span>Incorrect <b>'+s.w+'</b></div><div><span class="sw" style="background:var(--locked)"></span>Not attempted <b>'+s.n+'</b></div>'+
      '<div class="rep-lvl">Indicative level <b>'+s.lvl+'</b> / 8 <span>(band '+band(s.lvl)+')</span></div></div></div>'+
      '<button class="hub-btn" data-go="'+s.tab+'">Open Test '+s.letter+' →</button></div>';
  }).join('')+'</div>';
  h+='<p class="rep-note">Indicative level = fraction of questions correct × 8, rounded. It is a practice guide only; your teacher awards the real MYP criterion levels.</p></div>';
  var wrap=document.getElementById('wrap'); wrap.innerHTML=h;
  document.querySelector('.slide-progress').style.display='none';
  document.querySelector('.navbar').style.display='none';
  document.getElementById('paletteFab').style.display='none';
  document.getElementById('secSub').textContent='Report — chapter test results by MYP criterion';
  wrap.querySelectorAll('[data-go]').forEach(function(b){ b.addEventListener('click',function(){ activeTab=b.dataset.go; buildTabbar(); renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); }); });
}
var _rsReport = renderSlide;
renderSlide = function(){
  if(activeTab==='report'){ renderReport(); buildTabbar(); updateChapterProgress(); updateModePill(); saveState(); return; }
  _rsReport();
};


/* ================= skipped-question return ================= */
function firstSkippedIdx(ts){
  for(var i=0;i<ts.items.length;i++){
    var it=ts.items[i];
    if(MODE==='quiz'){ if(!isSlideAttempted(activeTab,i)) return i; }
    else if(it.status==='skipped'||it.status==='unanswered') return i;
  }
  return -1;
}
function skippedList(ts){
  var out=[]; for(var i=0;i<ts.items.length;i++){ var it=ts.items[i];
    if(MODE==='quiz' ? !isSlideAttempted(activeTab,i) : (it.status==='skipped'||it.status==='unanswered')) out.push(i); }
  return out;
}
function renderSkipGate(ts){
  var list=skippedList(ts);
  var h='<div class="qcard done-card"><div class="big">⏭️</div><h2>You skipped '+list.length+' question'+(list.length>1?'s':'')+'</h2>'+
    '<p style="color:var(--ink-soft);font-size:14px;">Answer them now, or submit the tab as it is. Answers are marked only when you submit.</p>'+
    '<div class="skip-chips">'+list.map(function(i){ return '<button class="chip skip-go" data-i="'+i+'">Q'+(i+1)+'</button>'; }).join('')+'</div>'+
    '<div class="skip-btns"><button class="btn btn-primary" id="btnGoSkipped">Answer skipped questions</button><button class="btn" id="btnSubmitAnyway">Submit anyway</button></div></div>';
  document.getElementById('wrap').innerHTML=h;
  document.getElementById('navbarInner').innerHTML='';
  var go=function(i){ ts.idx=i; ts.maxReached=Math.max(ts.maxReached,i); renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); };
  document.getElementById('btnGoSkipped').addEventListener('click',function(){ go(list[0]); });
  document.querySelectorAll('.skip-go').forEach(function(b){ b.addEventListener('click',function(){ go(parseInt(b.dataset.i,10)); }); });
  document.getElementById('btnSubmitAnyway').addEventListener('click',function(){ ts.submitOK=true; renderFinished(); ts.submitOK=false; });
  saveState();
}
var _rfSkip = renderFinished;
renderFinished = function(){
  var ts=state.tabs[activeTab];
  if(MODE==='quiz' && !ts.submitOK && skippedList(ts).length){ renderSkipGate(ts); return; }
  _rfSkip();
  if(MODE==='learning'){
    var list=skippedList(ts);
    if(list.length){
      var card=document.querySelector('.done-card');
      if(card){ var d=document.createElement('div'); d.className='skip-btns';
        d.innerHTML='<button class="btn btn-primary" id="btnGoSkipped">Attempt skipped questions ('+list.length+')</button>';
        card.appendChild(d);
        document.getElementById('btnGoSkipped').addEventListener('click',function(){ ts.idx=list[0]; ts.recorded=false; renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); }); }
    }
  }
};


/* ================= approx answers (physics: within 1%) ================= */
var _amTools = answerMatches;
answerMatches = function(input,answer,accept,expr){
  if(expr==='approx'){
    var n1=parseNum(input); if(n1===null) return false;
    return [answer].concat(accept||[]).some(function(a){ var n2=parseNum(a); if(n2===null) return false; return Math.abs(n1-n2) <= Math.max(0.011*Math.abs(n2), 1e-9); });
  }
  return _amTools(input,answer,accept,expr);
};

/* ================= palette: every question already reached can be opened ================= */
statusOf = function(tabId,i){
  var ts=state.tabs[tabId];
  if(i>ts.maxReached) return 'locked';
  if(i===ts.idx) return 'current';
  var s=ts.items[i].status;
  if(s==='unanswered') return 'skipped';
  return s;
};

/* ================= on-screen keyboard ================= */
var KB={on:true, page:'num', target:null};
try{ var kbp=localStorage.getItem('sopaan-kb-pref'); if(kbp==='off') KB.on=false; }catch(e){}
function kbSave(){ try{ localStorage.setItem('sopaan-kb-pref', KB.on?'on':'off'); }catch(e){} }
var KEYS_NUM=[['7','8','9','(',')'],['4','5','6','−','/'],['1','2','3','.',','],['0',':','%','°','⌫'],['abc','←','→','Clear','Done']];
var KEYS_FRAC=[['7','8','9','/'],['4','5','6','−'],['1','2','3','space'],['0',',','⌫','Clear'],['abc','←','→','Done']];
var KEYS_ALG=[['7','8','9','x','y','n'],['4','5','6','+','−','a'],['1','2','3','×','÷','b'],['0','.','(',')','^','²'],['/','π','|','t','⌫','Clear'],['abc','←','→','Done']];
function kbLayoutFor(inp){ try{ var ts=state.tabs[activeTab], sl=SLIDES[activeTab][ts.idx], stp=sl.flat[parseInt(inp.dataset.step,10)]; var m=stp.expr, key=String(stp.a[inp.dataset.bkey]||'');
  if(m==='words'||m==='glist'||m==='angle') return 'abc'; if(m===true||m==='pow'||m==='primes') return 'alg';
  if(['fv','fe','fl','fm','fi','flist'].indexOf(m)>=0) return 'frac'; if(m==='dec'||m==='approx'||m==='dlist'||m==='set'||m==='coord'||m==='list'||m==='time') return 'num';
  if(/^[\-−]?\d+ \d+\/\d+$/.test(key)||/^[\-−]?\d+\/\d+$/.test(key)) return 'frac'; if(/[a-df-z]/i.test(key.replace(/pi/gi,''))) return /\d/.test(key)?'alg':'abc'; return 'num'; }catch(e){ return 'num'; } }
var KEYS_ABC=[['q','w','e','r','t','y','u','i','o','p'],['a','s','d','f','g','h','j','k','l','-'],['z','x','c','v','b','n','m',',',':','/'],['123','space','←','→','⌫','Done']];
function kbBuild(){
  var el=document.getElementById('vkb'); if(!el){ el=document.createElement('div'); el.id='vkb'; el.className='vkb'; document.body.appendChild(el);
    el.addEventListener('pointerdown',function(e){ var b=e.target.closest('button[data-k]'); e.preventDefault(); if(b) kbPress(b.dataset.k); });
    el.addEventListener('mousedown',function(e){ e.preventDefault(); }); }
  var rows={num:KEYS_NUM,frac:KEYS_FRAC,alg:KEYS_ALG,abc:KEYS_ABC}[KB.page]||KEYS_NUM;
  el.innerHTML='<div class="vkb-top"><span>⌨️ Keyboard</span><button data-k="device" class="vkb-link">Use device keyboard</button></div>'+
    rows.map(function(r){ return '<div class="vkb-row">'+r.map(function(k){
      var cls='vkb-k'+(/^(abc|123|Done|Clear|⌫|←|→|space)$/.test(k)?' fn':'')+(k==='Done'?' done':'');
      return '<button type="button" class="'+cls+'" data-k="'+k+'">'+(k==='space'?'space':k)+'</button>'; }).join('')+'</div>'; }).join('');
  return el;
}
function kbShow(inp){ KB.target=inp; KB.home=kbLayoutFor(inp); KB.page=KB.home; if(!KB.on) return; var cp=document.getElementById('calcPanel'); if(cp&&cp.classList.contains('show')) return; var el=kbBuild(); var nb=document.querySelector('.navbar'); el.style.bottom=(nb?nb.getBoundingClientRect().height:0)+'px'; el.classList.add('show'); document.body.classList.add('kb-open'); setTimeout(function(){ var r=inp.getBoundingClientRect(), top=el.getBoundingClientRect().top; if(r.bottom>top-12) window.scrollBy({top:r.bottom-top+60,behavior:'smooth'}); else if(r.top<60) window.scrollBy({top:r.top-80,behavior:'smooth'}); },30); }
function kbHide(){ var el=document.getElementById('vkb'); if(el) el.classList.remove('show'); document.body.classList.remove('kb-open'); }
function kbInsert(s){
  var t=KB.target; if(!t||t.disabled) return;
  var a=t.selectionStart==null?t.value.length:t.selectionStart, b=t.selectionEnd==null?a:t.selectionEnd;
  t.value=t.value.slice(0,a)+s+t.value.slice(b); var p=a+s.length; try{ t.setSelectionRange(p,p); }catch(e){}
  t.dispatchEvent(new Event('input',{bubbles:true}));
}
function kbPress(k){
  var t=KB.target; if(k==='device'){ KB.on=false; kbSave(); kbHide(); document.querySelectorAll('.blank-input').forEach(function(i){ i.removeAttribute('inputmode'); }); if(t){ t.blur(); setTimeout(function(){ t.focus(); },50); } showToast('Device keyboard on. Tap ⌨️ on any blank to bring the on-screen keyboard back.'); return; }
  if(k==='Done'){ kbHide(); if(t) t.blur(); return; }
  if(k==='abc'||k==='123'){ KB.page=(k==='abc')?'abc':(KB.home&&KB.home!=='abc'?KB.home:'num'); kbBuild(); return; }
  if(!t) return;
  if(k==='⌫'){ var a=t.selectionStart, b=t.selectionEnd; if(a===b&&a>0){ t.value=t.value.slice(0,a-1)+t.value.slice(b); try{t.setSelectionRange(a-1,a-1);}catch(e){} } else { t.value=t.value.slice(0,a)+t.value.slice(b); try{t.setSelectionRange(a,a);}catch(e){} } t.dispatchEvent(new Event('input',{bubbles:true})); return; }
  if(k==='Clear'){ t.value=''; t.dispatchEvent(new Event('input',{bubbles:true})); return; }
  if(k==='←'||k==='→'){ var p=(t.selectionStart||0)+(k==='←'?-1:1); p=Math.max(0,Math.min(t.value.length,p)); try{t.setSelectionRange(p,p);}catch(e){} return; }
  var map={'−':'-','space':' '}; kbInsert(map[k]!==undefined?map[k]:k);
}
function kbWire(){
  document.querySelectorAll('.blank-input').forEach(function(inp){
    if(inp.dataset.kb) return; inp.dataset.kb='1';
    if(KB.on) inp.setAttribute('inputmode','none');
    inp.addEventListener('focus',function(){ kbShow(inp); });
    var btn=document.createElement('button'); btn.type='button'; btn.className='kb-toggle'; btn.title='On-screen keyboard'; btn.textContent='⌨️'; btn.tabIndex=-1;
    btn.addEventListener('mousedown',function(e){ e.preventDefault(); });
    btn.addEventListener('click',function(){ KB.on=true; kbSave(); document.querySelectorAll('.blank-input').forEach(function(i){ i.setAttribute('inputmode','none'); }); inp.focus(); kbShow(inp); });
    if(!inp.disabled) inp.insertAdjacentElement('afterend',btn);
  });
}
document.addEventListener('focusout',function(e){ setTimeout(function(){ var a=document.activeElement; if(!a||!a.classList||!a.classList.contains('blank-input')){ if(!document.querySelector('#vkb:hover')) kbHide(); } },120); });

/* ================= calculator ================= */
var CALC={expr:'', ans:0};
function calcEval(src){
  var s=String(src).replace(/×/g,'*').replace(/÷/g,'/').replace(/−/g,'-').replace(/π/g,'(PI)').replace(/Ans/g,'('+CALC.ans+')').replace(/\^/g,'**').replace(/√\(/g,'sqrt(').replace(/²/g,'**2').replace(/E/g,'*10**');
  s=s.replace(/(^|[(*\/+\-,])-/g,'$1(-1)*');
  if(/[^0-9+\-*/().,a-z A-Z]/.test(s)) throw 0;
  var ok=s.replace(/sin|cos|tan|asin|acos|atan|sqrt|log|ln|PI|abs/g,''); if(/[a-zA-Z]/.test(ok)) throw 0;
  var f=new Function('sin','cos','tan','asin','acos','atan','sqrt','log','ln','PI','abs','return ('+s+');');
  var d=Math.PI/180;
  var v=f(function(x){return Math.sin(x*d);},function(x){return Math.cos(x*d);},function(x){return Math.tan(x*d);},
    function(x){return Math.asin(x)/d;},function(x){return Math.acos(x)/d;},function(x){return Math.atan(x)/d;},Math.sqrt,Math.log10,Math.log,Math.PI,Math.abs);
  if(typeof v!=='number'||!isFinite(v)) throw 0; return v;
}
function fmtNum(v){ if(Math.abs(v)>=1e10||(Math.abs(v)<1e-6&&v!==0)) return v.toExponential(6).replace(/\.?0+e/,'e'); return String(parseFloat(v.toPrecision(10))); }
var CKEYS=[['sin(','cos(','tan(','√(','^','²'],['asin(','acos(','atan(','(',')','π'],['7','8','9','÷','⌫','AC'],['4','5','6','×','E','Ans'],['1','2','3','−','(−)','Insert'],['0','.','=','+']];
function openCalc(){
  var p=document.getElementById('calcPanel');
  if(!p){ p=document.createElement('div'); p.id='calcPanel'; p.className='tool-panel calc';
    p.innerHTML='<div class="tp-head"><b>🧮 Calculator</b><span class="tp-note">degrees · tap a blank, then Insert</span><button class="tp-x" data-c="close">✕</button></div>'+
      '<div class="calc-disp"><div class="calc-expr" id="calcExpr"></div><div class="calc-res" id="calcRes">0</div></div>'+
      '<div class="calc-keys">'+CKEYS.map(function(r){ return r.map(function(k){ return '<button type="button" data-c="'+k+'" class="'+(k==='='?'eq':(/^(AC|⌫|Insert)$/.test(k)?'fn':''))+'">'+({'sin(':'sin','cos(':'cos','tan(':'tan','asin(':'sin⁻¹','acos(':'cos⁻¹','atan(':'tan⁻¹','√(':'√'}[k]||k)+'</button>'; }).join(''); }).join('')+'</div>';
    document.body.appendChild(p);
    p.addEventListener('mousedown',function(e){ if(e.target.closest('button')) e.preventDefault(); });
    p.addEventListener('click',function(e){ var b=e.target.closest('button[data-c]'); if(!b) return; calcKey(b.dataset.c); });
  }
  kbHide(); var nb=document.querySelector('.navbar'); p.style.bottom=((nb?nb.getBoundingClientRect().height:0)+8)+'px'; p.classList.add('show'); document.body.classList.add('calc-open'); calcShow();
}
function calcShow(res){ document.getElementById('calcExpr').textContent=CALC.expr||' '; if(res!==undefined) document.getElementById('calcRes').textContent=res; }
function calcKey(k){
  if(k==='close'){ document.getElementById('calcPanel').classList.remove('show'); document.body.classList.remove('calc-open'); return; }
  if(k==='AC'){ CALC.expr=''; calcShow('0'); return; }
  if(k==='⌫'){ CALC.expr=CALC.expr.replace(/(asin\(|acos\(|atan\(|sin\(|cos\(|tan\(|√\(|Ans|.)$/,''); calcShow(); return; }
  if(k==='='){ try{ var v=calcEval(CALC.expr); CALC.ans=v; calcShow(fmtNum(v)); }catch(e){ calcShow('Error'); } return; }
  if(k==='(−)'){ CALC.expr+='−'; calcShow(); return; }
  if(k==='Insert'){ var r=document.getElementById('calcRes').textContent; if(KB.target && !KB.target.disabled && r!=='Error'){ KB.target.value=r; KB.target.dispatchEvent(new Event('input',{bubbles:true})); showToast('Inserted '+r+' into the blank.'); } else showToast('Tap a blank first, then press Insert.'); return; }
  CALC.expr+=k; calcShow();
}

/* ================= Desmos ================= */
var DESMOS_KEY='dcb31709b452b1cf9dc26972add0fda6', desmosCalc=null, desmosLoading=false;
function openDesmos(exprs){
  var p=document.getElementById('desmosPanel');
  if(!p){ p=document.createElement('div'); p.id='desmosPanel'; p.className='tool-panel desmos';
    p.innerHTML='<div class="tp-head"><b>📈 Desmos graphing calculator</b><button class="tp-x" id="desmosReset">Reset graph</button><button class="tp-x" id="desmosClose">✕</button></div><div id="desmosBox"><div class="desmos-msg">Loading Desmos…</div></div>';
    document.body.appendChild(p);
    document.getElementById('desmosClose').addEventListener('click',function(){ p.classList.remove('show'); });
    document.getElementById('desmosReset').addEventListener('click',function(){ if(desmosCalc) desmosSet(p._exprs||[]); });
  }
  p._exprs=exprs||[]; p.classList.add('show');
  if(window.Desmos){ desmosInit(); desmosSet(p._exprs); return; }
  if(desmosLoading) return; desmosLoading=true;
  var sc=document.createElement('script'); sc.src='https://www.desmos.com/api/v1.9/calculator.js?apiKey='+DESMOS_KEY;
  sc.onload=function(){ desmosInit(); desmosSet(p._exprs); };
  sc.onerror=function(){ desmosLoading=false; document.getElementById('desmosBox').innerHTML='<div class="desmos-msg">Desmos needs an internet connection. <a href="https://www.desmos.com/calculator" target="_blank" rel="noopener">Open Desmos in a new tab</a>.</div>'; };
  document.head.appendChild(sc);
}
function desmosInit(){ if(desmosCalc) return; var box=document.getElementById('desmosBox'); box.innerHTML=''; desmosCalc=Desmos.GraphingCalculator(box,{expressionsCollapsed:false,settingsMenu:false,border:false,degreeMode:true}); }
function desmosSet(exprs){ if(!desmosCalc) return; desmosCalc.setBlank(); (exprs||[]).forEach(function(e,i){ if(typeof e==='string') desmosCalc.setExpression({id:'e'+i,latex:e}); else desmosCalc.setExpression(Object.assign({id:'e'+i},e)); }); }

/* ================= toolbar on each question ================= */
var _rsTools = renderSlide;
renderSlide = function(){
  _rsTools();
  kbHide();
  if(activeTab==='theory'||activeTab==='report') return;
  var ts=state.tabs[activeTab]; if(!ts) return;
  var slide=SLIDES[activeTab][ts.idx], card=document.querySelector('#wrap .qcard');
  if(card && slide && slide.tools && slide.tools.length && !card.querySelector('.tool-bar')){
    var bar=document.createElement('div'); bar.className='tool-bar';
    bar.innerHTML=(slide.tools.indexOf('calc')>=0?'<button type="button" class="tool-btn" data-t="calc">🧮 Calculator</button>':'')+
                  (slide.tools.indexOf('desmos')>=0?'<button type="button" class="tool-btn" data-t="desmos">📈 Desmos graph</button>':'');
    card.insertBefore(bar, card.firstChild);
    bar.addEventListener('click',function(e){ var b=e.target.closest('[data-t]'); if(!b) return; if(b.dataset.t==='calc') openCalc(); else openDesmos(slide.desmos||[]); });
  }
  kbWire();
};



/* ================= signed fractions in text: {−3/4}, {3/−4}, {−2 1/3}, {p/q} ================= */
fr = function(s){ return String(s).replace(/&lt;(\/?)(b|sup|sub|i)>/g,'<$1$2>')
  .replace(/\{([−-]?\d+) (\d+)\/(\d+)\}/g,'<span class="mx">$1<span class="fq"><span>$2</span><span>$3</span></span></span>')
  .replace(/\{([−-]?[A-Za-z0-9]+)\/([−-]?[A-Za-z0-9]+)\}/g,'<span class="fq"><span>$1</span><span>$2</span></span>'); };
/* ================= BMA badge → main page of this sheet (theory hub) ================= */
(function(){
  var c=document.querySelector('.brand .crest'); if(!c) return;
  var a=document.createElement('button'); a.type='button'; a.className='crest crest-home'; a.title='Back to the main page (theory notes)'; a.setAttribute('aria-label','Main page');
  a.innerHTML='BM<span class="crest-h">⌂</span>'; c.parentNode.replaceChild(a,c);
  a.addEventListener('click',function(){
    if(!student||!MODE){ window.scrollTo({top:0,behavior:'smooth'}); return; }
    if(typeof kbHide==='function') kbHide(); if(typeof SP!=='undefined'&&SP.on) spToggle(false);
    var cp=document.getElementById('calcPanel'); if(cp) cp.classList.remove('show'); document.body.classList.remove('calc-open');
    activeTab = (typeof THEORY!=='undefined') ? 'theory' : TAB_DEFS[0].id;
    buildTabbar(); renderSlide(); window.scrollTo({top:0,behavior:'smooth'});
  });
})();

/* ================= session clock: starts at sign-in and keeps running ================= */
var CLK={t0:null};
(function(){
  var row=document.querySelector('.brand .brand-row'); if(!row) return;
  var d=document.createElement('div'); d.className='bmasw off'; d.id='swBox'; d.title='Time since you signed in';
  d.innerHTML='<span class="bmasw-ic">⏱</span><span class="bmasw-t" id="swT">00:00</span>';
  row.appendChild(d); setInterval(swTick,1000);
})();
function swFmt(s){ s=Math.floor(s||0); var h=Math.floor(s/3600), m=Math.floor(s%3600/60), x=s%60; return (h?h+':'+String(m).padStart(2,'0'):String(m).padStart(2,'0'))+':'+String(x).padStart(2,'0'); }
function swTick(){
  var box=document.getElementById('swBox'); if(!box) return;
  if(student && !CLK.t0) CLK.t0=Date.now();
  if(!student) CLK.t0=null;
  box.classList.toggle('off',!CLK.t0);
  document.getElementById('swT').textContent = CLK.t0 ? swFmt((Date.now()-CLK.t0)/1000) : '00:00';
}
function swTab(){ try{ if(!state||!state.tabs||activeTab==='theory'||activeTab==='report') return null; return state.tabs[activeTab]||null; }catch(e){ return null; } }
var _rsSW = renderSlide;
renderSlide = function(){ _rsSW(); swTick(); };
var _rfSW = renderFinished;
renderFinished = function(){ _rfSW(); var done=document.querySelector('#wrap .done-card'); if(CLK.t0 && done && !done.querySelector('.bmasw-done')){ var p=document.createElement('p'); p.className='bmasw-done'; p.textContent='⏱ Time since sign-in: '+swFmt((Date.now()-CLK.t0)/1000); var h2=done.querySelector('h2'); if(h2) h2.insertAdjacentElement('afterend',p); else done.appendChild(p); } };

/* ================= scratchpad (Khan-style, 4 pens) ================= */
var SP={on:false, draw:true, color:'ink', size:3, erase:false, store:{}, key:null, cv:null, ctx:null, down:false, last:null};
var SP_COL={ink:null, blue:'#2563EB', red:'#DC2626', green:'#16A34A'};
function spInk(){ return getComputedStyle(document.documentElement).getPropertyValue('--ink').trim()||'#211E1A'; }
function spKey(){ var ts=swTab(); return ts ? (MODE+'|'+activeTab+'|'+ts.idx) : null; }
function spBuild(){
  if(SP.cv) return;
  var cv=document.createElement('canvas'); cv.id='spCanvas'; cv.className='sp-canvas'; document.body.appendChild(cv);
  var bar=document.createElement('div'); bar.id='spBar'; bar.className='sp-bar';
  bar.innerHTML='<span class="sp-lbl">✏️ Scratchpad</span>'+
    ['ink','blue','red','green'].map(function(c){ return '<button type="button" class="sp-pen" data-c="'+c+'" title="'+(c==='ink'?'black':c)+' pen"><i style="background:'+(c==='ink'?'var(--ink)':SP_COL[c])+'"></i></button>'; }).join('')+
    '<button type="button" class="sp-tool" data-t="erase" title="Eraser">🧽</button><button type="button" class="sp-tool" data-t="size" title="Pen size">●</button><button type="button" class="sp-tool" data-t="scroll" title="Pause drawing to scroll or answer">✋</button>'+
    '<button type="button" class="sp-tool" data-t="clear" title="Clear page">🗑</button><button type="button" class="sp-tool" data-t="close" title="Close scratchpad">✕</button>';
  document.body.appendChild(bar);
  bar.addEventListener('click',function(e){ var b=e.target.closest('button'); if(!b) return;
    if(b.dataset.c){ SP.color=b.dataset.c; SP.erase=false; SP.draw=true; }
    else if(b.dataset.t==='erase'){ SP.erase=true; SP.draw=true; }
    else if(b.dataset.t==='size'){ SP.size = SP.size===3?6:(SP.size===6?1.5:3); b.textContent = SP.size===6?'⬤':(SP.size===1.5?'·':'●'); }
    else if(b.dataset.t==='scroll'){ SP.draw=!SP.draw; }
    else if(b.dataset.t==='clear'){ spClear(); }
    else if(b.dataset.t==='close'){ spToggle(false); return; }
    spUI(); });
  SP.cv=cv; SP.ctx=cv.getContext('2d');
  cv.addEventListener('pointerdown',function(e){ if(!SP.draw) return; e.preventDefault(); cv.setPointerCapture(e.pointerId); SP.down=true; SP.last=spPt(e); spDot(SP.last); });
  cv.addEventListener('pointermove',function(e){ if(!SP.down) return; e.preventDefault(); var p=spPt(e); spLine(SP.last,p); SP.last=p; });
  var up=function(){ if(SP.down){ SP.down=false; spSave(); } };
  cv.addEventListener('pointerup',up); cv.addEventListener('pointercancel',up); cv.addEventListener('pointerleave',up);
  window.addEventListener('resize',function(){ if(SP.on) spFit(true); });
}
function spPt(e){ var r=SP.cv.getBoundingClientRect(); return {x:e.clientX-r.left, y:e.clientY-r.top}; }
function spStyle(){ var c=SP.ctx; c.lineCap='round'; c.lineJoin='round'; c.globalCompositeOperation=SP.erase?'destination-out':'source-over'; c.strokeStyle=c.fillStyle=(SP.color==='ink'?spInk():SP_COL[SP.color]); c.lineWidth=SP.erase?22:SP.size; }
function spDot(p){ spStyle(); var c=SP.ctx; c.beginPath(); c.arc(p.x,p.y,(SP.erase?11:SP.size/2),0,Math.PI*2); c.fill(); }
function spLine(a,b){ spStyle(); var c=SP.ctx; c.beginPath(); c.moveTo(a.x,a.y); c.lineTo(b.x,b.y); c.stroke(); }
function spSave(){ if(SP.key&&SP.cv){ try{ SP.store[SP.key]=SP.cv.toDataURL(); }catch(e){} } }
function spClear(){ if(!SP.ctx) return; SP.ctx.save(); SP.ctx.setTransform(1,0,0,1,0,0); SP.ctx.clearRect(0,0,SP.cv.width,SP.cv.height); SP.ctx.restore(); if(SP.key) delete SP.store[SP.key]; }
function spFit(keep){
  var wrap=document.getElementById('wrap'); if(!wrap||!SP.cv) return;
  var r=wrap.getBoundingClientRect(), top=r.top+window.scrollY, h=Math.max(wrap.scrollHeight, window.innerHeight-r.top)+40, w=document.documentElement.clientWidth;
  var old=keep&&SP.key?SP.store[SP.key]:null, dpr=window.devicePixelRatio||1;
  SP.cv.style.top=top+'px'; SP.cv.style.left='0px'; SP.cv.style.width=w+'px'; SP.cv.style.height=h+'px';
  SP.cv.width=Math.round(w*dpr); SP.cv.height=Math.round(h*dpr); SP.ctx.setTransform(dpr,0,0,dpr,0,0);
  if(old){ var im=new Image(); im.onload=function(){ SP.ctx.save(); SP.ctx.setTransform(1,0,0,1,0,0); SP.ctx.drawImage(im,0,0); SP.ctx.restore(); }; im.src=old; }
}
function spLoad(){ spSave(); SP.key=spKey(); spFit(false); var d=SP.key&&SP.store[SP.key]; if(d){ var im=new Image(); im.onload=function(){ SP.ctx.save(); SP.ctx.setTransform(1,0,0,1,0,0); SP.ctx.drawImage(im,0,0); SP.ctx.restore(); }; im.src=d; } }
function spUI(){
  var bar=document.getElementById('spBar'); if(!bar) return;
  bar.querySelectorAll('.sp-pen').forEach(function(b){ b.classList.toggle('on', !SP.erase && SP.draw && b.dataset.c===SP.color); });
  bar.querySelector('[data-t=erase]').classList.toggle('on', SP.erase && SP.draw);
  bar.querySelector('[data-t=scroll]').classList.toggle('on', !SP.draw);
  SP.cv.classList.toggle('passive', !SP.draw);
  var fb=document.getElementById('spFab'); if(fb) fb.classList.toggle('on',SP.on);
}
function spToggle(on){
  spBuild(); SP.on=(on===undefined)?!SP.on:on;
  document.body.classList.toggle('sp-open',SP.on); SP.cv.style.display=SP.on?'block':'none'; document.getElementById('spBar').style.display=SP.on?'flex':'none';
  if(SP.on){ SP.draw=true; SP.erase=false; spLoad(); if(typeof kbHide==='function') kbHide(); } else { spSave(); }
  spUI();
}
(function(){ var f=document.createElement('button'); f.type='button'; f.id='spFab'; f.className='sp-fab'; f.innerHTML='✏️ <span>Scratchpad</span>'; f.title='Open a scratchpad to write your working'; f.addEventListener('click',function(){ spToggle(); }); document.body.appendChild(f); })();
var _rsSP = renderSlide;
renderSlide = function(){ _rsSP(); var fab=document.getElementById('spFab'); var q=!!swTab(); if(fab) fab.style.display=q?'':'none'; if(!q && SP.on) spToggle(false); if(SP.on) setTimeout(spLoad,30); };

renderLogin();
})();
</script>
</body>
</html>
