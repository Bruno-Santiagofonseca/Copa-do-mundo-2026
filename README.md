
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Meu Álbum Copa 2026 ⚽</title>
  <link rel="manifest" href="./manifest.json">
  <meta name="theme-color" content="#009C3B">
  <meta name="apple-mobile-web-app-capable" content="yes">
  
  <script src="https://cdn-jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

  <style>
    :root {
      --verde: #009C3B;
      --amarelo: #FFDF00;
      --azul: #002776;
      --branco: #FFFFFF;
      --gramado: #15803D;
      --cinza-claro: #F3F4F6;
      --faltando: #E5E7EB;
      --colada: #22C55E;
      --repetida: #3B82F6;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
      -webkit-tap-highlight-color: transparent;
    }

    body {
      background-color: #0A192F;
      background-image: radial-gradient(var(--azul) 20%, transparent 80%);
      background-size: 100% 100%;
      color: #333;
      padding-bottom: 90px;
    }

    /* Topo Temático (Estilo Placar de Estádio) */
    .header {
      background: linear-gradient(180deg, var(--verde), var(--gramado));
      color: var(--branco);
      padding: 20px 15px;
      border-radius: 0 0 28px 28px;
      box-shadow: 0 6px 20px rgba(0,0,0,0.4);
      text-align: center;
      border-bottom: 4px solid var(--amarelo);
    }

    .profile-area {
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 15px;
      margin-bottom: 15px;
    }

    .avatar-container {
      position: relative;
      width: 75px;
      height: 75px;
      cursor: pointer;
    }

    .avatar {
      width: 100%;
      height: 100%;
      border-radius: 50%;
      border: 4px solid var(--amarelo);
      object-fit: cover;
      background-color: var(--branco);
    }

    .kid-name {
      font-size: 1.6rem;
      font-weight: 900;
      border: none;
      background: transparent;
      color: var(--branco);
      border-bottom: 3px dashed var(--amarelo);
      width: 160px;
      text-align: center;
      text-shadow: 2px 2px 0px var(--azul);
    }

    .kid-name:focus { outline: none; }

    /* Dashboard Principal (Tela Inicial) */
    .dashboard {
      background: var(--branco);
      margin: -15px 15px 20px 15px;
      padding: 20px;
      border-radius: 20px;
      box-shadow: 0 8px 16px rgba(0,0,0,0.2);
      border: 2px solid var(--amarelo);
    }

    .main-progress-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-weight: 900;
      font-size: 1.2rem;
      color: var(--azul);
      margin-bottom: 8px;
    }

    .progress-container {
      background-color: var(--cinza-claro);
      border-radius: 15px;
      height: 28px;
      width: 100%;
      overflow: hidden;
      margin-bottom: 12px;
      box-shadow: inset 0 3px 5px rgba(0,0,0,0.15);
      border: 1px solid #DDD;
    }

    .progress-bar {
      background: linear-gradient(90deg, var(--amarelo), #00C853);
      height: 100%;
      width: 0%;
      transition: width 0.6s cubic-bezier(0.4, 0, 0.2, 1);
    }

    .countdown-text {
      font-size: 0.95rem;
      font-weight: 700;
      text-align: center;
      color: #4B5563;
      margin-bottom: 15px;
      background: #FEF3C7;
      padding: 6px;
      border-radius: 8px;
    }

    .stats-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 6px;
      text-align: center;
    }

    .stat-card {
      padding: 10px 4px;
      border-radius: 12px;
      font-size: 0.75rem;
      font-weight: 800;
      box-shadow: 0 2px 4px rgba(0,0,0,0.05);
    }
    .stat-card span {
      display: block;
      font-size: 1.3rem;
      font-weight: 900;
      margin-top: 2px;
    }
    .card-tot { background-color: var(--cinza-claro); color: #374151;}
    .card-col { background-color: #DCFCE7; color: #15803D; border: 1px solid #BBF7D0; }
    .card-rep { background-color: #DBEAFE; color: #1D4ED8; border: 1px solid #BFDBFE; }
    .card-fal { background-color: #FEE2E2; color: #B91C1C; border: 1px solid #FECACA; }

    /* Seção de Conquistas (Medalhas) */
    .achievements-box {
      margin: 15px;
      background: var(--branco);
      padding: 15px;
      border-radius: 16px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.15);
    }
    .achievements-title {
      font-size: 1rem;
      font-weight: 800;
      color: var(--azul);
      margin-bottom: 10px;
      display: flex;
      align-items: center;
      gap: 5px;
    }
    .badge-row {
      display: flex;
      justify-content: space-around;
      gap: 10px;
    }
    .medal {
      font-size: 2rem;
      filter: grayscale(100%);
      opacity: 0.3;
      transition: all 0.5s ease;
      text-align: center;
      display: flex;
      flex-direction: column;
      font-weight: bold;
    }
    .medal span { font-size: 0.65rem; color: #6B7280; display: block; margin-top: 2px;}
    .medal.unlocked {
      filter: grayscale(0%);
      opacity: 1;
      transform: scale(1.1);
    }

    /* Busca */
    .search-container { margin: 0 15px 15px 15px; }
    .search-input {
      width: 100%;
      padding: 14px 20px;
      border-radius: 30px;
      border: 3px solid var(--amarelo);
      font-size: 1.1rem;
      font-weight: bold;
      box-shadow: 0 4px 10px rgba(0,0,0,0.2);
      outline: none;
    }

    /* Conteúdos e Containers */
    .content-section {
      margin: 0 15px;
      background-color: var(--branco);
      border-radius: 20px;
      padding: 15px;
      box-shadow: 0 6px 15px rgba(0,0,0,0.2);
      display: none;
    }
    .content-section.active { display: block; }

    /* Seleções e Barras de Progresso Individuais */
    .team-container {
      margin-top: 15px;
      background-color: var(--cinza-claro);
      padding: 12px;
      border-radius: 16px;
      border: 1px solid #E5E7EB;
    }
    .team-header-info {
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-weight: bold;
      font-size: 0.95rem;
      margin-bottom: 6px;
    }
    .team-mini-bar-bg {
      background: #E5E7EB;
      height: 8px;
      border-radius: 4px;
      overflow: hidden;
      margin-bottom: 12px;
    }
    .team-mini-bar-fill {
      background: var(--verde);
      height: 100%;
      width: 0%;
      transition: width 0.4s ease;
    }

    /* Grid de Figurinhas */
    .stickers-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(58px, 1fr));
      gap: 8px;
    }

    .sticker-btn {
      aspect-ratio: 1;
      border: 2px solid #D1D5DB;
      border-radius: 14px;
      font-size: 1rem;
      font-weight: 800;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      transition: transform 0.1s, background-color 0.2s;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
      position: relative;
    }
    .sticker-btn:active { transform: scale(0.85); }

    .sticker-btn.status-0 { background-color: var(--faltando); color: #6B7280; }
    .sticker-btn.status-1 { background-color: var(--colada); color: white; border-color: #16A34A; }
    .sticker-btn.status-2 { background-color: var(--repetida); color: white; border-color: #2563EB; }

    .badge-rep {
      position: absolute;
      top: -4px;
      right: -4px;
      background-color: #EF4444;
      color: white;
      font-size: 0.75rem;
      padding: 2px 7px;
      border-radius: 10px;
      font-weight: 900;
      border: 1.5px solid white;
    }

    /* Cards de Repetidas */
    .rep-cards-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
      gap: 12px;
      margin-top: 15px;
    }
    .rep-card {
      background: linear-gradient(135deg, #DBEAFE, #EFF6FF);
      border: 3px solid var(--repetida);
      border-radius: 16px;
      padding: 12px;
      text-align: center;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
      font-weight: bold;
    }
    .rep-card .code {
      font-size: 1.2rem;
      color: var(--azul);
      display: block;
      margin-bottom: 5px;
    }
    .rep-card .counter {
      background: var(--repetida);
      color: white;
      padding: 4px 8px;
      border-radius: 20px;
      font-size: 0.85rem;
    }

    /* Ranking */
    .ranking-item {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 12px 15px;
      background: var(--cinza-claro);
      margin-bottom: 8px;
      border-radius: 12px;
      font-weight: bold;
    }
    .ranking-item:nth-child(1) { background: #FEF3C7; border: 2px solid var(--amarelo); }

    /* Mensagem Flutuante de Parabéns Completo */
    #congrats-modal {
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%) scale(0);
      background: var(--branco);
      padding: 25px;
      border-radius: 24px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.5);
      z-index: 1000;
      text-align: center;
      width: 85%;
      max-width: 320px;
      border: 4px solid var(--verde);
      transition: transform 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    }
    #congrats-modal.show { transform: translate(-50%, -50%) scale(1); }
    #congrats-modal h2 { color: var(--verde); font-size: 1.6rem; margin-bottom: 10px; }
    #congrats-modal button {
      background: var(--azul);
      color: white;
      border: none;
      padding: 10px 20px;
      border-radius: 12px;
      font-weight: bold;
      margin-top: 15px;
      cursor: pointer;
    }

    /* Navegação Inferior Ergonômica */
    .nav-bar {
      position: fixed;
      bottom: 0;
      left: 0;
      right: 0;
      height: 75px;
      background-color: var(--branco);
      display: flex;
      justify-content: space-around;
      align-items: center;
      box-shadow: 0 -5px 15px rgba(0,0,0,0.2);
      border-radius: 24px 24px 0 0;
      z-index: 100;
    }
    .nav-btn {
      background: none;
      border: none;
      display: flex;
      flex-direction: column;
      align-items: center;
      font-size: 0.8rem;
      font-weight: 800;
      color: #9CA3AF;
      cursor: pointer;
      width: 25%;
    }
    .nav-btn span:first-child {
      font-size: 1.7rem;
      margin-bottom: 2px;
      transition: transform 0.2s;
    }
    .nav-btn.active { color: var(--azul); }
    .nav-btn.active span:first-child { transform: scale(1.25); }

    .btn-action {
      flex: 1; padding: 14px; border: none; border-radius: 14px;
      font-weight: bold; color: white; cursor: pointer; font-size: 0.95rem;
    }
  </style>
</head>
<body>

  <div id="congrats-modal">
    <h2>🎉 PARABÉNS!</h2>
    <p id="congrats-text">Você completou um time!</p>
    <div style="font-size: 1.5rem; margin-top:10px;">⭐ ⭐ ⭐ ⭐ ⭐</div>
    <button onclick="closeCongrats()">Uau, que legal! ⚽</button>
  </div>

  <div class="header">
    <div class="profile-area">
      <div class="avatar-container" onclick="document.getElementById('avatar-input').click()">
        <img id="kid-avatar" class="avatar" src="https://cdn-icons-png.flaticon.com/512/5323/5323860.png" alt="Avatar">
        <input type="file" id="avatar-input" accept="image/*" style="display:none" onchange="loadAvatar(event)">
      </div>
      <div>
        <input type="text" id="kid-name-input" class="kid-name" value="Campeão" onchange="saveProfileName()">
      </div>
    </div>
  </div>

  <div class="dashboard">
    <div class="main-progress-header">
      <span>🏆 Álbum Copa 2026</span>
      <span id="txt-porcentagem">0%</span>
    </div>
    <div class="progress-container">
      <div id="barra-progresso" class="progress-bar"></div>
    </div>
    <div class="countdown-text" id="txt-restantes">
      Faltam apenas 0 figurinhas para completar seu álbum!
    </div>
    <div class="stats-grid">
      <div class="stat-card card-tot">Total<span id="stat-total">0</span></div>
      <div class="stat-card card-col">Coladas<span id="stat-coladas">0</span></div>
      <div class="stat-card card-rep">Repetidas<span id="stat-repetidas">0</span></div>
      <div class="stat-card card-fal">Faltam<span id="stat-faltam">0</span></div>
    </div>
  </div>

  <div class="achievements-box">
    <div class="achievements-title">🏅 Minhas Medalhas de Colecionador</div>
    <div class="badge-row">
      <div class="medal" id="medal-50">🥉<span id="lbl-m50">50 Fig.</span></div>
      <div class="medal" id="medal-250">🥈<span>250 Fig.</span></div>
      <div class="medal" id="medal-500">🥇<span>500 Fig.</span></div>
      <div class="medal" id="medal-100">🏆<span>100%</span></div>
    </div>
  </div>

  <div class="search-container">
    <input type="text" id="search" class="search-input" placeholder="🔍 Digite o número ou código (Ex: BRA 5)..." oninput="filterStickers()">
  </div>

  <div id="sec-album" class="content-section active">
    <div id="album-render"></div>
  </div>

  <div id="sec-repetidas" class="content-section">
    <h2 style="color: var(--azul);">🔄 Minhas Repetidas para Troca</h2>
    <div id="repetidas-render" class="rep-cards-grid"></div>
  </div>

  <div id="sec-ranking" class="content-section">
    <h2 style="color: var(--azul); margin-bottom: 15px;">📊 Seleções Mais Completas</h2>
    <div id="ranking-render"></div>
  </div>

  <div id="sec-mais" class="content-section">
    <h2 style="color: var(--azul);">Opções do Aplicativo ⚙️</h2>
    <div style="display:flex; gap:10px; margin-top:15px;">
      <button class="btn-action" style="background:#009C3B" onclick="exportBackup()">📥 Salvar Backup</button>
      <button class="btn-action" style="background:#002776" onclick="document.getElementById('file-input').click()">📤 Ler Backup</button>
      <input type="file" id="file-input" accept=".json" style="display:none" onchange="importBackup(event)">
    </div>
    <button onclick="resetData()" style="width:100%; padding:14px; margin-top:40px; background-color:#EF4444; color:white; border:none; border-radius:14px; font-weight:bold; cursor:pointer;">
      🚨 Apagar Tudo e Recomeçar do Zero
    </button>
  </div>

  <nav class="nav-bar">
    <button class="nav-btn active" id="btn-nav-album" onclick="switchSection('album')">
      <span>📖</span><span>Álbum</span>
    </button>
    <button class="nav-btn" id="btn-nav-rep" onclick="switchSection('repetidas')">
      <span>🔄</span><span>Repetidas</span>
    </button>
    <button class="nav-btn" id="btn-nav-ranking" onclick="switchSection('ranking')">
      <span>🏆</span><span>Ranking</span>
    </button>
    <button class="nav-btn" id="btn-nav-mais" onclick="switchSection('mais')">
      <span>⚙️</span><span>Opções</span>
    </button>
  </nav>

  <script>
    // Configuração Completa do Álbum da Copa 2026 (Bandeiras + Prefixos)
    const ALBUM_DATA = [
      {
        grupo: "Estádios e Especiais 🏟️",
        selecoes: [
          { nome: "Especiais 🌟", prefixo: "FWC", total: 10 }
        ]
      },
      {
        grupo: "Grupo A",
        selecoes: [
          { nome: "Brasil 🇧🇷", prefixo: "BRA", total: 18 },
          { nome: "Alemanha 🇩🇪", prefixo: "GER", total: 18 },
          { nome: "Catar 🇶🇦", prefixo: "QAT", total: 18 },
          { nome: "Equador 🇪🇨", prefixo: "ECU", total: 18 }
        ]
      },
      {
        grupo: "Grupo B",
        selecoes: [
          { nome: "Argentina 🇦🇷", prefixo: "ARG", total: 18 },
          { nome: "França 🇫🇷", prefixo: "FRA", total: 18 },
          { nome: "Inglaterra 🏴󠁧󠁢󠁥󠁮󠁧󠁿", prefixo: "ENG", total: 18 },
          { nome: "Estados Unidos 🇺🇸", prefixo: "USA", total: 18 }
        ]
      },
      {
        grupo: "Grupo C",
        selecoes: [
          { nome: "Espanha 🇪🇸", prefixo: "ESP", total: 18 },
          { nome: "Portugal 🇵🇹", prefixo: "POR", total: 18 },
          { nome: "Japão 🇯🇵", prefixo: "JPN", total: 18 },
          { nome: "Marrocos 🇲🇦", prefixo: "MAR", total: 18 }
        ]
      }
    ];

    let estadoFigurinhas = {};

    window.addEventListener('DOMContentLoaded', () => {
      loadProfile();
      initStickersData();
      renderAlbum();
      recalculateStats();
      registerServiceWorker();
    });

    function registerServiceWorker() {
      if ('serviceWorker' in navigator) {
        navigator.serviceWorker.register('./sw.js').catch(()=>null);
      }
    }

    function initStickersData() {
      const localData = localStorage.getItem('album_copa_2026_data');
      if (localData) {
        estadoFigurinhas = JSON.parse(localData);
      } else {
        ALBUM_DATA.forEach(g => {
          g.selecoes.forEach(sel => {
            for (let i = 1; i <= sel.total; i++) {
              estadoFigurinhas[`${sel.prefixo}-${i}`] = 0;
            }
          });
        });
        saveToStorage();
      }
    }

    function saveToStorage() {
      localStorage.setItem('album_copa_2026_data', JSON.stringify(estadoFigurinhas));
    }

    // Renderização Dinâmica com Mini Barras por Seleção
    function renderAlbum() {
      const container = document.getElementById('album-render');
      container.innerHTML = '';

      ALBUM_DATA.forEach(g => {
        const grupoDiv = document.createElement('div');
        grupoDiv.innerHTML = `<h2 style="background:var(--azul); color:white; padding:8px 12px; border-radius:8px; margin-top:20px; font-size:1.1rem;">${g.grupo}</h2>`;
        
        g.selecoes.forEach(sel => {
          const teamDiv = document.createElement('div');
          teamDiv.className = 'team-container';
          teamDiv.id = `section-team-${sel.prefixo}`;
          
          teamDiv.innerHTML = `
            <div class="team-header-info">
              <span>${sel.nome}</span>
              <span id="progress-txt-${sel.prefixo}">0/0 (0%)</span>
            </div>
            <div class="team-mini-bar-bg">
              <div id="progress-bar-${sel.prefixo}" class="team-mini-bar-fill"></div>
            </div>
          `;
          
          const grid = document.createElement('div');
          grid.className = 'stickers-grid';

          for (let i = 1; i <= sel.total; i++) {
            const idFig = `${sel.prefixo}-${i}`;
            const qtd = estadoFigurinhas[idFig] || 0;
            let statusClass = "status-0";
            if (qtd === 1) statusClass = "status-1";
            if (qtd > 1) statusClass = "status-2";

            const btn = document.createElement('button');
            btn.className = `sticker-btn ${statusClass}`;
            btn.id = `btn-${idFig}`;
            btn.setAttribute('data-id', idFig);
            btn.onclick = () => handleStickerClick(idFig, sel);
            btn.innerHTML = `<span>${i}</span>`;
            
            if (qtd > 1) {
              const badge = document.createElement('span');
              badge.className = 'badge-rep';
              badge.innerText = `+${qtd - 1}`;
              btn.appendChild(badge);
            }
            grid.appendChild(btn);
          }
          teamDiv.appendChild(grid);
          grupoDiv.appendChild(teamDiv);
        });
        container.appendChild(grupoDiv);
      });
    }

    function handleStickerClick(idFig, selecao) {
      let atual = estadoFigurinhas[idFig] || 0;
      let antigoEstado = atual;
      
      if (atual === 0) estadoFigurinhas[idFig] = 1;
      else if (atual === 1) estadoFigurinhas[idFig] = 2;
      else estadoFigurinhas[idFig] = 0;

      saveToStorage();
      updateStickerVisual(idFig);
      updateSingleTeamProgress(selecao);
      recalculateStats();

      // Checa se completou a seleção neste exato momento
      if(antigoEstado === 0 && estadoFigurinhas[idFig] === 1) {
        checkTeamCompletion(selecao);
      }
    }

    function updateStickerVisual(idFig) {
      const btn = document.getElementById(`btn-${idFig}`);
      if (!btn) return;
      const qtd = estadoFigurinhas[idFig] || 0;
      btn.className = "sticker-btn";
      const oldBadge = btn.querySelector('.badge-rep');
      if (oldBadge) oldBadge.remove();

      if (qtd === 0) btn.classList.add('status-0');
      else if (qtd === 1) btn.classList.add('status-1');
      else if (qtd > 1) {
        btn.classList.add('status-2');
        const badge = document.createElement('span');
        badge.className = 'badge-rep';
        badge.innerText = `+${qtd - 1}`;
        btn.appendChild(badge);
      }
    }

    // Atualiza a mini barra de progresso daquela seleção específica
    function updateSingleTeamProgress(sel) {
      let coladas = 0;
      for (let i = 1; i <= sel.total; i++) {
        if ((estadoFigurinhas[`${sel.prefixo}-${i}`] || 0) > 0) coladas++;
      }
      let pct = Math.round((coladas / sel.total) * 100);
      
      const txt = document.getElementById(`progress-txt-${sel.prefixo}`);
      const bar = document.getElementById(`progress-bar-${sel.prefixo}`);
      if(txt) txt.innerText = `${coladas}/${sel.total} (${pct}%)`;
      if(bar) bar.style.width = `${pct}%`;
    }

    // Disparador de Animação de Confetes e Alerta fofinho
    function checkTeamCompletion(sel) {
      let completo = true;
      for (let i = 1; i <= sel.total; i++) {
        if ((estadoFigurinhas[`${sel.prefixo}-${i}`] || 0) === 0) {
          completo = false; break;
        }
      }
      if(completo) {
        confetti({ particleCount: 150, spread: 80, origin: { y: 0.6 } });
        document.getElementById('congrats-text').innerText = `Você completou a seleção do ${sel.nome}!`;
        document.getElementById('congrats-modal').classList.add('show');
      }
    }

    function closeCongrats() {
      document.getElementById('congrats-modal').classList.remove('show');
    }

    // Recalcula Dashboard, Medalhas de Conquistas e Totais do Álbum
    function recalculateStats() {
      let total = 0;
      let coladas = 0;
      let repetidas = 0;

      // Primeiro passa atualizando as mini barras de todas
      ALBUM_DATA.forEach(g => {
        g.selecoes.forEach(sel => {
          let selColadas = 0;
          total += sel.total;
          for (let i = 1; i <= sel.total; i++) {
            let qtd = estadoFigurinhas[`${sel.prefixo}-${i}`] || 0;
            if (qtd > 0) { coladas++; selColadas++; }
            if (qtd > 1) repetidas += (qtd - 1);
          }
          let pctSel = Math.round((selColadas / sel.total) * 100);
          const txt = document.getElementById(`progress-txt-${sel.prefixo}`);
          const bar = document.getElementById(`progress-bar-${sel.prefixo}`);
          if(txt) txt.innerText = `${selColadas}/${sel.total} (${pctSel}%)`;
          if(bar) bar.style.width = `${pctSel}%`;
        });
      });

      let faltam = total - coladas;
      let pctGeral = total > 0 ? Math.round((coladas / total) * 100) : 0;

      document.getElementById('stat-total').innerText = total;
      document.getElementById('stat-coladas').innerText = coladas;
      document.getElementById('stat-repetidas').innerText = repetidas;
      document.getElementById('stat-faltam').innerText = faltam;
      document.getElementById('txt-porcentagem').innerText = `${pctGeral}%`;
      document.getElementById('barra-progresso').style.width = `${pctGeral}%`;
      document.getElementById('txt-restantes').innerText = `Faltam apenas ${faltam} figurinhas para completar seu álbum!`;

      // Regra de ativação automática das Medalhas
      if (coladas >= 50) document.getElementById('medal-50').classList.add('unlocked');
      else document.getElementById('medal-50').classList.remove('unlocked');

      if (coladas >= 250) document.getElementById('medal-250').classList.add('unlocked');
      else document.getElementById('medal-250').classList.remove('unlocked');

      if (coladas >= 500) document.getElementById('medal-500').classList.add('unlocked');
      else document.getElementById('medal-500').classList.remove('unlocked');

      if (pctGeral === 100) document.getElementById('medal-100').classList.add('unlocked');
      else document.getElementById('medal-100').classList.remove('unlocked');
    }

    // Tela de Repetidas em Formato de Cartões Coloridos
    function renderRepetidas() {
      const container = document.getElementById('repetidas-render');
      container.innerHTML = '';
      let temRepetida = false;

      for (let chave in estadoFigurinhas) {
        let qtd = estadoFigurinhas[chave];
        if (qtd > 1) {
          temRepetida = true;
          const card = document.createElement('div');
          card.className = 'rep-card';
          card.innerHTML = `
            <span class="code">🔄 ${chave}</span>
            <span class="counter">Qtd: ${qtd - 1}</span>
          `;
          container.appendChild(card);
        }
      }
      if (!temRepetida) {
        container.innerHTML = '<p style="grid-column: 1/-1; color:#9CA3AF; text-align:center; padding:20px;">Nenhuma repetida ainda! Jogue para ganhar! ⚽</p>';
      }
    }

    // Geração Dinâmica da Tela de Ranking Automático das Melhores Seleções
    function renderRanking() {
      const container = document.getElementById('ranking-render');
      container.innerHTML = '';
      let listaRanking = [];

      ALBUM_DATA.forEach(g => {
        g.selecoes.forEach(sel => {
          let selColadas = 0;
          for (let i = 1; i <= sel.total; i++) {
            if ((estadoFigurinhas[`${sel.prefixo}-${i}`] || 0) > 0) selColadas++;
          }
          listaRanking.push({
            nome: sel.nome,
            coladas: selColadas,
            total: sel.total,
            pct: Math.round((selColadas / sel.total) * 100)
          });
        });
      });

      // Ordena da mais completa para a menos completa
      listaRanking.sort((a,b) => b.pct - a.pct);

      listaRanking.forEach((item, index) => {
        let podio = `${index + 1}º`;
        if (index === 0) podio = "1️⃣ 🏆";
        if (index === 1) podio = "2️⃣";
        if (index === 2) podio = "3️⃣";

        const row = document.createElement('div');
        row.className = 'ranking-item';
        row.innerHTML = `
          <div><span>${podio}</span> <span style="margin-left:8px;">${item.nome}</span></div>
          <div style="color:var(--azul)">${item.coladas}/${item.total} (${item.pct}%)</div>
        `;
        container.appendChild(row);
      });
    }

    function filterStickers() {
      const termo = document.getElementById('search').value.toUpperCase().replace(/\s+/g, '-').trim();
      const botoes = document.querySelectorAll('.sticker-btn');

      botoes.forEach(btn => {
        const idFig = btn.getAttribute('data-id');
        const numPuro = idFig.split('-')[1];
        if (idFig.includes(termo) || numPuro === termo || termo === '') {
          btn.style.opacity = '1';
          btn.style.transform = 'scale(1)';
        } else {
          btn.style.opacity = '0.15';
          btn.style.transform = 'scale(0.85)';
        }
      });
    }

    function switchSection(secName) {
      document.querySelectorAll('.content-section').forEach(s => s.classList.remove('active'));
      document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));

      if (secName === 'album') {
        document.getElementById('sec-album').classList.add('active');
        document.getElementById('btn-nav-album').classList.add('active');
      } else if (secName === 'repetidas') {
        renderRepetidas();
        document.getElementById('sec-repetidas').classList.add('active');
        document.getElementById('btn-nav-rep').classList.add('active');
      } else if (secName === 'ranking') {
        renderRanking();
        document.getElementById('sec-ranking').classList.add('active');
        document.getElementById('btn-nav-ranking').classList.add('active');
      } else if (secName === 'mais') {
        document.getElementById('sec-mais').classList.add('active');
        document.getElementById('btn-nav-mais').classList.add('active');
      }
      window.scrollTo(0,0);
    }

    // Configurações do Avatar e Nome de Usuário
    function loadAvatar(event) {
      const reader = new FileReader();
      reader.onload = function() {
        document.getElementById('kid-avatar').src = reader.result;
        localStorage.setItem('album_copa_avatar', reader.result);
      }
      if(event.target.files[0]) reader.readAsDataURL(event.target.files[0]);
    }

    function saveProfileName() {
      localStorage.setItem('album_copa_nome', document.getElementById('kid-name-input').value);
    }

    function loadProfile() {
      const salvoNome = localStorage.getItem('album_copa_nome');
      const salvoAvatar = localStorage.getItem('album_copa_avatar');
      if (salvoNome) document.getElementById('kid-name-input').value = salvoNome;
      if (salvoAvatar) document.getElementById('kid-avatar').src = salvoAvatar;
    }

    // Backup
    function exportBackup() {
      const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(estadoFigurinhas));
      const downloadAnchor = document.createElement('a');
      downloadAnchor.setAttribute("href", dataStr);
      downloadAnchor.setAttribute("download", "meu_album_copa_2026.json");
      document.body.appendChild(downloadAnchor);
      downloadAnchor.click();
      downloadAnchor.remove();
    }

    function importBackup(event) {
      const fileReader = new FileReader();
      fileReader.onload = function(e) {
        try {
          const dadosImportados = JSON.parse(e.target.result);
          if (typeof dadosImportados === 'object') {
            estadoFigurinhas = dadosImportados;
            saveToStorage();
            renderAlbum();
            recalculateStats();
            alert("Seu álbum foi restaurado com sucesso! 🎉");
          }
        } catch { alert("Arquivo inválido."); }
      }
      if(event.target.files[0]) fileReader.readAsText(event.target.files[0]);
    }

    function resetData() {
      if(confirm("Deseja mesmo apagar todo o progresso do álbum?")) {
        localStorage.removeItem('album_copa_2026_data');
        initStickersData();
        renderAlbum();
        recalculateStats();
        switchSection('album');
      }
    }
  </script>
</body>
</html>