[index.html](https://github.com/user-attachments/files/26381927/index.html)
<!DOCTYPE html>
<html lang="pt-BR">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Gerador de Etiquetas Hospitalares</title>

  <!-- Importando fonte corporativa e moderna -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;800&display=swap" rel="stylesheet">

  <style>
    /* Variáveis de estilo flexíveis */
    :root {
      --bg-color: #f0f4f8;
      --primary: #2563eb;
      --primary-hover: #1d4ed8;
      --secondary: #10b981;
      --secondary-hover: #059669;
      --text: #1e293b;
      --text-light: #64748b;
      --border: #e2e8f0;
      --card-bg: #ffffff;

      /* Variáveis injetadas pelo Configuração do usuário */
      --label-width: 240px;
      --label-height: 150px;
      --grid-cols: 3;
    }

    body {
      font-family: 'Inter', system-ui, -apple-system, sans-serif;
      /* Novo Fundo Hospitalar Muito Claro e Limpo (Azul Gelo) + Imagem Hospitalar */
      background: linear-gradient(135deg, rgba(224, 242, 254, 0.85), rgba(240, 248, 255, 0.95)), 
                  url('https://images.unsplash.com/photo-1516549655169-df83a0774514?q=80&w=2000&auto=format&fit=crop');
      background-size: cover;
      background-attachment: fixed;
      background-position: center;
      
      color: var(--text);
      margin: 0;
      padding: 40px 20px;
      transition: all 0.3s ease;
      min-height: 100vh;
    }

    /* Container Principal Estilo Glassmorphism (Como na imagem) */
    .glass-container {
      max-width: 900px;
      margin: 0 auto;
      background: rgba(255, 255, 255, 0.55);
      backdrop-filter: blur(24px);
      -webkit-backdrop-filter: blur(24px);
      border: 1px solid rgba(255, 255, 255, 0.8);
      border-radius: 28px;
      padding: 40px;
      box-shadow: 0 25px 50px -12px rgba(15, 23, 42, 0.15);
    }

    h1 {
      color: #0f172a; /* Azul Marinho super escuro */
      text-align: center;
      font-weight: 800;
      font-size: 2.4rem;
      margin-bottom: 40px;
      letter-spacing: -1px;
    }

    /* Abas - Estilo Pílula Oval Azul Claro */
    .tabs {
      display: flex;
      justify-content: center;
      gap: 15px;
      margin-bottom: 35px;
      flex-wrap: wrap;
    }

    .tab-btn {
      padding: 12px 26px;
      border: 1px solid rgba(255, 255, 255, 0.6);
      background: rgba(255, 255, 255, 0.65);
      cursor: pointer;
      border-radius: 9999px; /* Pílula 100% arredondada */
      font-weight: 600;
      font-size: 14px;
      color: #0369a1; /* Texto azul royal claro */
      transition: all 0.2s ease;
    }

    .tab-btn.active {
      background: #bae6fd; /* Azul pastel vivo */
      color: #082f49; /* Texto azul hiper escuro */
      border-color: #7dd3fc;
      box-shadow: 0 4px 14px rgba(56, 189, 248, 0.2);
    }

    .tab-btn:hover:not(.active) {
      transform: translateY(-2px);
      background: rgba(255, 255, 255, 0.9);
      color: #0284c7;
    }

    /* Conteúdo das Abas - Fundo Branco Leite */
    .tab-content {
      display: none;
      max-width: 100%;
      background: rgba(255, 255, 255, 0.95);
      padding: 35px;
      border-radius: 20px;
      box-shadow: inset 0 0 0 1px rgba(255,255,255,1), 0 10px 20px rgba(0,0,0,0.03);
      animation: fadeIn 0.3s ease-out forwards;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .tab-content.active {
      display: block;
    }

    h3 {
      margin-top: 0;
      color: #0f172a;
      font-size: 1.4rem;
      margin-bottom: 15px;
    }

    p {
      line-height: 1.6;
      color: var(--text-light);
    }

    /* Inputs de Texto */
    textarea {
      width: 100%;
      height: 220px;
      padding: 16px;
      font-family: ui-monospace, 'Cascadia Code', monospace;
      font-size: 14px;
      border: 2px solid var(--border);
      border-radius: 12px;
      background: #f8fafc;
      box-sizing: border-box;
      transition: border-color 0.2s;
      resize: vertical;
      outline: none;
      line-height: 1.5;
    }

    textarea:focus { border-color: var(--primary); background: #fff; }

    .form-group {
      margin-bottom: 20px;
      display: flex;
      flex-direction: column;
      gap: 8px;
    }

    label {
      font-weight: 600;
      color: var(--text);
      font-size: 14px;
    }

    input[type="url"], input[type="number"] {
      width: 100%;
      padding: 14px;
      border: 2px solid var(--border);
      border-radius: 12px;
      background: #f8fafc;
      font-size: 15px;
      outline: none;
      transition: all 0.2s;
    }

    input[type="number"] { width: 140px; }

    input[type="url"]:focus, input[type="number"]:focus {
      border-color: var(--primary);
      background: #fff;
      box-shadow: 0 0 0 3px rgba(37,99,235,0.1);
    }

    /* Botões - Completamente Arredondados */
    .btn {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      padding: 14px 28px;
      background: var(--secondary); /* Verde */
      color: #fff;
      border: none;
      border-radius: 9999px; /* Oval */
      cursor: pointer;
      font-size: 16px;
      font-weight: 600;
      transition: all 0.2s ease;
      margin-top: 10px;
      box-shadow: 0 6px 14px rgba(16, 185, 129, 0.25);
    }

    .btn:hover {
      background: var(--secondary-hover);
      transform: translateY(-2px);
      box-shadow: 0 8px 16px rgba(16, 185, 129, 0.35);
    }

    .btn:active { transform: translateY(1px); }

    .btn-print {
      background: var(--primary); /* Azul Forte */
      width: 100%;
      font-size: 18px;
      padding: 18px;
      box-shadow: 0 6px 14px rgba(37, 99, 235, 0.25);
    }

    .btn-print:hover {
      background: var(--primary-hover);
      box-shadow: 0 8px 16px rgba(37, 99, 235, 0.35);
    }

    /* Área de Impressão */
    #label-container {
      display: grid;
      grid-template-columns: repeat(var(--grid-cols), var(--label-width));
      gap: 15px;
      justify-content: center;
      margin-top: 40px;
      background: rgba(255,255,255,0.8);
      backdrop-filter: blur(10px);
      padding: 20px;
      border-radius: 16px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.1);
    }

    .label-box {
      width: var(--label-width);
      height: var(--label-height);
      border: 1px solid #000;
      background: #fff;
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: flex-start;
      padding: 2mm;
      box-sizing: border-box;
      overflow: hidden;
      border-radius: 8px;
      color: #000;
    }

    .label-box img {
      width: var(--qr-size, auto);
      height: var(--qr-size, 100%);
      object-fit: contain;
      margin-right: 2mm;
      flex-shrink: 0;
    }

    .label-content {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      flex: 1;
      height: 100%;
      text-align: center;
      overflow: hidden;
      min-width: 0;
      container-type: inline-size;
    }

    .label-box .code {
      font-weight: 800;
      font-size: min(var(--font-code, 1.15rem), 14cqi);
      margin-bottom: 1mm;
      letter-spacing: 0.5px;
      line-height: 1.1;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      max-width: 100%;
    }

    .label-box .product {
      font-size: var(--font-prod, 0.85rem);
      line-height: 1.1;
      font-weight: 600;
      display: -webkit-box;
      -webkit-line-clamp: 5;
      -webkit-box-orient: vertical;
      overflow: hidden;
      word-wrap: break-word;
      text-transform: uppercase;
    }

    .label-box.not-found {
      color: #ef4444;
      outline: 3px dashed #ef4444;
      background: #fef2f2;
    }

    /* MEDIA QUERIES PARA IMPRESSAO FÍSICA A4 */
    @media print {
      body {
        padding: 0;
        background: #fff !important;
        margin: 0;
      }

      .no-print {
        display: none !important;
      }

      #label-container {
        margin-top: 0;
        padding: 0;
        background: transparent !important;
        box-shadow: none;
        backdrop-filter: none;
        gap: 1mm;
        justify-content: start;
      }

      .label-box {
        border: 1px solid #000;
        border-radius: 0;
        box-sizing: border-box;
        page-break-inside: avoid;
      }

      @page {
        margin: 10mm;
      }
    }
  </style>
</head>

<body>

  <!-- Interface Gráfica -->
  <div class="no-print glass-container">
    <h1>Gerador de Etiquetas Inteligente</h1>

    <div class="tabs">
      <button class="tab-btn active" onclick="openTab('tab-db')">1. Banco de Dados</button>
      <button class="tab-btn" onclick="openTab('tab-sel')">2. Seleção</button>
      <button class="tab-btn" onclick="openTab('tab-cfg')">3. Configuração</button>
      <button class="tab-btn" onclick="openTab('tab-preview'); generateLabels();">4. Visualizar & Imprimir</button>
    </div>

    <!-- DB TAB -->
    <div id="tab-db" class="tab-content active">
      <h3>Sincronizar Dados</h3>
      <p>Cole abaixo o Link de Compartilhamento da sua planilha original. (Clique em Compartilhar > <b>"Qualquer pessoa com o link pode ler"</b> > Copiar Link).</p>
      <div class="form-group">
        <label>Link de Compartilhamento (Google Sheets)</label>
        <input type="url" id="db-input" placeholder="https://docs.google.com/spreadsheets/d/1LhOrAMHTciuV.../edit">
      </div>
      <button class="btn" onclick="saveDB()">🔄 Sincronizar Agora</button>
      <span id="db-msg" style="color:var(--secondary); font-weight:600; margin-left:15px;"></span>
      <p style="font-size:14px; font-weight:600; margin-top:20px;" id="db-status"></p>
    </div>

    <!-- SELECTION TAB -->
    <div id="tab-sel" class="tab-content">
      <h3>Ações e Sincronização</h3>
      <p>Digite, bipe (com leitor de código de barras) ou cole todos os códigos dos produtos que deseja emitir em
        etiquetas. Colocar <b>um código por linha</b>.</p>
      <textarea id="sel-input" placeholder="1001&#10;1002&#10;1001"></textarea>
      <button class="btn" style="background:#2563eb;" onclick="saveSel()">💾 Salvar Códigos</button>
      <span id="sel-msg" style="color:#2563eb; font-weight:600; margin-left:15px;"></span>
    </div>

    <!-- CONFIG TAB -->
    <div id="tab-cfg" class="tab-content">
      <h3>Layout e Papel de Impressão</h3>
      <div class="form-group">
        <label>Largura Fixa da Etiqueta (mm)</label>
        <input type="number" step="1" id="cfg-w" value="65">
      </div>
      <div class="form-group">
        <label>Altura Fixa da Etiqueta (mm)</label>
        <input type="number" step="1" id="cfg-h" value="30">
      </div>
      <div class="form-group">
        <label>Quantidade de colunas na folha</label>
        <input type="number" id="cfg-cols" value="3">
      </div>

      <button class="btn" style="background:#2563eb;" onclick="saveCfg()">⚙️ Aplicar e Salvar Ajustes</button>
      <span id="cfg-msg" style="color:#2563eb; font-weight:600; margin-left:15px;"></span>
    </div>

    <!-- PREVIEW TAB -->
    <div id="tab-preview" class="tab-content">
      <h3>Visualizar Grade de Impressão</h3>
      <p>Abaixo está o preview fiel do recorte das etiquetas baseado em sua configuração. Ajuste caso o corte caia sobre
        algum texto na configuração e depois clique no botão abaixo.</p>
      <button class="btn btn-print" onclick="window.print()">🖨️ IMPRIMIR ETIQUETAS (Ctrl + P)</button>
    </div>
  </div>

  <!-- Container da Grade Visível Constantemente Pós Geração -->
  <div id="label-container" class="no-print" style="display:none;"></div>

  <!-- Lógica em Javascript Local -->
  <script>
    // Hooks no DOM
    const elDbInput = document.getElementById('db-input');
    const elSelInput = document.getElementById('sel-input');
    const elCfgW = document.getElementById('cfg-w');
    const elCfgH = document.getElementById('cfg-h');
    const elCfgCols = document.getElementById('cfg-cols');
    const container = document.getElementById('label-container');
    const dbStatus = document.getElementById('db-status');

    // Inicialização
    window.onload = () => {
      elDbInput.value = localStorage.getItem('etiquetas_db_url') || '';
      elSelInput.value = localStorage.getItem('etiquetas_sel') || '';
      if (localStorage.getItem('etiquetas_cfg_w')) elCfgW.value = localStorage.getItem('etiquetas_cfg_w');
      if (localStorage.getItem('etiquetas_cfg_h')) elCfgH.value = localStorage.getItem('etiquetas_cfg_h');
      if (localStorage.getItem('etiquetas_cfg_cols')) elCfgCols.value = localStorage.getItem('etiquetas_cfg_cols');
      applyCSSVars();
      
      // Se houver um link de base de dados já preenchido e cache, ele avisa
      if(localStorage.getItem('etiquetas_db_json')){
         dbStatus.style.color = '#10b981';
         dbStatus.innerText = '✅ Banco de Dados Mestre disponível nativamente.';
      }
      if(elDbInput.value.trim().length > 10) saveDB(); // atualiza em background
    };

    // Switch de Abas
    function openTab(id) {
      document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
      document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
      document.getElementById(id).classList.add('active');
      event.currentTarget.classList.add('active');

      if (id === 'tab-preview') {
        container.style.display = 'grid'; // Retorna o display grid original
        container.classList.remove('no-print');
        if(!localStorage.getItem('etiquetas_db_json')) alert('Atenção: Banco de Dados Mestre ainda não baixado! Vá na primeira aba!');
      } else {
        container.style.display = 'none';
        container.classList.add('no-print');
        container.innerHTML = '';
      }
    }

    // Rotina Dinâmica e Infalível para Google Sheets
    async function saveDB() {
      let url = elDbInput.value.trim();
      if(!url) return;
      
      // Tenta extrair o ID oficial da planilha
      const match = url.match(/\/d\/([a-zA-Z0-9-_]+)/);
      if(!match || !match[1]) {
         dbStatus.style.color = '#ef4444';
         dbStatus.innerHTML = '❌ <b>Erro:</b> Link inválido. Pegue o link oficial em "Compartilhar > Copiar Link".';
         return;
      }
      
      const sheetId = match[1];
      localStorage.setItem('etiquetas_db_url', url);
      dbStatus.style.color = '#f59e0b';
      dbStatus.innerText = 'Buscando planilha online no Google... aguarde.';
      
      // Usando técnica JSONP que nunca é bloqueada
      const callbackName = 'gvizCallback_' + Date.now();
      const scriptUrl = `https://docs.google.com/spreadsheets/d/${sheetId}/gviz/tq?tq=&tqx=out:json;responseHandler:${callbackName}`;
      
      window[callbackName] = function(json) {
         try {
             // Limpeza após uso
             delete window[callbackName];
             const scr = document.getElementById(callbackName);
             if(scr) scr.remove();
             
             if(!json || !json.table || !json.table.rows) throw new Error('Dados nulos');
             
             const dbObj = {};
             json.table.rows.forEach(r => {
                 if(r.c && r.c[0] && r.c[0].v != null && r.c[0].v !== '') {
                     let cod = String(r.c[0].v).trim();
                     if (cod.toUpperCase() !== 'CODIGO' && cod.toUpperCase() !== 'COD') {
                         let prodStr = (r.c[1] && r.c[1].v) ? String(r.c[1].v).trim() : '';
                         let linkStr = (r.c[2] && r.c[2].v) ? String(r.c[2].v).trim() : '';
                         dbObj[cod] = { prod: prodStr, link: linkStr };
                     }
                 }
             });
             
             localStorage.setItem('etiquetas_db_json', JSON.stringify(dbObj));
             
             dbStatus.style.color = '#10b981';
             dbStatus.innerText = '✅ Planilha Online sincronizada e pronta!';
             showMsg('db-msg', 'Banco Local Atualizado ✔️');
         } catch(e) {
             console.error(e);
             dbStatus.style.color = '#ef4444';
             dbStatus.innerHTML = '❌ <b>Erro Interno:</b> Formato da planilha inesperado. Coluna 1 precisa ser Código, Coluna 2 Descrição.';
         }
      };
      
      const script = document.createElement('script');
      script.id = callbackName;
      script.src = scriptUrl;
      script.onerror = function() {
          dbStatus.style.color = '#ef4444';
          dbStatus.innerHTML = '❌ <b>Erro Rede:</b> O seu Google Sheets não está "Aberto para Qualquer um com o link" poder ler.';
      };
      document.body.appendChild(script);
    }

    function saveSel() {
      localStorage.setItem('etiquetas_sel', elSelInput.value);
      showMsg('sel-msg', 'Lista de Códigos salva ✔️');
    }

    function saveCfg() {
      localStorage.setItem('etiquetas_cfg_w', elCfgW.value);
      localStorage.setItem('etiquetas_cfg_h', elCfgH.value);
      localStorage.setItem('etiquetas_cfg_cols', elCfgCols.value);
      applyCSSVars();
      generateLabels();
      showMsg('cfg-msg', 'Ajustes Aplicados ✔️');
    }

    function showMsg(id, txt) {
      const m = document.getElementById(id);
      m.innerText = txt;
      setTimeout(() => m.innerText = '', 2500);
    }

    function applyCSSVars() {
      const r = document.documentElement;
      const w = parseFloat(elCfgW.value) || 65;
      const h = parseFloat(elCfgH.value) || 30;
      
      r.style.setProperty('--label-width', w + 'mm');
      r.style.setProperty('--label-height', h + 'mm');
      r.style.setProperty('--grid-cols', elCfgCols.value);
      
      const qrSize = Math.max(10, h - 4);
      r.style.setProperty('--qr-size', qrSize + 'mm');
      r.style.setProperty('--font-code', Math.max(1.5, h * 0.12) + 'mm');
      r.style.setProperty('--font-prod', Math.max(1.2, h * 0.08) + 'mm');
    }

    function generateLabels() {
      container.innerHTML = '';

      const jsonStr = localStorage.getItem('etiquetas_db_json');
      let dbMap = {};
      if(jsonStr) {
          try { dbMap = JSON.parse(jsonStr); } catch(e) {}
      }

      const selRaw = elSelInput.value.split(/\r?\n/);

      selRaw.forEach(rawItem => {
        const code = rawItem.trim();
        if (!code) return;

        const box = document.createElement('div');
        box.className = 'label-box';

        const data = dbMap[code];

        if (data) {
          let finalLink = data.link ? data.link : code; 
          let qrImgUrl = 'https://api.qrserver.com/v1/create-qr-code/?size=300x300&data=' + encodeURIComponent(finalLink);
          
          box.innerHTML = `
            <img src="${qrImgUrl}" alt="QR" onerror="this.src=''; this.alt='ERRO'">
            <div class="label-content">
              <div class="code">${code}</div>
              <div class="product">${data.prod}</div>
            </div>
          `;
        } else {
          box.classList.add('not-found');
          box.innerHTML = `
            <div style="font-size:32px; padding: 0 5px;">⚠️</div>
            <div class="label-content">
              <div class="code">${code}</div>
              <div class="product">CÓDIGO NÃO<br>ENCONTRADO</div>
            </div>
          `;
        }
        container.appendChild(box);
      });
    }
  </script>
</body>

</html>
