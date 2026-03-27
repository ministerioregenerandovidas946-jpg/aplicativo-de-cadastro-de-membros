<!doctype html>
<html lang="pt-BR" class="h-full">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cadastro - Ministério Regenerando Vidas</title>
  <script src="https://cdn.tailwindcss.com/3.4.17"></script>
  <script src="https://cdn.jsdelivr.net/npm/lucide@0.263.0/dist/umd/lucide.min.js"></script>
  <script src="/_sdk/element_sdk.js"></script>
  <script src="/_sdk/data_sdk.js"></script>
  <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600;700&amp;display=swap" rel="stylesheet">
  <style>
    * { font-family: 'Outfit', sans-serif; }
    .fade-in { animation: fadeIn 0.3s ease; }
    @keyframes fadeIn { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: translateY(0); } }
    .card-hover { transition: transform 0.2s, box-shadow 0.2s; }
    .card-hover:hover { transform: translateY(-2px); box-shadow: 0 8px 25px rgba(0,0,0,0.15); }
    input:focus, select:focus, textarea:focus { outline: none; box-shadow: 0 0 0 2px #d4a056; }
  </style>
  <style>body { box-sizing: border-box; }</style>
 </head>
 <body class="h-full">
  <div id="app" class="h-full w-full overflow-auto" style="background: #1a1a2e;"><!-- Header -->
   <header style="background: linear-gradient(135deg, #16213e 0%, #1a1a2e 100%); border-bottom: 2px solid #d4a056;">
    <div class="max-w-5xl mx-auto px-4 py-5 flex items-center justify-between flex-wrap gap-3">
     <div class="flex items-center gap-3">
      <div style="background: #d4a056; width:44px; height:44px; border-radius:12px;" class="flex items-center justify-center text-xl">
       ✝️
      </div>
      <div>
       <h1 id="el-church-name" class="text-xl font-bold" style="color: #d4a056;">Ministério Regenerando Vidas</h1>
       <p id="el-welcome-text" class="text-sm" style="color: #8a8a9a;">Gestão de Membros</p>
      </div>
     </div>
     <div class="flex items-center gap-2 flex-wrap">
      <div class="relative"><i data-lucide="search" style="color:#8a8a9a; position:absolute; left:10px; top:50%; transform:translateY(-50%); width:16px; height:16px;"></i> <input id="searchInput" type="text" placeholder="Buscar membro..." class="rounded-lg text-sm py-2 pl-8 pr-3" style="background:#0f3460; color:#e0e0e0; border:1px solid #2a2a4a; width:200px;" oninput="filterMembers()">
      </div><button onclick="openForm()" class="flex items-center gap-1 text-sm font-semibold px-4 py-2 rounded-lg" style="background:#d4a056; color:#1a1a2e;"> <i data-lucide="plus" style="width:16px;height:16px;"></i> Novo </button>
     </div>
    </div>
   </header><!-- Stats -->
   <div class="max-w-5xl mx-auto px-4 py-4">
    <div class="grid grid-cols-2 sm:grid-cols-4 gap-3">
     <div class="rounded-xl p-3 text-center" style="background:#16213e; border:1px solid #2a2a4a;">
      <p class="text-2xl font-bold" style="color:#d4a056;" id="statTotal">0</p>
      <p class="text-xs" style="color:#8a8a9a;">Total</p>
     </div>
     <div class="rounded-xl p-3 text-center" style="background:#16213e; border:1px solid #2a2a4a;">
      <p class="text-2xl font-bold" style="color:#4ecca3;" id="statAtivos">0</p>
      <p class="text-xs" style="color:#8a8a9a;">Ativos</p>
     </div>
     <div class="rounded-xl p-3 text-center" style="background:#16213e; border:1px solid #2a2a4a;">
      <p class="text-2xl font-bold" style="color:#e8b84b;" id="statInativos">0</p>
      <p class="text-xs" style="color:#8a8a9a;">Inativos</p>
     </div>
     <div class="rounded-xl p-3 text-center" style="background:#16213e; border:1px solid #2a2a4a;">
      <p class="text-2xl font-bold" style="color:#7b68ee;" id="statVisitantes">0</p>
      <p class="text-xs" style="color:#8a8a9a;">Visitantes</p>
     </div>
    </div>
   </div><!-- Filter -->
   <div class="max-w-5xl mx-auto px-4 pb-3 flex gap-2 flex-wrap"><button onclick="setFilter('todos')" class="filter-btn text-xs px-3 py-1 rounded-full font-medium" data-filter="todos" style="background:#d4a056; color:#1a1a2e;">Todos</button> <button onclick="setFilter('Ativo')" class="filter-btn text-xs px-3 py-1 rounded-full font-medium" data-filter="Ativo" style="background:#2a2a4a; color:#8a8a9a;">Ativos</button> <button onclick="setFilter('Inativo')" class="filter-btn text-xs px-3 py-1 rounded-full font-medium" data-filter="Inativo" style="background:#2a2a4a; color:#8a8a9a;">Inativos</button> <button onclick="setFilter('Visitante')" class="filter-btn text-xs px-3 py-1 rounded-full font-medium" data-filter="Visitante" style="background:#2a2a4a; color:#8a8a9a;">Visitantes</button>
   </div><!-- Member List -->
   <div class="max-w-5xl mx-auto px-4 pb-8">
    <div id="memberList"></div>
    <div id="emptyState" class="text-center py-16 fade-in" style="display:none;">
     <div class="text-5xl mb-3">
      🕊️
     </div>
     <p class="text-lg font-medium" style="color:#8a8a9a;">Nenhum membro cadastrado</p>
     <p class="text-sm" style="color:#5a5a6a;">Clique em "Novo" para adicionar o primeiro membro</p>
    </div>
    <div id="noResults" class="text-center py-16" style="display:none;">
     <p class="text-lg" style="color:#8a8a9a;">Nenhum resultado encontrado</p>
    </div>
   </div><!-- Limit Warning -->
   <div id="limitWarning" class="max-w-5xl mx-auto px-4 pb-4" style="display:none;">
    <div class="rounded-xl p-3 text-center text-sm font-medium" style="background:#4a2020; color:#f87171; border:1px solid #7f1d1d;">
     Limite de 999 membros atingido. Remova membros para adicionar novos.
    </div>
   </div><!-- Modal Form -->
   <div id="formModal" class="fixed inset-0 flex items-center justify-center p-4" style="display:none; z-index:50; background:rgba(0,0,0,0.7);">
    <div class="w-full max-w-lg rounded-2xl p-6 fade-in overflow-auto" style="background:#16213e; border:1px solid #2a2a4a; max-height:95%;">
     <div class="flex justify-between items-center mb-5">
      <h2 id="formTitle" class="text-lg font-bold" style="color:#d4a056;">Novo Membro</h2><button onclick="closeForm()" class="p-1 rounded-lg" style="color:#8a8a9a;"><i data-lucide="x" style="width:20px;height:20px;"></i></button>
     </div>
     <form id="memberForm" onsubmit="saveMember(event)" class="space-y-3">
      <div><label class="text-xs font-medium mb-1 block" style="color:#8a8a9a;" for="f-nome">Nome Completo *</label> <input id="f-nome" required class="w-full rounded-lg px-3 py-2 text-sm" style="background:#0f3460; color:#e0e0e0; border:1px solid #2a2a4a;">
      </div>
      <div class="grid grid-cols-2 gap-3">
       <div><label class="text-xs font-medium mb-1 block" style="color:#8a8a9a;" for="f-tel">Telefone</label> <input id="f-tel" class="w-full rounded-lg px-3 py-2 text-sm" style="background:#0f3460; color:#e0e0e0; border:1px solid #2a2a4a;">
       </div>
       <div><label class="text-xs font-medium mb-1 block" style="color:#8a8a9a;" for="f-nasc">Data Nascimento</label> <input id="f-nasc" type="date" class="w-full rounded-lg px-3 py-2 text-sm" style="background:#0f3460; color:#e0e0e0; border:1px solid #2a2a4a;">
       </div>
      </div>
      <div><label class="text-xs font-medium mb-1 block" style="color:#8a8a9a;" for="f-email">E-mail</label> <input id="f-email" type="email" class="w-full rounded-lg px-3 py-2 text-sm" style="background:#0f3460; color:#e0e0e0; border:1px solid #2a2a4a;">
      </div>
      <div><label class="text-xs font-medium mb-1 block" style="color:#8a8a9a;" for="f-end">Endereço</label> <input id="f-end" class="w-full rounded-lg px-3 py-2 text-sm" style="background:#0f3460; color:#e0e0e0; border:1px solid #2a2a4a;">
      </div>
      <div class="grid grid-cols-2 gap-3">
       <div><label class="text-xs font-medium mb-1 block" style="color:#8a8a9a;" for="f-funcao">Função</label> <select id="f-funcao" class="w-full rounded-lg px-3 py-2 text-sm" style="background:#0f3460; color:#e0e0e0; border:1px solid #2a2a4a;"> <option value="Membro">Membro</option> <option value="Pastor">Pastor</option> <option value="Diácono">Diácono</option> <option value="Líder de Louvor">Líder de Louvor</option> <option value="Professor EBD">Professor EBD</option> <option value="Obreiro">Obreiro</option> <option value="Secretário">Secretário</option> <option value="Tesoureiro">Tesoureiro</option> <option value="Visitante">Visitante</option> </select>
       </div>
       <div><label class="text-xs font-medium mb-1 block" style="color:#8a8a9a;" for="f-status">Status</label> <select id="f-status" class="w-full rounded-lg px-3 py-2 text-sm" style="background:#0f3460; color:#e0e0e0; border:1px solid #2a2a4a;"> <option value="Ativo">Ativo</option> <option value="Inativo">Inativo</option> <option value="Visitante">Visitante</option> </select>
       </div>
      </div>
      <div><label class="text-xs font-medium mb-1 block" style="color:#8a8a9a;" for="f-data-membro">Membro desde</label> <input id="f-data-membro" type="date" class="w-full rounded-lg px-3 py-2 text-sm" style="background:#0f3460; color:#e0e0e0; border:1px solid #2a2a4a;">
      </div>
      <div><label class="text-xs font-medium mb-1 block" style="color:#8a8a9a;" for="f-obs">Observações</label> <textarea id="f-obs" rows="2" class="w-full rounded-lg px-3 py-2 text-sm" style="background:#0f3460; color:#e0e0e0; border:1px solid #2a2a4a;"></textarea>
      </div>
      <div class="flex gap-2 pt-2"><button type="submit" id="btnSave" class="flex-1 py-2 rounded-lg text-sm font-semibold" style="background:#d4a056; color:#1a1a2e;">Salvar</button> <button type="button" onclick="closeForm()" class="px-4 py-2 rounded-lg text-sm" style="background:#2a2a4a; color:#8a8a9a;">Cancelar</button>
      </div>
     </form>
    </div>
   </div><!-- View Modal -->
   <div id="viewModal" class="fixed inset-0 flex items-center justify-center p-4" style="display:none; z-index:50; background:rgba(0,0,0,0.7);">
    <div class="w-full max-w-lg rounded-2xl p-6 fade-in overflow-auto" style="background:#16213e; border:1px solid #2a2a4a; max-height:95%;">
     <div class="flex justify-between items-center mb-5">
      <h2 class="text-lg font-bold" style="color:#d4a056;">Detalhes do Membro</h2><button onclick="closeView()" class="p-1 rounded-lg" style="color:#8a8a9a;"><i data-lucide="x" style="width:20px;height:20px;"></i></button>
     </div>
     <div id="viewContent" class="space-y-3"></div>
     <div class="flex gap-2 mt-5"><button id="btnEdit" class="flex-1 py-2 rounded-lg text-sm font-semibold flex items-center justify-center gap-1" style="background:#d4a056; color:#1a1a2e;"> <i data-lucide="edit" style="width:14px;height:14px;"></i> Editar </button> <button id="btnDelete" class="px-4 py-2 rounded-lg text-sm font-medium flex items-center justify-center gap-1" style="background:#4a2020; color:#f87171;"> <i data-lucide="trash-2" style="width:14px;height:14px;"></i> Excluir </button>
     </div>
     <div id="deleteConfirm" class="mt-3 p-3 rounded-lg text-center" style="display:none; background:#3a1515; border:1px solid #7f1d1d;">
      <p class="text-sm mb-2" style="color:#f87171;">Tem certeza que deseja excluir?</p>
      <div class="flex gap-2 justify-center"><button id="btnConfirmDel" class="px-4 py-1 rounded-lg text-sm font-semibold" style="background:#dc2626; color:white;">Sim, excluir</button> <button onclick="document.getElementById('deleteConfirm').style.display='none'" class="px-4 py-1 rounded-lg text-sm" style="background:#2a2a4a; color:#8a8a9a;">Cancelar</button>
      </div>
     </div>
    </div>
   </div><!-- Toast -->
   <div id="toast" class="fixed bottom-4 left-1/2 -translate-x-1/2 px-5 py-2 rounded-xl text-sm font-medium" style="display:none; z-index:60; background:#d4a056; color:#1a1a2e;"></div>
  </div>
  <script>
  let allMembers = [];
  let currentFilter = 'todos';
  let editingMember = null;
  let viewingMember = null;

  const defaultConfig = {
    church_name: 'Ministério Regenerando Vidas',
    welcome_text: 'Gestão de Membros',
    background_color: '#1a1a2e',
    accent_color: '#d4a056',
    card_color: '#16213e',
    text_color: '#e0e0e0',
    muted_color: '#8a8a9a',
    font_family: 'Outfit'
  };

  function applyConfig(config) {
    const bg = config.background_color || defaultConfig.background_color;
    const accent = config.accent_color || defaultConfig.accent_color;
    const card = config.card_color || defaultConfig.card_color;
    const text = config.text_color || defaultConfig.text_color;
    const muted = config.muted_color || defaultConfig.muted_color;
    const font = config.font_family || defaultConfig.font_family;

    document.getElementById('app').style.background = bg;
    document.getElementById('el-church-name').textContent = config.church_name || defaultConfig.church_name;
    document.getElementById('el-church-name').style.color = accent;
    document.getElementById('el-welcome-text').textContent = config.welcome_text || defaultConfig.welcome_text;
    document.getElementById('el-welcome-text').style.color = muted;

    document.querySelectorAll('#app *').forEach(el => {
      el.style.fontFamily = `${font}, Outfit, sans-serif`;
    });

    renderList();
  }

  window.elementSdk.init({
    defaultConfig,
    onConfigChange: async (config) => applyConfig(config),
    mapToCapabilities: (config) => ({
      recolorables: [
        { get: () => config.background_color || defaultConfig.background_color, set: v => { config.background_color = v; window.elementSdk.setConfig({ background_color: v }); } },
        { get: () => config.card_color || defaultConfig.card_color, set: v => { config.card_color = v; window.elementSdk.setConfig({ card_color: v }); } },
        { get: () => config.text_color || defaultConfig.text_color, set: v => { config.text_color = v; window.elementSdk.setConfig({ text_color: v }); } },
        { get: () => config.accent_color || defaultConfig.accent_color, set: v => { config.accent_color = v; window.elementSdk.setConfig({ accent_color: v }); } },
        { get: () => config.muted_color || defaultConfig.muted_color, set: v => { config.muted_color = v; window.elementSdk.setConfig({ muted_color: v }); } }
      ],
      borderables: [],
      fontEditable: {
        get: () => config.font_family || defaultConfig.font_family,
        set: v => { config.font_family = v; window.elementSdk.setConfig({ font_family: v }); }
      },
      fontSizeable: undefined
    }),
    mapToEditPanelValues: (config) => new Map([
      ['church_name', config.church_name || defaultConfig.church_name],
      ['welcome_text', config.welcome_text || defaultConfig.welcome_text]
    ])
  });

  const dataHandler = {
    onDataChanged(data) {
      allMembers = data;
      updateStats();
      renderList();
    }
  };

  (async () => {
    const r = await window.dataSdk.init(dataHandler);
    if (!r.isOk) console.error('Data SDK init failed');
  })();

  function updateStats() {
    document.getElementById('statTotal').textContent = allMembers.length;
    document.getElementById('statAtivos').textContent = allMembers.filter(m => m.status === 'Ativo').length;
    document.getElementById('statInativos').textContent = allMembers.filter(m => m.status === 'Inativo').length;
    document.getElementById('statVisitantes').textContent = allMembers.filter(m => m.status === 'Visitante').length;
    document.getElementById('limitWarning').style.display = allMembers.length >= 999 ? '' : 'none';
  }

  function getFiltered() {
    let list = allMembers;
    if (currentFilter !== 'todos') list = list.filter(m => m.status === currentFilter);
    const q = document.getElementById('searchInput').value.toLowerCase();
    if (q) list = list.filter(m => (m.nome || '').toLowerCase().includes(q) || (m.telefone || '').includes(q) || (m.funcao || '').toLowerCase().includes(q));
    return list;
  }

  function filterMembers() { renderList(); }

  function setFilter(f) {
    currentFilter = f;
    document.querySelectorAll('.filter-btn').forEach(b => {
      if (b.dataset.filter === f) { b.style.background = '#d4a056'; b.style.color = '#1a1a2e'; }
      else { b.style.background = '#2a2a4a'; b.style.color = '#8a8a9a'; }
    });
    renderList();
  }

  function statusColor(s) {
    if (s === 'Ativo') return '#4ecca3';
    if (s === 'Inativo') return '#f87171';
    return '#7b68ee';
  }

  function renderList() {
    const list = getFiltered();
    const container = document.getElementById('memberList');
    const empty = document.getElementById('emptyState');
    const noRes = document.getElementById('noResults');

    if (allMembers.length === 0) { container.innerHTML = ''; empty.style.display = ''; noRes.style.display = 'none'; return; }
    empty.style.display = 'none';
    if (list.length === 0) { container.innerHTML = ''; noRes.style.display = ''; return; }
    noRes.style.display = 'none';

    const existingMap = new Map([...container.children].map(el => [el.dataset.id, el]));
    const ids = new Set(list.map(m => m.__backendId));

    existingMap.forEach((el, id) => { if (!ids.has(id)) el.remove(); });

    list.forEach(m => {
      const id = m.__backendId;
      let card = existingMap.get(id);
      if (!card) {
        card = document.createElement('div');
        card.dataset.id = id;
        card.className = 'rounded-xl p-4 mb-2 cursor-pointer card-hover fade-in';
        card.style.cssText = 'background:#16213e; border:1px solid #2a2a4a;';
        card.onclick = () => openView(m.__backendId);
        container.appendChild(card);
      }
      card.onclick = () => openView(m.__backendId);
      card.innerHTML = `
        <div class="flex items-center justify-between gap-3">
          <div class="flex items-center gap-3 min-w-0">
            <div class="w-10 h-10 rounded-full flex items-center justify-center text-sm font-bold flex-shrink-0" style="background:#0f3460; color:#d4a056;">
              ${(m.nome || '?').charAt(0).toUpperCase()}
            </div>
            <div class="min-w-0">
              <p class="font-semibold text-sm truncate" style="color:#e0e0e0;">${m.nome || 'Sem nome'}</p>
              <p class="text-xs truncate" style="color:#8a8a9a;">${m.funcao || 'Membro'}${m.telefone ? ' • ' + m.telefone : ''}</p>
            </div>
          </div>
          <span class="text-xs px-2 py-0.5 rounded-full font-medium flex-shrink-0" style="background:${statusColor(m.status)}22; color:${statusColor(m.status)};">${m.status || 'Ativo'}</span>
        </div>`;
    });
  }

  function openForm(member) {
    editingMember = member || null;
    document.getElementById('formTitle').textContent = member ? 'Editar Membro' : 'Novo Membro';
    document.getElementById('f-nome').value = member ? member.nome || '' : '';
    document.getElementById('f-tel').value = member ? member.telefone || '' : '';
    document.getElementById('f-email').value = member ? member.email || '' : '';
    document.getElementById('f-nasc').value = member ? member.data_nascimento || '' : '';
    document.getElementById('f-end').value = member ? member.endereco || '' : '';
    document.getElementById('f-funcao').value = member ? member.funcao || 'Membro' : 'Membro';
    document.getElementById('f-status').value = member ? member.status || 'Ativo' : 'Ativo';
    document.getElementById('f-data-membro').value = member ? member.data_membro || '' : '';
    document.getElementById('f-obs').value = member ? member.observacoes || '' : '';
    document.getElementById('formModal').style.display = 'flex';
  }

  function closeForm() { document.getElementById('formModal').style.display = 'none'; editingMember = null; }

  async function saveMember(e) {
    e.preventDefault();
    const btn = document.getElementById('btnSave');
    btn.textContent = 'Salvando...'; btn.disabled = true;

    const data = {
      nome: document.getElementById('f-nome').value.trim(),
      telefone: document.getElementById('f-tel').value.trim(),
      email: document.getElementById('f-email').value.trim(),
      data_nascimento: document.getElementById('f-nasc').value,
      endereco: document.getElementById('f-end').value.trim(),
      funcao: document.getElementById('f-funcao').value,
      status: document.getElementById('f-status').value,
      data_membro: document.getElementById('f-data-membro').value,
      observacoes: document.getElementById('f-obs').value.trim()
    };

    let result;
    if (editingMember) {
      result = await window.dataSdk.update({ ...editingMember, ...data });
    } else {
      if (allMembers.length >= 999) { showToast('Limite de 999 membros atingido!'); btn.textContent = 'Salvar'; btn.disabled = false; return; }
      result = await window.dataSdk.create(data);
    }

    btn.textContent = 'Salvar'; btn.disabled = false;
    if (result.isOk) { showToast(editingMember ? 'Membro atualizado!' : 'Membro cadastrado!'); closeForm(); }
    else showToast('Erro ao salvar. Tente novamente.');
  }

  function openView(id) {
    const m = allMembers.find(x => x.__backendId === id);
    if (!m) return;
    viewingMember = m;
    const fields = [
      ['Nome', m.nome], ['Telefone', m.telefone], ['E-mail', m.email],
      ['Nascimento', m.data_nascimento], ['Endereço', m.endereco],
      ['Função', m.funcao], ['Status', m.status],
      ['Membro desde', m.data_membro], ['Observações', m.observacoes]
    ];
    document.getElementById('viewContent').innerHTML = fields.map(([l, v]) =>
      v ? `<div class="flex justify-between py-2" style="border-bottom:1px solid #2a2a4a;"><span class="text-xs" style="color:#8a8a9a;">${l}</span><span class="text-sm font-medium text-right" style="color:#e0e0e0;">${v}</span></div>` : ''
    ).join('');
    document.getElementById('deleteConfirm').style.display = 'none';
    document.getElementById('btnEdit').onclick = () => { closeView(); openForm(m); };
    document.getElementById('btnDelete').onclick = () => { document.getElementById('deleteConfirm').style.display = ''; };
    document.getElementById('btnConfirmDel').onclick = () => deleteMember(m);
    document.getElementById('viewModal').style.display = 'flex';
    lucide.createIcons();
  }

  function closeView() { document.getElementById('viewModal').style.display = 'none'; viewingMember = null; }

  async function deleteMember(m) {
    const btn = document.getElementById('btnConfirmDel');
    btn.textContent = 'Excluindo...'; btn.disabled = true;
    const r = await window.dataSdk.delete(m);
    btn.textContent = 'Sim, excluir'; btn.disabled = false;
    if (r.isOk) { showToast('Membro removido!'); closeView(); }
    else showToast('Erro ao excluir.');
  }

  function showToast(msg) {
    const t = document.getElementById('toast');
    t.textContent = msg; t.style.display = '';
    setTimeout(() => t.style.display = 'none', 2500);
  }

  lucide.createIcons();
</script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9e2c4e1471a4979a',t:'MTc3NDU5MjU5Mi4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
