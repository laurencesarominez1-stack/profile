<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Laurence Sarominez — Full Stack Developer</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,500;9..144,600;9..144,700&family=JetBrains+Mono:wght@400;500;600;700&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#15171d;
    --bg-side:#101217;
    --panel:#1b1e26;
    --panel-2:#20242e;
    --border:#2b2f3a;
    --amber:#e0a458;
    --amber-dim:#8a6a3c;
    --teal:#5fd6c4;
    --text:#eae7df;
    --text-dim:#9aa0ad;
    --text-faint:#5b6170;
    --serif:'Fraunces', serif;
    --mono:'JetBrains Mono', monospace;
    --sans:'Inter', sans-serif;
  }
  *{margin:0;padding:0;box-sizing:border-box;}
  html{scroll-behavior:smooth;}
  body{background:var(--bg);color:var(--text);font-family:var(--sans);}
  a{color:inherit;text-decoration:none;}
  ::selection{background:var(--amber);color:#15171d;}

  .layout{display:grid;grid-template-columns:230px 1fr;min-height:100vh;}

  /* SIDEBAR — file explorer */
  .sidebar{
    background:var(--bg-side);border-right:1px solid var(--border);
    padding:28px 0;position:sticky;top:0;height:100vh;overflow-y:auto;
  }
  .side-brand{padding:0 22px 26px;border-bottom:1px solid var(--border);margin-bottom:18px;}
  .side-brand .name{font-family:var(--serif);font-weight:600;font-size:19px;line-height:1.15;}
  .side-brand .role{font-family:var(--mono);font-size:10.5px;color:var(--teal);margin-top:6px;letter-spacing:.04em;}
  .explorer-label{padding:0 22px;font-family:var(--mono);font-size:10px;color:var(--text-faint);letter-spacing:.14em;margin-bottom:10px;}
  .file-item{
    display:flex;align-items:center;gap:9px;padding:9px 22px;font-family:var(--mono);font-size:12.5px;
    color:var(--text-dim);cursor:pointer;border-left:2px solid transparent;transition:all .15s ease;
  }
  .file-item:hover{background:rgba(255,255,255,0.03);color:var(--text);}
  .file-item.active{background:rgba(224,164,88,0.08);border-left-color:var(--amber);color:var(--amber);}
  .file-item .dot{width:6px;height:6px;border-radius:50%;background:currentColor;opacity:.7;flex-shrink:0;}
  .sidebar-footer{padding:22px;margin-top:20px;border-top:1px solid var(--border);}
  .status-line{font-family:var(--mono);font-size:10.5px;color:var(--text-faint);display:flex;align-items:center;gap:7px;}
  .status-line .blip{width:6px;height:6px;border-radius:50%;background:var(--teal);box-shadow:0 0 6px var(--teal);animation:blip 1.8s infinite;}
  @keyframes blip{0%,100%{opacity:1}50%{opacity:.3}}

  .main{width:100%;padding:0 0 40px;}

  /* TOPBAR / tabs */
  .topbar{
    display:flex;align-items:center;gap:2px;background:var(--panel);border-bottom:1px solid var(--border);
    padding:0 20px;position:sticky;top:0;z-index:20;overflow-x:auto;
  }
  .tab{
    font-family:var(--mono);font-size:12px;padding:13px 16px;color:var(--text-faint);white-space:nowrap;
    border-bottom:2px solid transparent;cursor:pointer;
  }
  .tab.active{color:var(--amber);border-bottom-color:var(--amber);}

  /* HERO — terminal window */
  .hero{padding:64px 48px 30px;max-width:1320px;margin:0 auto;}
  .term-window{
    background:#0e1015;border:1px solid var(--border);border-radius:12px;overflow:hidden;
    box-shadow:0 30px 70px -25px rgba(0,0,0,0.6);
  }
  .term-bar{display:flex;align-items:center;gap:8px;padding:12px 16px;background:#15171d;border-bottom:1px solid var(--border);}
  .term-dot{width:11px;height:11px;border-radius:50%;}
  .term-bar .t-label{margin-left:8px;font-family:var(--mono);font-size:11.5px;color:var(--text-faint);}
  .term-body{padding:30px 34px 36px;font-family:var(--mono);font-size:14px;line-height:1.9;}
  .term-body .prompt{color:var(--teal);}
  .term-body .comment{color:var(--text-faint);}
  .hero-name{
    font-family:var(--serif);font-size:clamp(38px,5.2vw,58px);font-weight:600;line-height:1.05;margin:14px 0 6px;
    color:var(--text);
  }
  .hero-name em{font-style:normal;color:var(--amber);}
  .cursor{display:inline-block;width:9px;height:1.1em;background:var(--amber);vertical-align:text-bottom;animation:caret 1s steps(1) infinite;margin-left:2px;}
  @keyframes caret{50%{opacity:0}}
  .hero-role{font-family:var(--mono);font-size:14.5px;color:var(--teal);margin-top:10px;}
  .hero-desc{color:var(--text-dim);font-size:14.5px;line-height:1.75;max-width:560px;margin-top:16px;}
  .hero-cta{display:flex;gap:12px;margin-top:28px;flex-wrap:wrap;}
  .btn{
    font-family:var(--mono);font-size:12.5px;font-weight:500;padding:12px 20px;border-radius:8px;
    display:inline-flex;align-items:center;gap:8px;cursor:pointer;transition:transform .18s ease, box-shadow .18s ease;
    border:1px solid transparent;
  }
  .btn:hover{transform:translateY(-2px);}
  .btn-amber{background:var(--amber);color:#1a1305;}
  .btn-amber:hover{box-shadow:0 10px 26px rgba(224,164,88,0.25);}
  .btn-ghost{background:transparent;border-color:var(--border);color:var(--text);}
  .btn-ghost:hover{border-color:var(--teal);color:var(--teal);}

  /* SECTIONS */
  .section{padding:64px 48px;border-top:1px solid var(--border);}
  .section > .sec-head, .section > .sec-sub, .section > div, .section > p{max-width:1320px;margin-left:auto;margin-right:auto;}
  .sec-head, .sec-sub{max-width:1320px;}
  .sec-head{display:flex;align-items:baseline;gap:14px;margin-bottom:38px;}
  .sec-num{font-family:var(--mono);color:var(--amber-dim);font-size:13px;}
  .sec-title{font-family:var(--serif);font-size:28px;font-weight:600;}
  .sec-sub{color:var(--text-dim);font-size:13.5px;margin-top:10px;max-width:520px;line-height:1.6;}

  /* ABOUT — code-block bio */
  .about-wrap{display:grid;grid-template-columns:1fr 1fr;gap:40px;}
  .code-block{
    background:var(--panel);border:1px solid var(--border);border-radius:10px;padding:26px 28px;
    font-family:var(--mono);font-size:12.5px;line-height:2;color:var(--text-dim);
  }
  .code-block .key{color:var(--teal);}
  .code-block .str{color:var(--amber);}
  .code-block .punct{color:var(--text-faint);}
  .facts-list{display:flex;flex-direction:column;gap:0;}
  .facts-list .row{display:flex;justify-content:space-between;padding:16px 0;border-bottom:1px solid var(--border);}
  .facts-list .row:last-child{border-bottom:none;}
  .facts-list .k{font-family:var(--mono);font-size:11.5px;color:var(--text-faint);letter-spacing:.05em;text-transform:uppercase;}
  .facts-list .v{font-size:14px;font-weight:500;}

  /* SKILLS — grouped tags */
  .skill-groups{display:flex;flex-direction:column;gap:22px;}
  .skill-group-row{display:grid;grid-template-columns:150px 1fr;gap:20px;align-items:start;padding:18px 0;border-bottom:1px solid var(--border);}
  .skill-group-row:last-child{border-bottom:none;}
  .sg-label{font-family:var(--mono);font-size:11.5px;color:var(--text-faint);letter-spacing:.06em;text-transform:uppercase;padding-top:6px;}
  .sg-tags{display:flex;flex-wrap:wrap;gap:9px;}
  .sg-tag{
    font-family:var(--mono);font-size:12.5px;padding:8px 14px;border-radius:7px;background:var(--panel);
    border:1px solid var(--border);color:var(--text);transition:border-color .2s ease;
  }
  .sg-tag:hover{border-color:var(--teal);color:var(--teal);}

  /* PROJECTS — list style */
  .proj-list{display:flex;flex-direction:column;}
  .proj-row{
    display:grid;grid-template-columns:36px 1fr auto;gap:22px;align-items:start;
    padding:26px 0;border-bottom:1px solid var(--border);
  }
  .proj-row:last-child{border-bottom:none;}
  .proj-idx{font-family:var(--mono);color:var(--amber-dim);font-size:12.5px;padding-top:3px;}
  .proj-name{font-family:var(--serif);font-size:19px;font-weight:600;}
  .proj-desc{color:var(--text-dim);font-size:13.5px;margin-top:8px;line-height:1.65;max-width:520px;}
  .proj-stack{display:flex;gap:8px;margin-top:12px;flex-wrap:wrap;}
  .proj-stack span{font-family:var(--mono);font-size:10.5px;color:var(--teal);}
  .proj-stack span::after{content:" · ";color:var(--text-faint);}
  .proj-stack span:last-child::after{content:"";}
  .proj-link{font-family:var(--mono);font-size:12px;color:var(--text-faint);white-space:nowrap;padding-top:3px;}
  .proj-row:hover .proj-link{color:var(--amber);}
  .proj-row:hover .proj-name{color:var(--amber);}

  /* EDUCATION */
  .edu-row{display:grid;grid-template-columns:110px 1fr;gap:24px;padding:20px 0;border-bottom:1px solid var(--border);}
  .edu-row:last-child{border-bottom:none;}
  .edu-time{font-family:var(--mono);font-size:12px;color:var(--text-faint);padding-top:3px;}
  .edu-title{font-family:var(--serif);font-size:18px;font-weight:600;}
  .edu-desc{color:var(--text-dim);font-size:13.5px;margin-top:8px;line-height:1.65;max-width:540px;}

  /* CONTACT */
  .contact-block{
    background:var(--panel);border:1px solid var(--border);border-radius:14px;padding:44px;
    display:grid;grid-template-columns:1fr 1fr;gap:40px;
  }
  .contact-block h3{font-family:var(--serif);font-size:24px;font-weight:600;}
  .contact-block p{color:var(--text-dim);font-size:13.5px;margin-top:12px;line-height:1.7;max-width:380px;}
  .clink{display:flex;align-items:center;gap:12px;font-family:var(--mono);font-size:12.5px;color:var(--text-dim);margin-top:14px;}
  .clink .ic{width:30px;height:30px;border-radius:8px;background:var(--panel-2);display:flex;align-items:center;justify-content:center;flex-shrink:0;border:1px solid var(--border);}
  .field{margin-bottom:14px;}
  .field label{font-family:var(--mono);font-size:10.5px;color:var(--text-faint);letter-spacing:.06em;text-transform:uppercase;display:block;margin-bottom:7px;}
  .field input, .field textarea{
    width:100%;background:var(--panel-2);border:1px solid var(--border);border-radius:8px;padding:12px 14px;
    color:var(--text);font-family:var(--sans);font-size:13.5px;
  }
  .field textarea{resize:none;min-height:80px;}
  .field input:focus, .field textarea:focus{outline:1px solid var(--amber);border-color:transparent;}

  footer{padding:30px 48px;font-family:var(--mono);font-size:11px;color:var(--text-faint);border-top:1px solid var(--border);}

  .nav-toggle{display:none;}

  @media (max-width:880px){
    .layout{grid-template-columns:1fr;}
    .sidebar{position:relative;height:auto;padding:18px 0;}
    .hero, .section{padding:44px 22px;}
    .about-wrap{grid-template-columns:1fr;}
    .skill-group-row{grid-template-columns:1fr;}
    .contact-block{grid-template-columns:1fr;padding:26px;}
    .proj-row{grid-template-columns:28px 1fr;}
    .proj-link{grid-column:2;}
    .edu-row{grid-template-columns:1fr;}
  }
</style>
</head>
<body>

<div class="layout">
  <aside class="sidebar">
    <div class="side-brand">
      <div class="name">Laurence<br>Sarominez</div>
      <div class="role">FULL STACK DEV</div>
    </div>
    <div class="explorer-label">EXPLORER</div>
    <a class="file-item active" href="#home"><span class="dot"></span>home.tsx</a>
    <a class="file-item" href="#about"><span class="dot"></span>about.md</a>
    <a class="file-item" href="#skills"><span class="dot"></span>skills.json</a>
    <a class="file-item" href="#projects"><span class="dot"></span>projects/</a>
    <a class="file-item" href="#education"><span class="dot"></span>education.md</a>
    <a class="file-item" href="#contact"><span class="dot"></span>contact.sh</a>
    <div class="sidebar-footer">
      <div class="status-line"><span class="blip"></span>available for work</div>
    </div>
  </aside>

  <main class="main">
    <div class="topbar" id="topbar">
      <div class="tab active" data-target="home">home.tsx</div>
      <div class="tab" data-target="about">about.md</div>
      <div class="tab" data-target="skills">skills.json</div>
      <div class="tab" data-target="projects">projects/</div>
      <div class="tab" data-target="education">education.md</div>
      <div class="tab" data-target="contact">contact.sh</div>
    </div>

    <section class="hero" id="home">
      <div class="term-window">
        <div class="term-bar">
          <div class="term-dot" style="background:#e0645c"></div>
          <div class="term-dot" style="background:#e0b25c"></div>
          <div class="term-dot" style="background:#5fd6a4"></div>
          <span class="t-label">home.tsx — zsh</span>
        </div>
        <div class="term-body">
          <div><span class="prompt">$</span> whoami</div>
          <div class="hero-name">Laurence <em>Sarominez</em><span class="cursor"></span></div>
          <div class="hero-role">const role = "Fresh Graduate · BS Information Technology · Full Stack Developer"</div>
          <p class="hero-desc"><span class="comment">// </span>I design and build responsive interfaces, practical backend systems, and mobile apps — increasingly leaning into AI-assisted tooling and IoT-connected products.</p>
          <div class="hero-cta">
            <a href="data:application/pdf;base64,JVBERi0xLjQKJZOMi54gUmVwb3J0TGFiIEdlbmVyYXRlZCBQREYgZG9jdW1lbnQgKG9wZW5zb3VyY2UpCjEgMCBvYmoKPDwKL0YxIDIgMCBSIC9GMiAzIDAgUiAvRjMgNCAwIFIKPj4KZW5kb2JqCjIgMCBvYmoKPDwKL0Jhc2VGb250IC9IZWx2ZXRpY2EgL0VuY29kaW5nIC9XaW5BbnNpRW5jb2RpbmcgL05hbWUgL0YxIC9TdWJ0eXBlIC9UeXBlMSAvVHlwZSAvRm9udAo+PgplbmRvYmoKMyAwIG9iago8PAovQmFzZUZvbnQgL0hlbHZldGljYS1Cb2xkIC9FbmNvZGluZyAvV2luQW5zaUVuY29kaW5nIC9OYW1lIC9GMiAvU3VidHlwZSAvVHlwZTEgL1R5cGUgL0ZvbnQKPj4KZW5kb2JqCjQgMCBvYmoKPDwKL0Jhc2VGb250IC9IZWx2ZXRpY2EtT2JsaXF1ZSAvRW5jb2RpbmcgL1dpbkFuc2lFbmNvZGluZyAvTmFtZSAvRjMgL1N1YnR5cGUgL1R5cGUxIC9UeXBlIC9Gb250Cj4+CmVuZG9iago1IDAgb2JqCjw8Ci9Db250ZW50cyA5IDAgUiAvTWVkaWFCb3ggWyAwIDAgNjEyIDc5MiBdIC9QYXJlbnQgOCAwIFIgL1Jlc291cmNlcyA8PAovRm9udCAxIDAgUiAvUHJvY1NldCBbIC9QREYgL1RleHQgL0ltYWdlQiAvSW1hZ2VDIC9JbWFnZUkgXQo+PiAvUm90YXRlIDAgL1RyYW5zIDw8Cgo+PiAKICAvVHlwZSAvUGFnZQo+PgplbmRvYmoKNiAwIG9iago8PAovUGFnZU1vZGUgL1VzZU5vbmUgL1BhZ2VzIDggMCBSIC9UeXBlIC9DYXRhbG9nCj4+CmVuZG9iago3IDAgb2JqCjw8Ci9BdXRob3IgKGFub255bW91cykgL0NyZWF0aW9uRGF0ZSAoRDoyMDI2MDcwMzA5NTExNSswMCcwMCcpIC9DcmVhdG9yIChhbm9ueW1vdXMpIC9LZXl3b3JkcyAoKSAvTW9kRGF0ZSAoRDoyMDI2MDcwMzA5NTExNSswMCcwMCcpIC9Qcm9kdWNlciAoUmVwb3J0TGFiIFBERiBMaWJyYXJ5IC0gXChvcGVuc291cmNlXCkpIAogIC9TdWJqZWN0ICh1bnNwZWNpZmllZCkgL1RpdGxlICh1bnRpdGxlZCkgL1RyYXBwZWQgL0ZhbHNlCj4+CmVuZG9iago4IDAgb2JqCjw8Ci9Db3VudCAxIC9LaWRzIFsgNSAwIFIgXSAvVHlwZSAvUGFnZXMKPj4KZW5kb2JqCjkgMCBvYmoKPDwKL0ZpbHRlciBbIC9BU0NJSTg1RGVjb2RlIC9GbGF0ZURlY29kZSBdIC9MZW5ndGggMTg4MAo+PgpzdHJlYW0KR2F0bTs5bG8mSSZBQHNCbSZBSFdBND9eOjcvJ1NMUTxQWVVsclpyWkxMKz9xUGBVdCwkXDdxIWRpW0hOODRtbkI0JWM9PWZFKlc5cXNhPUhRT2NJXW5fTio4IWRMOVBYJU9PXiFhLFBRa181LENAJDcoKnJcLD8lNmgjSWZNOEtIXDZiPEUtNEU3UDkrTC0+QG4zLDQ1SyliU1dlIltIZTE1KWBcVDRiTi45XVFXRTw2OiIqcEEjTkc1IW50RFpdXUUyX08pVFdLTjhddUwkPVZfLWJwZC1NOjlybkwhSicsTFkzKnVnJWtDcD5ZUC1jYmNZazJcJUFNaC1tJD4uR2VrZDpIdHRLLk04LWBjJiNnQCo+US9dUDNeW0omLD5cJW1xT0xXTlFYMjssOyJ0UU5RZVxbMjQ4WSg/clUucW1ERy8qai1hcXNNRDtzUj5eMFUoTSxcOU5eKW11J0gmYCFBKmlrclpqRTU3VjpTUFZUZE5PajY9bzZuLkFoMGpvZzQ7YGo2RmhJN2htSWZSXzJZZVxvKC82ZFxMOCxlYnFyJHNrNlcmMWlKLlQqSkknJmNCXyxNK0g8UmJ0OitDazQ+YUFPWUJZWixfbDpyPlFNL0VhRCRUPUomKihKbHIiJC8zYygnME5LXFRPSXFlXV0xO2oiaFNFRFg9R1dWI0Bnb3FcVkF0K0QhL2ZGNVQtRj4nVWdQTzI0LCtvTnVnUTslS3NhQyNFNHRRVFFoNyZlciZUXyFDbChYXHM+XFNIWS5JMF9bbTBxJW9sRypeXTVFUDU9ImBjbyJlY2dBRFYhXWlgUzY8KUwkL0dWbCpMMFhwblUuK14qT05tNyFwLjQzYVQ1L0BYTyMyL11BInBPL2IxWjxYLDdmU0FKSURpREJvalA+JlZhW0MuODdENDtiTE9DRyNSImMrIjFQaW90LDsjWUFrU1slYTpONGoxSHRxPU1uLi1aS04rbDk6XlhFVW9NaDotWTQwaDxVVzw0aV1vS1JtXDlZPDQ9S2dDSSc1YXNMZC5iXzpPPUUpMiVnNWdpaUdKTk8hUU5oPVRvKmlvX1ZWNm9XN01TQFM0Iyw2TC5vYT5yZmJlNiNGS1FHbylKLGY4bFcvZ0JcP11faE0tKWhnNikzdEhdPSQxNzsqWlowWT1sMT82aTghZD1lUSNLSW5jMzU2KUssNj9JX1spaiszKmRnRyFLWzFoXWsxN1deTyZVRDpyJyQrUkVqJl5jNTFUOEhOMTRCQ2xZLkxGUnNjUkJeO1tTZ0Q8ZmA3Rltuc0JhZU5vRUBbRTIySmEkbUMkTU0xY19VQmhVRS06X29pQWE6Nzg7WyE2LEBLWlY7blNZWl5cTjAmTj4jZWY1P0Q9XihfMGgkUFIqMEwyIylsOmQrI0M0Rm4jNyQ/Y3FpbDQ2ZFxZTixqWUUrR0k9OHRaNW9YNVBGWj1LV19Xa2ohLC1rSXJbP1xjNFYuTk44QU1oR19HdU0/SCJxSzI2SE4mQTplQkVWYUYmOyI7Vm1HJyheUV1JcmZTZlZWZjAuY05vcktOSTdfK0VdOTFwM108ZGY+bHMiVjNWMU0wVDspbktTViUsVD9YM21TUEVPal1eYERbKDAzZEM7LHJyVjdedU9OJUFnIy9iXUtMcylxKFQoTlQ+WWFgTUhbdCshcnJuUlI6X0I5PCMtcEVhMVNPOiFSRVJsTWIhUEZVKGsnYi9qZl06Wywsaz1kMVFIPltSZz9OazRWdE0yVjAxaWcwKihvKV1PR2JfMVNAK0trJUhlZ0VscCxyWVowYERIPF0xQUg1PC5yck90Uz5DXyctNGNXJlNDSCQsVmdrW0tcKXErMypLc29fUkJtTSdnImo0UlZjNl0wOFBvJ1RnNkA4P19DcTxdXkpqSjlmR3JXLnNdVmY2Y2cuRz1GWUpbWTU1bm5XQmtZaTAwYzJaIyNZOltaQFolZT9VYj08JzstIiMyPW1HQ1FtTWEsRkdhPlxMTkEvJEZQNHBXR3U3O1s1THBVXyEqV3FcY1k2Ozw6KXMnQXQwL2hAK1pZUlw8M3FTW2NbR0tKKHEqW0hHI25zRlhPLmwqND4+TC9BbiJcRTVtNVwpLyI7XjU4KmphLUxHUDQ3PUskYixAU3Eoal0oIltdMkdjOTdXbkopNSJXQzA0WiFpYVlJMCNVVkU/YEtaRXAlPVotWG9Db1tYYyYjPjE8S2UtWjVHVWBBUFFtPCFtR2tAcVB0UTpyLzE1WmI/T2BTa05kRV0/IVsvSCY+W21CZ25PQ3JwZXRsP1FZV09XP1lcXSU2NkhEMURHYi9Ta1ZxRWImJFRHQV5uWWpLOlNvVlFoXm45K29PVDlraTBiP1xsLW5zMSNgOjhTRWxKZj1iMjpjRzZSIyM1InBUV0ZNKShcLEgrQms5UiQlJFJCOXNPX28jUUI2ZkdCMl9tNXRIZHUrcG5IQ2w7MkxFTS03ZmwpbWhUMDlXNjxxNE1aPF5NaGpGPEFgcipLfj5lbmRzdHJlYW0KZW5kb2JqCnhyZWYKMCAxMAowMDAwMDAwMDAwIDY1NTM1IGYgCjAwMDAwMDAwNjEgMDAwMDAgbiAKMDAwMDAwMDExMiAwMDAwMCBuIAowMDAwMDAwMjE5IDAwMDAwIG4gCjAwMDAwMDAzMzEgMDAwMDAgbiAKMDAwMDAwMDQ0NiAwMDAwMCBuIAowMDAwMDAwNjM5IDAwMDAwIG4gCjAwMDAwMDA3MDcgMDAwMDAgbiAKMDAwMDAwMDk2OCAwMDAwMCBuIAowMDAwMDAxMDI3IDAwMDAwIG4gCnRyYWlsZXIKPDwKL0lEIApbPGFmMDFiMGY0ZGFjYzZkOTkzNmRlMmUyMTBhMzE2OTM2PjxhZjAxYjBmNGRhY2M2ZDk5MzZkZTJlMjEwYTMxNjkzNj5dCiUgUmVwb3J0TGFiIGdlbmVyYXRlZCBQREYgZG9jdW1lbnQgLS0gZGlnZXN0IChvcGVuc291cmNlKQoKL0luZm8gNyAwIFIKL1Jvb3QgNiAwIFIKL1NpemUgMTAKPj4Kc3RhcnR4cmVmCjI5OTgKJSVFT0YK" download="Laurence_Sarominez_Resume.pdf" class="btn btn-amber">⭳ resume.pdf</a>
            <a href="#projects" class="btn btn-ghost">→ ./projects</a>
            <a href="#contact" class="btn btn-ghost">✉ contact.sh</a>
          </div>
        </div>
      </div>
    </section>

    <section class="section" id="about">
      <div class="sec-head"><span class="sec-num">01</span><span class="sec-title">About</span></div>
      <p class="sec-sub">A quick profile, in two formats.</p>
      <div class="about-wrap" style="margin-top:30px;">
        <div class="code-block">
<div><span class="key">"name"</span><span class="punct">:</span> <span class="str">"Laurence Sarominez"</span><span class="punct">,</span></div>
<div><span class="key">"graduated"</span><span class="punct">:</span> <span class="str">"2026"</span><span class="punct">,</span></div>
<div><span class="key">"degree"</span><span class="punct">:</span> <span class="str">"BS Information Technology"</span><span class="punct">,</span></div>
<div><span class="key">"focus"</span><span class="punct">:</span> <span class="str">"Web, Mobile, IoT"</span><span class="punct">,</span></div>
<div><span class="key">"currently"</span><span class="punct">:</span> <span class="str">"open to junior roles"</span></div>
        </div>
        <div class="facts-list">
          <div class="row"><span class="k">Base</span><span class="v">Philippines</span></div>
          <div class="row"><span class="k">Strengths</span><span class="v">React, Laravel, Flutter</span></div>
          <div class="row"><span class="k">Interested in</span><span class="v">AI-assisted tooling, IoT</span></div>
          <div class="row"><span class="k">Working style</span><span class="v">Ships end to end</span></div>
        </div>
      </div>
    </section>

    <section class="section" id="skills">
      <div class="sec-head"><span class="sec-num">02</span><span class="sec-title">Skills</span></div>
      <p class="sec-sub">Grouped by where each tool sits in the stack.</p>
      <div class="skill-groups" style="margin-top:30px;">
        <div class="skill-group-row">
          <div class="sg-label">Frontend</div>
          <div class="sg-tags"><span class="sg-tag">React</span><span class="sg-tag">Tailwind CSS</span><span class="sg-tag">JavaScript</span></div>
        </div>
        <div class="skill-group-row">
          <div class="sg-label">Backend</div>
          <div class="sg-tags"><span class="sg-tag">Laravel</span><span class="sg-tag">Node.js</span><span class="sg-tag">PHP</span><span class="sg-tag">REST APIs</span></div>
        </div>
        <div class="skill-group-row">
          <div class="sg-label">Mobile</div>
          <div class="sg-tags"><span class="sg-tag">Flutter</span><span class="sg-tag">Dart</span></div>
        </div>
        <div class="skill-group-row">
          <div class="sg-label">Data</div>
          <div class="sg-tags"><span class="sg-tag">MySQL</span><span class="sg-tag">Supabase</span></div>
        </div>
        <div class="skill-group-row">
          <div class="sg-label">Tooling</div>
          <div class="sg-tags"><span class="sg-tag">Git</span><span class="sg-tag">Figma</span><span class="sg-tag">Postman</span></div>
        </div>
      </div>
    </section>

    <section class="section" id="projects">
      <div class="sec-head"><span class="sec-num">03</span><span class="sec-title">Projects</span></div>
      <p class="sec-sub">A few things built end to end.</p>
      <div class="proj-list" style="margin-top:20px;">
        <div class="proj-row">
          <div class="proj-idx">01</div>
          <div>
            <div class="proj-name">Inventory Dashboard</div>
            <div class="proj-desc">Real-time stock tracking with role-based access and low-stock alerts for a small retail team.</div>
            <div class="proj-stack"><span>React</span><span>Laravel</span><span>MySQL</span></div>
          </div>
          <div class="proj-link">view →</div>
        </div>
        <div class="proj-row">
          <div class="proj-idx">02</div>
          <div>
            <div class="proj-name">Campus Attendance</div>
            <div class="proj-desc">QR-based attendance app for students and faculty with offline sync support.</div>
            <div class="proj-stack"><span>Flutter</span><span>Supabase</span></div>
          </div>
          <div class="proj-link">view →</div>
        </div>
        <div class="proj-row">
          <div class="proj-idx">03</div>
          <div>
            <div class="proj-name">Smart Room Monitor</div>
            <div class="proj-desc">Sensor-fed dashboard showing live temperature, humidity, and occupancy data.</div>
            <div class="proj-stack"><span>React</span><span>Node.js</span><span>MQTT</span></div>
          </div>
          <div class="proj-link">view →</div>
        </div>
      </div>
    </section>

    <section class="section" id="education">
      <div class="sec-head"><span class="sec-num">04</span><span class="sec-title">Education</span></div>
      <div class="edu-row" style="margin-top:10px;">
        <div class="edu-time">2022 — 2026</div>
        <div>
          <div class="edu-title">Bachelor of Science in Information Technology</div>
          <div class="edu-desc">Coursework in software development, database systems, and networking fundamentals. Capstone: an IoT-enabled monitoring system with a connected web dashboard.</div>
        </div>
      </div>
    </section>

    <section class="section" id="contact">
      <div class="sec-head"><span class="sec-num">05</span><span class="sec-title">Contact</span></div>
      <p class="sec-sub">Open to junior developer roles, freelance work, and collaborations.</p>
      <div class="contact-block" style="margin-top:30px;">
        <div>
          <h3>Say hello</h3>
          <p>Have a role or a project in mind? I'd like to hear about it.</p>
          <div class="clink"><span class="ic">✉</span> laurence.sarominez@email.com</div>
          <div class="clink"><span class="ic">💼</span> linkedin.com/in/laurencesarominez</div>
          <div class="clink"><span class="ic">🐙</span> github.com/laurencesarominez</div>
        </div>
        <div>
          <div class="field"><label>Name</label><input type="text" placeholder="Your name"></div>
          <div class="field"><label>Email</label><input type="email" placeholder="you@email.com"></div>
          <div class="field"><label>Message</label><textarea placeholder="Tell me about your project"></textarea></div>
          <a href="#" class="btn btn-amber" style="width:100%;justify-content:center;">Send message</a>
        </div>
      </div>
    </section>

    <footer>© 2026 Laurence Sarominez — built line by line.</footer>
  </main>
</div>

<script>
  const files = document.querySelectorAll('.file-item');
  const tabs = document.querySelectorAll('.tab');
  const sections = document.querySelectorAll('section[id]');
  function setActive(id){
    files.forEach(f => f.classList.toggle('active', f.getAttribute('href') === '#'+id));
    tabs.forEach(t => t.classList.toggle('active', t.dataset.target === id));
  }
  window.addEventListener('scroll', () => {
    let current = 'home';
    sections.forEach(sec => { if(window.scrollY >= sec.offsetTop - 140) current = sec.id; });
    setActive(current);
  });
  tabs.forEach(t => t.addEventListener('click', () => {
    document.getElementById(t.dataset.target).scrollIntoView({behavior:'smooth'});
  }));
</script>

</body>
</html>
