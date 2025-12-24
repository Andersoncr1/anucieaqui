<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Site de Divulgação Profissional</title>
  <meta name="description" content="Divulgação profissional com sistema completo de mensagens e notificações." />

  <!-- Firebase -->
  <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-database-compat.js"></script>

  <style>
    :root {
      --cor-primaria: #2563eb;
      --cor-secundaria: #1e293b;
      --cor-fundo: #f8fafc;
      --cor-texto: #0f172a;
    }

    * { margin:0; padding:0; box-sizing:border-box; font-family: Arial, Helvetica, sans-serif; }
    body { background: var(--cor-fundo); color: var(--cor-texto); }

    header {
      background: linear-gradient(135deg, var(--cor-primaria), #3b82f6);
      color:#fff; text-align:center; padding:60px 20px;
    }

    .btn {
      background:#fff; color:var(--cor-primaria);
      padding:14px 28px; border-radius:8px; text-decoration:none; font-weight:bold;
    }

    section { padding:60px 20px; max-width:1100px; margin:auto; }
    h2 { text-align:center; margin-bottom:30px; }

    .cards { display:grid; grid-template-columns:repeat(auto-fit,minmax(250px,1fr)); gap:20px; }
    .card { background:#fff; padding:25px; border-radius:12px; box-shadow:0 10px 25px rgba(0,0,0,.08); text-align:center; }

    form { background:#fff; padding:40px; border-radius:12px; max-width:600px; margin:auto; box-shadow:0 10px 25px rgba(0,0,0,.08); }
    input, textarea { width:100%; padding:12px; margin-bottom:15px; border-radius:8px; border:1px solid #cbd5f5; }
    button { width:100%; padding:14px; background:var(--cor-primaria); color:#fff; border:none; border-radius:8px; font-size:1.1rem; cursor:pointer; }

    #painel {
      position:fixed; bottom:20px; right:20px; width:320px; background:#fff;
      border-radius:12px; box-shadow:0 10px 30px rgba(0,0,0,.2); display:none; flex-direction:column;
    }

    #painel header { background:var(--cor-primaria); padding:10px; color:#fff; font-size:14px; }
    #mensagens { padding:10px; max-height:300px; overflow-y:auto; font-size:14px; }

    .msg { background:#f1f5f9; padding:8px; border-radius:6px; margin-bottom:8px; }

    footer { background:var(--cor-secundaria); color:#fff; text-align:center; padding:30px; }
  </style>
</head>
<body>

<header>
  <h1>Divulgação Online Profissional</h1>
  <p>Clientes reais, mensagens em tempo real e notificações automáticas</p>
  <a href="#contato" class="btn">Quero divulgar agora</a>
</header>

<section>
  <h2>Serviços</h2>
  <div class="cards">
    <div class="card"><h3>Divulgação</h3><p>Atraia clientes todos os dias.</p></div>
    <div class="card"><h3>Sites</h3><p>Sites rápidos e profissionais.</p></div>
    <div class="card"><h3>Automação</h3><p>Sistemas que trabalham 24h.</p></div>
  </div>
</section>

<section id="contato">
  <h2>Contato</h2>
  <form onsubmit="enviarMensagem(event)">
    <input id="nome" placeholder="Seu nome" required>
    <input id="email" type="email" placeholder="Seu email" required>
    <textarea id="mensagem" placeholder="Mensagem" required></textarea>
    <button>Enviar mensagem</button>
  </form>
</section>

<footer>
  © 2025 - Sistema Completo de Divulgação
</footer>

<!-- Painel Admin -->
<div id="painel">
  <header>📨 Mensagens Recebidas</header>
  <div id="mensagens"></div>
</div>

<audio id="som" src="https://assets.mixkit.co/active_storage/sfx/2869/2869-preview.mp3"></audio>

<script>
  // CONFIGURE SEU FIREBASE AQUI
  const firebaseConfig = {
    apiKey: "SUA_API_KEY",
    authDomain: "SEU_DOMINIO.firebaseapp.com",
    databaseURL: "https://SEU_DOMINIO.firebaseio.com",
    projectId: "SEU_DOMINIO",
  };

  firebase.initializeApp(firebaseConfig);
  const db = firebase.database();

  function enviarMensagem(e) {
    e.preventDefault();
    const nome = nomeEl.value;
    const email = emailEl.value;
    const texto = mensagemEl.value;

    db.ref('mensagens').push({ nome, email, texto, data: Date.now() });
    document.getElementById('som').play();
    alert('Mensagem enviada com sucesso!');
    e.target.reset();
  }

  const nomeEl = document.getElementById('nome');
  const emailEl = document.getElementById('email');
  const mensagemEl = document.getElementById('mensagem');

  const painel = document.getElementById('painel');
  const mensagensDiv = document.getElementById('mensagens');

  db.ref('mensagens').on('child_added', snap => {
    painel.style.display = 'flex';
    document.getElementById('som').play();
    const m = snap.val();
    mensagensDiv.innerHTML += `<div class="msg"><b>${m.nome}</b><br>${m.texto}</div>`;
  });
</script>

</body>
</html>
 # anucieaqui
