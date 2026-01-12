<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>Meu Perfil</title>
  <style>
    :root{
      --bg:#0f172a;
      --card:#1e293b;
      --text:#e5e7eb;
      --accent:#38bdf8;
      --radius:10px;
    }

    html,body{height:100%;}
    body {
      margin:0;
      font-family: Inter, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
      background:var(--bg);
      color:var(--text);
      display:flex;
      align-items:center;
      justify-content:center;
      padding:32px;
    }

    .container{
      width:100%;
      max-width:720px;
      text-align:center;
    }

    header h1{
      margin:0 0 18px 0;
      font-size:1.5rem;
      line-height:1.2;
    }

    .controls{
      display:flex;
      gap:12px;
      justify-content:center;
      flex-wrap:wrap;
      margin-bottom:18px;
    }

    .controls button{
      background:var(--accent);
      color:#04263a;
      border:0;
      padding:10px 16px;
      border-radius:8px;
      cursor:pointer;
      font-size:15px;
      transition:transform .12s ease, box-shadow .12s ease;
    }

    .controls button:focus{outline:3px solid rgba(56,189,248,0.22); outline-offset:3px;}
    .controls button:hover{transform:translateY(-2px); box-shadow:0 6px 18px rgba(0,0,0,0.4);}

    .card {
      display:block;
      margin:0 auto;
      margin-top:12px;
      background:var(--card);
      padding:20px;
      border-radius:var(--radius);
      max-width:640px;
      box-sizing:border-box;
      text-align:left;
      opacity:0;
      transform:translateY(6px);
      pointer-events:none;
      transition:opacity .22s ease, transform .22s ease;
    }

    .card[aria-hidden="false"]{
      opacity:1;
      transform:translateY(0);
      pointer-events:auto;
    }

    .card p{margin:8px 0; font-size:0.98rem;}

    .contact-row{
      display:flex;
      gap:12px;
      flex-wrap:wrap;
      align-items:center;
    }

    .link-like{
      color:var(--accent);
      text-decoration:none;
      background:transparent;
      border:0;
      padding:6px 10px;
      border-radius:8px;
      cursor:pointer;
      font-size:0.95rem;
    }

    .small{
      font-size:0.88rem;
      color:#cbd5e1;
    }

    footer{margin-top:18px; font-size:0.8rem; color:#94a3b8;}

    @media (max-width:420px){
      header h1{font-size:1.2rem;}
      .controls button{font-size:14px; padding:9px 12px;}
    }
  </style>
</head>
<body>
  <div class="container" role="main">
    <header>
      <h1>👋 Olá! Eu sou um desenvolvedor iniciante</h1>
    </header>

    <nav class="controls" role="tablist" aria-label="Seções do perfil">
      <button role="tab" aria-controls="sobre" aria-selected="true" data-target="sobre">👀 Sobre mim</button>
      <button role="tab" aria-controls="contato" aria-selected="false" data-target="contato">📫 Contato</button>
    </nav>

    <section id="sobre" class="card" role="tabpanel" aria-hidden="false" tabindex="0">
      <p>🌱 Iniciando na programação</p>
      <p>💞️ Interesse em design web e mobile</p>
      <p class="small">Estou aprendendo HTML, CSS e JavaScript — sempre construindo pequenos projetos para praticar.</p>
    </section>

    <section id="contato" class="card" role="tabpanel" aria-hidden="true" tabindex="0">
      <div class="contact-row">
        <a class="link-like" href="tel:+5511961222449">📞 +55 (11) 96122-2449</a>
        <button class="link-like" id="copy-phone" title="Copiar telefone">📋 Copiar</button>
      </div>
      <div style="height:8px;"></div>
      <div class="contact-row">
        <a class="link-like" href="mailto:v1c.saahaas@gmail.com">📧 v1c.saahaas@gmail.com</a>
        <button class="link-like" id="copy-email" title="Copiar email">📋 Copiar</button>
      </div>
      <p class="small">Clique no número para ligar (em celulares) ou em enviar email para abrir seu cliente de e-mail.</p>
    </section>

    <footer>
      <p>Feito com ♥ — sempre aprendendo.</p>
    </footer>
  </div>

  <script>
    (function(){
      const tabs = document.querySelectorAll('.controls [role="tab"]');
      const panels = document.querySelectorAll('[role="tabpanel"]');

      function show(id){
        panels.forEach(p => {
          const isTarget = p.id === id;
          p.setAttribute('aria-hidden', (!isTarget).toString());
        });
        tabs.forEach(t => {
          const selected = t.dataset.target === id;
          t.setAttribute('aria-selected', selected.toString());
          if (selected) t.focus();
        });
      }

      // initialize from tab selected attribute or default to first tab
      const initial = Array.from(tabs).find(t => t.getAttribute('aria-selected') === 'true') || tabs[0];
      show(initial.dataset.target);

      // click handlers
      tabs.forEach(t => {
        t.addEventListener('click', () => show(t.dataset.target));
        t.addEventListener('keydown', (e) => {
          // left/right arrow navigation
          const idx = Array.from(tabs).indexOf(t);
          if (e.key === 'ArrowRight') tabs[(idx+1) % tabs.length].click();
          if (e.key === 'ArrowLeft') tabs[(idx-1 + tabs.length) % tabs.length].click();
        });
      });

      // copy to clipboard helpers
      function copy(text, el){
        navigator.clipboard?.writeText(text).then(() => {
          const orig = el.innerText;
          el.innerText = '✅ Copiado';
          setTimeout(()=> el.innerText = orig, 1500);
        }).catch(()=> {
          alert('Não foi possível copiar. Selecione e copie manualmente.');
        });
      }

      const phoneBtn = document.getElementById('copy-phone');
      const emailBtn = document.getElementById('copy-email');
      phoneBtn && phoneBtn.addEventListener('click', () => copy('+55 (11) 96122-2449', phoneBtn));
      emailBtn && emailBtn.addEventListener('click', () => copy('v1c.saahaas@gmail.com', emailBtn));
    })();
  </script>
</body>
</html>
