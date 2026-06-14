# HABITOS-D-A
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<title>HábitosDía</title>
<style>
:root{
  --bg:#0d0d1a;--bg2:#13131f;--bg3:#1a1a2e;
  --surface:#1f1f35;--border:rgba(255,255,255,0.07);
  --accent:#7c3aed;--accent2:#a855f7;--gold:#f59e0b;
  --green:#10b981;--red:#ef4444;--text:#f1f0ff;--muted:#8b8aa8;
}
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;}
html,body{height:100%;background:#000;overscroll-behavior:none;}
body{
  font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;
  background:var(--bg);color:var(--text);
  max-width:480px;margin:0 auto;
  min-height:100vh;overflow-x:hidden;
}
#app{display:flex;flex-direction:column;height:100vh;height:100dvh;}

/* PANTALLAS */
.screen{display:none;flex:1;overflow-y:auto;padding-bottom:70px;-webkit-overflow-scrolling:touch;}
.screen.active{display:block;}
.topbar{padding:env(safe-area-inset-top,44px) 20px 16px;padding-top:max(env(safe-area-inset-top,0px),44px);background:linear-gradient(180deg,var(--bg3),var(--bg));}
.topbar h1{font-size:26px;font-weight:700;letter-spacing:-.5px;}
.topbar p{color:var(--muted);font-size:13px;margin-top:3px;text-transform:capitalize;}

/* NAV */
nav{
  position:fixed;bottom:0;left:50%;transform:translateX(-50%);
  width:100%;max-width:480px;
  background:var(--bg2);border-top:1px solid var(--border);
  display:flex;z-index:100;
  padding-bottom:env(safe-area-inset-bottom,0px);
}
.nav-btn{
  flex:1;display:flex;flex-direction:column;align-items:center;
  gap:3px;padding:10px 0 8px;cursor:pointer;
  border:none;background:transparent;color:var(--muted);
  font-size:10px;font-family:inherit;transition:color .2s;
}
.nav-btn .ico{font-size:22px;transition:transform .2s;}
.nav-btn.active{color:var(--accent2);}
.nav-btn.active .ico{transform:scale(1.2);}

/* ANILLO */
.ring-area{display:flex;align-items:center;justify-content:center;padding:20px 20px 12px;gap:20px;}
.ring-wrap{position:relative;width:110px;height:110px;flex-shrink:0;}
.ring-wrap svg{transform:rotate(-90deg);}
.ring-label{position:absolute;top:50%;left:50%;transform:translate(-50%,-50%);text-align:center;}
.ring-big{font-size:26px;font-weight:700;}
.ring-sm{font-size:11px;color:var(--muted);}
.stats-col{display:flex;flex-direction:column;gap:10px;}
.stat-pill{background:var(--surface);border-radius:14px;padding:10px 14px;display:flex;align-items:center;gap:10px;min-width:148px;}
.stat-pill .ico2{font-size:20px;}
.stat-pill .sv{font-size:20px;font-weight:700;}
.stat-pill .sl{font-size:11px;color:var(--muted);}

/* SECCIÓN */
.sec-title{font-size:11px;font-weight:600;letter-spacing:.08em;text-transform:uppercase;color:var(--muted);padding:0 20px;margin-bottom:10px;}

/* HÁBITOS */
.habit-card{
  margin:0 14px 10px;background:var(--surface);
  border:1px solid var(--border);border-radius:18px;
  padding:14px 16px;display:flex;align-items:center;gap:14px;
  cursor:pointer;position:relative;overflow:hidden;
  transition:transform .1s;user-select:none;
}
.habit-card:active{transform:scale(.97);}
.habit-card.done{border-color:rgba(124,58,237,.4);}
.habit-done-bg{position:absolute;inset:0;background:linear-gradient(90deg,rgba(124,58,237,.07),transparent);pointer-events:none;}
.habit-icon{width:46px;height:46px;border-radius:14px;display:flex;align-items:center;justify-content:center;font-size:24px;flex-shrink:0;}
.habit-info{flex:1;min-width:0;}
.habit-name{font-weight:500;font-size:15px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.habit-sub{font-size:12px;color:var(--muted);margin-top:2px;}
.prog{height:4px;background:rgba(255,255,255,.08);border-radius:99px;margin-top:8px;}
.prog-fill{height:100%;border-radius:99px;transition:width .4s ease;}
.check{
  width:32px;height:32px;border-radius:50%;flex-shrink:0;
  border:2px solid rgba(255,255,255,.15);
  display:flex;align-items:center;justify-content:center;
  font-size:15px;color:transparent;transition:all .25s;
}
.habit-card.done .check{background:var(--accent);border-color:var(--accent);color:#fff;}

/* FRASE */
.frase-box{margin:16px 14px 0;background:linear-gradient(135deg,var(--bg3),#1e1040);border:1px solid rgba(124,58,237,.2);border-radius:18px;padding:16px;}
.frase-q{font-size:14px;line-height:1.6;font-style:italic;}
.frase-a{font-size:12px;color:var(--accent2);margin-top:8px;}

/* STATS CARDS */
.stats-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px;padding:0 14px 14px;}
.stat-card{background:var(--surface);border:1px solid var(--border);border-radius:18px;padding:14px;}
.stat-card .lbl{font-size:11px;color:var(--muted);margin-bottom:6px;}
.stat-card .val{font-size:24px;font-weight:700;}
.stat-card .sub{font-size:11px;color:var(--muted);margin-top:2px;}

/* GRÁFICO */
.chart-box{margin:0 14px 14px;background:var(--surface);border:1px solid var(--border);border-radius:18px;padding:16px;}
.chart-box h3{font-size:14px;font-weight:500;margin-bottom:16px;}
.bar-chart{display:flex;align-items:flex-end;gap:5px;height:110px;}
.bar-col{flex:1;display:flex;flex-direction:column;align-items:center;gap:4px;}
.bar{width:100%;border-radius:6px 6px 0 0;min-height:4px;}
.bar-lbl{font-size:10px;color:var(--muted);}
.bar-val{font-size:10px;font-weight:600;}

/* HEATMAP */
.heatmap-box{margin:0 14px 14px;background:var(--surface);border:1px solid var(--border);border-radius:18px;padding:16px;}
.heatmap-box h3{font-size:14px;font-weight:500;margin-bottom:12px;}
.hm-days{display:grid;grid-template-columns:repeat(7,1fr);gap:3px;margin-bottom:4px;}
.hm-days span{text-align:center;font-size:9px;color:var(--muted);}
.hm-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:3px;}
.hm-cell{aspect-ratio:1;border-radius:4px;background:rgba(255,255,255,.05);}
.hm-cell.partial{background:rgba(124,58,237,.25);}
.hm-cell.good{background:rgba(124,58,237,.5);}
.hm-cell.perfect{background:var(--accent);}
.hm-legend{display:flex;gap:12px;margin-top:10px;}
.hm-legend span{display:flex;align-items:center;gap:4px;font-size:11px;color:var(--muted);}
.hm-legend i{width:12px;height:12px;border-radius:3px;display:inline-block;}

/* GESTIONAR */
.hab-item{margin:0 14px 8px;background:var(--surface);border:1px solid var(--border);border-radius:18px;padding:14px 16px;display:flex;align-items:center;gap:12px;}
.hli-icon{width:42px;height:42px;border-radius:12px;display:flex;align-items:center;justify-content:center;font-size:22px;flex-shrink:0;}
.hli-info{flex:1;min-width:0;}
.hli-name{font-weight:500;font-size:15px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.hli-streak{font-size:12px;color:var(--gold);margin-top:2px;}
.hli-btns{display:flex;gap:6px;}
.ico-btn{width:36px;height:36px;border-radius:10px;border:1px solid var(--border);background:transparent;cursor:pointer;font-size:16px;display:flex;align-items:center;justify-content:center;}
.ico-btn.del{border-color:rgba(239,68,68,.3);background:rgba(239,68,68,.1);}
.add-btn{
  margin:4px 14px 16px;width:calc(100% - 28px);
  background:var(--accent);border:none;color:#fff;
  border-radius:18px;padding:15px;
  font-family:inherit;font-size:15px;font-weight:500;
  cursor:pointer;display:flex;align-items:center;justify-content:center;gap:8px;
}
.add-btn:active{opacity:.85;}

/* LOGROS */
.badge-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px;padding:0 14px 14px;}
.badge-card{background:var(--surface);border:1px solid var(--border);border-radius:18px;padding:16px;text-align:center;transition:opacity .3s;}
.badge-card.locked{opacity:.38;filter:grayscale(.8);}
.badge-card:not(.locked){border-color:rgba(124,58,237,.3);}
.badge-ico{font-size:38px;margin-bottom:10px;}
.badge-name{font-size:13px;font-weight:500;margin-bottom:4px;}
.badge-desc{font-size:11px;color:var(--muted);line-height:1.5;}
.badge-ok{font-size:11px;color:var(--accent2);margin-top:8px;font-weight:500;}

/* MODAL */
.modal-overlay{
  display:none;position:fixed;inset:0;background:rgba(0,0,0,.75);
  z-index:300;align-items:flex-end;justify-content:center;
}
.modal-overlay.open{display:flex;}
.modal-box{
  background:var(--bg2);border-radius:24px 24px 0 0;
  width:100%;max-width:480px;padding:24px 20px;
  padding-bottom:max(40px,env(safe-area-inset-bottom,40px));
  border-top:1px solid var(--border);
  max-height:90vh;overflow-y:auto;
}
.modal-box h2{font-size:20px;font-weight:700;margin-bottom:20px;}
.form-lbl{display:block;font-size:13px;color:var(--muted);margin-bottom:6px;}
.form-input{
  width:100%;background:var(--surface);border:1px solid var(--border);
  color:var(--text);border-radius:12px;padding:13px 14px;
  font-family:inherit;font-size:16px;outline:none;
  -webkit-appearance:none;
}
.form-input:focus{border-color:var(--accent);}
.emoji-grid{display:grid;grid-template-columns:repeat(6,1fr);gap:6px;margin-bottom:16px;}
.emoji-opt{aspect-ratio:1;border-radius:10px;background:var(--surface);border:2px solid transparent;display:flex;align-items:center;justify-content:center;font-size:24px;cursor:pointer;}
.emoji-opt.sel{border-color:var(--accent);background:rgba(124,58,237,.15);}
.color-grid{display:grid;grid-template-columns:repeat(6,1fr);gap:6px;margin-bottom:20px;}
.color-opt{aspect-ratio:1;border-radius:10px;cursor:pointer;border:3px solid transparent;transition:transform .15s;}
.color-opt.sel{border-color:#fff;transform:scale(1.1);}
.modal-btns{display:flex;gap:10px;}
.btn-sec{flex:1;background:var(--surface);border:1px solid var(--border);color:var(--text);border-radius:12px;padding:14px;font-family:inherit;font-size:15px;cursor:pointer;}
.btn-pri{flex:2;background:var(--accent);border:none;color:#fff;border-radius:12px;padding:14px;font-family:inherit;font-size:15px;font-weight:500;cursor:pointer;}

/* TOAST */
.toast{
  position:fixed;bottom:80px;left:50%;transform:translateX(-50%) translateY(10px);
  background:var(--surface);border:1px solid rgba(255,255,255,.12);
  border-radius:14px;padding:12px 20px;font-size:14px;
  white-space:nowrap;opacity:0;transition:all .25s;z-index:500;
  pointer-events:none;max-width:calc(100% - 40px);text-align:center;
}
.toast.show{opacity:1;transform:translateX(-50%) translateY(0);}

/* CONFETI */
.conf-particle{position:fixed;top:-10px;width:8px;height:8px;border-radius:2px;z-index:999;pointer-events:none;animation:cffall 2s ease-in forwards;}
@keyframes cffall{to{transform:translateY(110vh) rotate(720deg);opacity:0;}}

::-webkit-scrollbar{width:0;}
</style>
</head>
<body>
<div id="app">

  <!-- HOY -->
  <div class="screen active" id="s-hoy">
    <div class="topbar">
      <h1 id="saludo"></h1>
      <p id="fecha"></p>
    </div>
    <div class="ring-area">
      <div class="ring-wrap">
        <svg width="110" height="110" viewBox="0 0 110 110">
          <defs>
            <linearGradient id="rg" x1="0%" y1="0%" x2="100%" y2="0%">
              <stop offset="0%" stop-color="#7c3aed"/>
              <stop offset="100%" stop-color="#a855f7"/>
            </linearGradient>
          </defs>
          <circle cx="55" cy="55" r="46" fill="none" stroke="#1f1f35" stroke-width="9"/>
          <circle id="ring" cx="55" cy="55" r="46" fill="none" stroke="url(#rg)"
            stroke-width="9" stroke-linecap="round"
            stroke-dasharray="289" stroke-dashoffset="289"
            style="transition:stroke-dashoffset .6s ease"/>
        </svg>
        <div class="ring-label">
          <div class="ring-big" id="ring-pct">0%</div>
          <div class="ring-sm">hoy</div>
        </div>
      </div>
      <div class="stats-col">
        <div class="stat-pill">
          <span class="ico2">🔥</span>
          <div><div class="sv" id="racha-v">0</div><div class="sl">días de racha</div></div>
        </div>
        <div class="stat-pill">
          <span class="ico2">✅</span>
          <div><div class="sv" id="comp-v">0/0</div><div class="sl">completados</div></div>
        </div>
      </div>
    </div>
    <p class="sec-title">Hábitos de hoy</p>
    <div id="lista-hoy"></div>
    <div class="frase-box">
      <p class="frase-q" id="frase-q"></p>
      <p class="frase-a" id="frase-a"></p>
    </div>
  </div>

  <!-- STATS -->
  <div class="screen" id="s-stats">
    <div class="topbar"><h1>Estadísticas 📊</h1><p>Tu progreso reciente</p></div>
    <div class="stats-grid">
      <div class="stat-card"><div class="lbl">Racha máxima</div><div class="val" id="st-max">0</div><div class="sub">días</div></div>
      <div class="stat-card"><div class="lbl">Esta semana</div><div class="val" id="st-sem">0%</div><div class="sub">completado</div></div>
      <div class="stat-card"><div class="lbl">Días perfectos</div><div class="val" id="st-perf">0</div><div class="sub">100% del día</div></div>
      <div class="stat-card"><div class="lbl">Total hábitos</div><div class="val" id="st-tot">0</div><div class="sub">completados</div></div>
    </div>
    <div class="chart-box"><h3>Últimos 7 días</h3><div class="bar-chart" id="barras"></div></div>
    <div class="heatmap-box">
      <h3>Mes actual</h3>
      <div class="hm-days"><span>L</span><span>M</span><span>X</span><span>J</span><span>V</span><span>S</span><span>D</span></div>
      <div class="hm-grid" id="heatmap"></div>
      <div class="hm-legend">
        <span><i style="background:rgba(255,255,255,.05)"></i>Sin datos</span>
        <span><i style="background:rgba(124,58,237,.25)"></i>Parcial</span>
        <span><i style="background:#7c3aed"></i>Perfecto</span>
      </div>
    </div>
  </div>

  <!-- HÁBITOS -->
  <div class="screen" id="s-habitos">
    <div class="topbar"><h1>Mis hábitos ✏️</h1><p>Edita y organiza tu lista</p></div>
    <div id="lista-hab"></div>
    <button class="add-btn" id="btn-add">＋ Añadir hábito</button>
  </div>

  <!-- LOGROS -->
  <div class="screen" id="s-logros">
    <div class="topbar"><h1>Logros 🏆</h1><p>Medallas desbloqueadas</p></div>
    <div class="badge-grid" id="badges"></div>
  </div>

  <!-- NAV -->
  <nav>
    <button class="nav-btn active" id="nb-hoy" onclick="ir('hoy')">
      <span class="ico">🏠</span>Hoy
    </button>
    <button class="nav-btn" id="nb-stats" onclick="ir('stats')">
      <span class="ico">📊</span>Stats
    </button>
    <button class="nav-btn" id="nb-habitos" onclick="ir('habitos')">
      <span class="ico">📋</span>Hábitos
    </button>
    <button class="nav-btn" id="nb-logros" onclick="ir('logros')">
      <span class="ico">🏆</span>Logros
    </button>
  </nav>
</div>

<!-- MODAL -->
<div class="modal-overlay" id="modal">
  <div class="modal-box">
    <h2 id="modal-title">Nuevo hábito</h2>
    <label class="form-lbl">Nombre del hábito</label>
    <input class="form-input" id="h-name" placeholder="Ej: Leer 20 minutos" maxlength="40" style="margin-bottom:16px">
    <label class="form-lbl">Emoji</label>
    <div class="emoji-grid" id="emoji-grid"></div>
    <label class="form-lbl">Color</label>
    <div class="color-grid" id="color-grid"></div>
    <div class="modal-btns">
      <button class="btn-sec" onclick="cerrarModal()">Cancelar</button>
      <button class="btn-pri" onclick="guardarHabito()">Guardar</button>
    </div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
// ── DATOS ──────────────────────────────────────────
const FRASES=[
  {q:"No cuentes los días, haz que los días cuenten.",a:"Muhammad Ali"},
  {q:"El éxito es la suma de pequeños esfuerzos repetidos.",a:"Robert Collier"},
  {q:"Los hábitos son el interés compuesto de la superación personal.",a:"James Clear"},
  {q:"La disciplina es elegir entre lo que quieres ahora y lo que quieres más.",a:"Abraham Lincoln"},
  {q:"Primero formas tus hábitos, luego tus hábitos te forman.",a:"John Dryden"},
  {q:"Cada día es una nueva oportunidad de mejorar.",a:"Anónimo"},
];
const EMOJIS=['💧','📚','🏃','🧘','📵','💪','🥗','🎨','🎸','🌿','😴','✍️','🚴','🧠','🌞','🎯','🏊','🍎','📝','🎵'];
const COLORES=['#3b82f6','#10b981','#f97316','#7c3aed','#ef4444','#f59e0b','#ec4899','#14b8a6','#84cc16','#6366f1','#f43f5e','#8b5cf6'];
const HABITOS_DEF=[
  {id:1,nombre:'Beber 2L de agua',emoji:'💧',color:'#3b82f6'},
  {id:2,nombre:'Leer 20 minutos',emoji:'📚',color:'#10b981'},
  {id:3,nombre:'Hacer ejercicio',emoji:'🏃',color:'#f97316'},
  {id:4,nombre:'Meditar 10 min',emoji:'🧘',color:'#7c3aed'},
  {id:5,nombre:'Sin redes tras las 22:00',emoji:'📵',color:'#ef4444'},
];
const LOGROS=[
  {id:'l1',ico:'🌟',name:'Primer paso',desc:'Completa tu primer hábito',fn:d=>d.tot>=1},
  {id:'l2',ico:'🔥',name:'En racha',desc:'7 días de racha',fn:d=>d.racha>=7},
  {id:'l3',ico:'💎',name:'Diamante',desc:'30 días de racha',fn:d=>d.racha>=30},
  {id:'l4',ico:'⭐',name:'Día perfecto',desc:'Todos los hábitos en un día',fn:d=>d.perf>=1},
  {id:'l5',ico:'🏆',name:'Semana perfecta',desc:'7 días perfectos en total',fn:d=>d.perf>=7},
  {id:'l6',ico:'🎯',name:'Disciplinado',desc:'100 hábitos completados',fn:d=>d.tot>=100},
  {id:'l7',ico:'🚀',name:'Imparable',desc:'14 días de racha',fn:d=>d.racha>=14},
  {id:'l8',ico:'🌈',name:'Creador',desc:'Añade 3 hábitos propios',fn:d=>d.propios>=3},
];

// ── ESTADO ─────────────────────────────────────────
function leer(k,def){try{const v=localStorage.getItem(k);return v!=null?JSON.parse(v):def;}catch{return def;}}
function salvar(k,v){try{localStorage.setItem(k,JSON.stringify(v));}catch{}}

let habitos  = leer('h2',HABITOS_DEF);
let hist     = leer('ht2',{});
let racha    = leer('rc2',{actual:0,max:0,ultimo:null});
let unlock   = leer('ul2',[]);
let editId   = null;
let emojiSel = EMOJIS[0];
let colorSel = COLORES[0];

function hoyStr(){
  const d=new Date();
  return d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0')+'-'+String(d.getDate()).padStart(2,'0');
}

function initHoy(){
  const d=hoyStr();
  if(!hist[d]){
    hist[d]={};
    habitos.forEach(h=>{hist[d][h.id]=false;});
    salvar('ht2',hist);
    const ayer=new Date(); ayer.setDate(ayer.getDate()-1);
    const ayerS=ayer.getFullYear()+'-'+String(ayer.getMonth()+1).padStart(2,'0')+'-'+String(ayer.getDate()).padStart(2,'0');
    if(racha.ultimo && racha.ultimo!==ayerS && racha.ultimo!==d){
      racha.actual=0; salvar('rc2',racha);
    }
  }
}

// ── NAVEGACIÓN ─────────────────────────────────────
function ir(pantalla){
  ['hoy','stats','habitos','logros'].forEach(p=>{
    document.getElementById('s-'+p).classList.remove('active');
    document.getElementById('nb-'+p).classList.remove('active');
  });
  document.getElementById('s-'+pantalla).classList.add('active');
  document.getElementById('nb-'+pantalla).classList.add('active');
  if(pantalla==='hoy')     renderHoy();
  if(pantalla==='stats')   renderStats();
  if(pantalla==='habitos') renderHabitos();
  if(pantalla==='logros')  renderLogros();
}

// ── HOY ────────────────────────────────────────────
function renderHoy(){
  initHoy();
  const d=hoyStr();
  const datos=hist[d]||{};
  const total=habitos.length;
  const hechos=habitos.filter(h=>datos[h.id]).length;
  const pct=total?Math.round(hechos/total*100):0;

  const hora=new Date().getHours();
  document.getElementById('saludo').textContent=
    hora<12?'Buenos días 👋':hora<19?'Buenas tardes ☀️':'Buenas noches 🌙';
  document.getElementById('fecha').textContent=
    new Date().toLocaleDateString('es-ES',{weekday:'long',day:'numeric',month:'long'});

  // Anillo
  const circ=2*Math.PI*46;
  document.getElementById('ring').style.strokeDashoffset=circ*(1-pct/100);
  document.getElementById('ring-pct').textContent=pct+'%';
  document.getElementById('racha-v').textContent=racha.actual;
  document.getElementById('comp-v').textContent=hechos+'/'+total;

  // Lista
  const lista=document.getElementById('lista-hoy');
  lista.innerHTML='';
  habitos.forEach(h=>{
    const done=!!datos[h.id];
    const card=document.createElement('div');
    card.className='habit-card'+(done?' done':'');
    card.innerHTML=
      (done?'<div class="habit-done-bg"></div>':'')+
      '<div class="habit-icon" style="background:'+h.color+'22">'+h.emoji+'</div>'+
      '<div class="habit-info">'+
        '<div class="habit-name">'+h.nombre+'</div>'+
        '<div class="habit-sub">'+(done?'✓ Completado hoy':'Pendiente')+'</div>'+
        '<div class="prog"><div class="prog-fill" style="width:'+(done?100:0)+'%;background:'+h.color+'"></div></div>'+
      '</div>'+
      '<div class="check">'+(done?'✓':'')+'</div>';
    card.addEventListener('click',()=>toggleH(h.id));
    lista.appendChild(card);
  });

  const fi=FRASES[new Date().getDate()%FRASES.length];
  document.getElementById('frase-q').textContent='"'+fi.q+'"';
  document.getElementById('frase-a').textContent='— '+fi.a;
}

function toggleH(id){
  const d=hoyStr();
  if(!hist[d]) hist[d]={};
  hist[d][id]=!hist[d][id];
  salvar('ht2',hist);

  const total=habitos.length;
  const hechos=habitos.filter(h=>hist[d][h.id]).length;

  if(hechos>0){
    const ayer=new Date(); ayer.setDate(ayer.getDate()-1);
    const ayerS=ayer.getFullYear()+'-'+String(ayer.getMonth()+1).padStart(2,'0')+'-'+String(ayer.getDate()).padStart(2,'0');
    if(racha.ultimo===ayerS||racha.ultimo===null){racha.actual++;}
    else if(racha.ultimo!==d){racha.actual=1;}
    racha.ultimo=d;
    if(racha.actual>racha.max) racha.max=racha.actual;
    salvar('rc2',racha);
  }

  if(hechos===total&&total>0){
    confeti();
    toast('🎉 ¡Día perfecto! ¡Todos completados!');
  }

  verificarLogros();
  renderHoy();
}

// ── STATS ──────────────────────────────────────────
function renderStats(){
  let tot=0,perf=0;
  Object.keys(hist).forEach(dia=>{
    const h=habitos.filter(x=>hist[dia]&&hist[dia][x.id]).length;
    tot+=h; if(habitos.length>0&&h===habitos.length) perf++;
  });
  let sc=0,st=0;
  for(let i=0;i<7;i++){
    const dd=new Date(); dd.setDate(dd.getDate()-i);
    const ds=dd.getFullYear()+'-'+String(dd.getMonth()+1).padStart(2,'0')+'-'+String(dd.getDate()).padStart(2,'0');
    if(hist[ds]){sc+=habitos.filter(x=>hist[ds][x.id]).length;st+=habitos.length;}
  }
  document.getElementById('st-max').textContent=racha.max;
  document.getElementById('st-sem').textContent=st?Math.round(sc/st*100)+'%':'0%';
  document.getElementById('st-perf').textContent=perf;
  document.getElementById('st-tot').textContent=tot;

  // Barras
  const dias=['L','M','X','J','V','S','D'];
  const datos7=[];
  for(let i=6;i>=0;i--){
    const dd=new Date(); dd.setDate(dd.getDate()-i);
    const ds=dd.getFullYear()+'-'+String(dd.getMonth()+1).padStart(2,'0')+'-'+String(dd.getDate()).padStart(2,'0');
    let p=0;
    if(hist[ds]&&habitos.length>0){
      p=Math.round(habitos.filter(x=>hist[ds][x.id]).length/habitos.length*100);
    }
    datos7.push({p,lbl:dias[dd.getDay()===0?6:dd.getDay()-1],hoy:i===0});
  }
  const maxB=Math.max(...datos7.map(v=>v.p),1);
  const barras=document.getElementById('barras');
  barras.innerHTML='';
  datos7.forEach(v=>{
    const h=Math.max(Math.round(v.p/maxB*95),4);
    const col=document.createElement('div');
    col.className='bar-col';
    col.innerHTML=
      '<span class="bar-val" style="color:'+(v.p===100?'#a855f7':'#8b8aa8')+'">'+v.p+'%</span>'+
      '<div class="bar" style="height:'+h+'px;background:'+(v.hoy?'#7c3aed':v.p===100?'#a855f7':'#1f1f35')+';border:1px solid rgba(255,255,255,.07)"></div>'+
      '<span class="bar-lbl" style="font-weight:'+(v.hoy?600:400)+'">'+v.lbl+'</span>';
    barras.appendChild(col);
  });

  // Heatmap
  const hm=document.getElementById('heatmap');
  hm.innerHTML='';
  const now=new Date();
  const y=now.getFullYear(),m=now.getMonth();
  const first=new Date(y,m,1).getDay();
  const blancos=first===0?6:first-1;
  const ultimo=new Date(y,m+1,0).getDate();
  for(let i=0;i<blancos;i++){const e=document.createElement('div');e.className='hm-cell';hm.appendChild(e);}
  for(let day=1;day<=ultimo;day++){
    const ds=y+'-'+String(m+1).padStart(2,'0')+'-'+String(day).padStart(2,'0');
    const e=document.createElement('div');e.className='hm-cell';
    if(hist[ds]&&habitos.length>0){
      const p=habitos.filter(x=>hist[ds][x.id]).length/habitos.length;
      if(p===1) e.classList.add('perfect');
      else if(p>=.5) e.classList.add('good');
      else if(p>0) e.classList.add('partial');
    }
    hm.appendChild(e);
  }
}

// ── HÁBITOS ────────────────────────────────────────
function renderHabitos(){
  const lista=document.getElementById('lista-hab');
  lista.innerHTML='';
  habitos.forEach(h=>{
    let streak=0; const dd=new Date();
    for(let i=0;i<365;i++){
      const ds=dd.getFullYear()+'-'+String(dd.getMonth()+1).padStart(2,'0')+'-'+String(dd.getDate()).padStart(2,'0');
      if(hist[ds]&&hist[ds][h.id]) streak++;
      else break;
      dd.setDate(dd.getDate()-1);
    }
    const div=document.createElement('div');
    div.className='hab-item';
    div.innerHTML=
      '<div class="hli-icon" style="background:'+h.color+'22">'+h.emoji+'</div>'+
      '<div class="hli-info">'+
        '<div class="hli-name">'+h.nombre+'</div>'+
        '<div class="hli-streak">🔥 '+streak+' días de racha</div>'+
      '</div>'+
      '<div class="hli-btns">'+
        '<button class="ico-btn" onclick="editarH('+h.id+')">✏️</button>'+
        '<button class="ico-btn del" onclick="borrarH('+h.id+')">🗑️</button>'+
      '</div>';
    lista.appendChild(div);
  });
}

function editarH(id){
  const h=habitos.find(x=>x.id===id);
  if(!h) return;
  editId=id;
  document.getElementById('modal-title').textContent='Editar hábito';
  document.getElementById('h-name').value=h.nombre;
  emojiSel=h.emoji; colorSel=h.color;
  abrirModal();
}

function borrarH(id){
  if(!confirm('¿Eliminar este hábito?')) return;
  habitos=habitos.filter(h=>h.id!==id);
  salvar('h2',habitos);
  Object.keys(hist).forEach(d=>{if(hist[d]) delete hist[d][id];});
  salvar('ht2',hist);
  renderHabitos();
  toast('Hábito eliminado');
}

// ── MODAL ──────────────────────────────────────────
function abrirModal(){
  const eg=document.getElementById('emoji-grid');
  eg.innerHTML='';
  EMOJIS.forEach(e=>{
    const d=document.createElement('div');
    d.className='emoji-opt'+(emojiSel===e?' sel':'');
    d.textContent=e;
    d.onclick=()=>{emojiSel=e;eg.querySelectorAll('.emoji-opt').forEach(x=>x.classList.remove('sel'));d.classList.add('sel');};
    eg.appendChild(d);
  });
  const cg=document.getElementById('color-grid');
  cg.innerHTML='';
  COLORES.forEach(c=>{
    const d=document.createElement('div');
    d.className='color-opt'+(colorSel===c?' sel':'');
    d.style.background=c;
    d.onclick=()=>{colorSel=c;cg.querySelectorAll('.color-opt').forEach(x=>x.classList.remove('sel'));d.classList.add('sel');};
    cg.appendChild(d);
  });
  document.getElementById('modal').classList.add('open');
}

function cerrarModal(){
  document.getElementById('modal').classList.remove('open');
  document.getElementById('h-name').value='';
  editId=null; emojiSel=EMOJIS[0]; colorSel=COLORES[0];
  document.getElementById('modal-title').textContent='Nuevo hábito';
}

function guardarHabito(){
  const nombre=document.getElementById('h-name').value.trim();
  if(!nombre){toast('Escribe un nombre');return;}
  if(editId){
    habitos=habitos.map(h=>h.id===editId?{...h,nombre,emoji:emojiSel,color:colorSel}:h);
    toast('Hábito actualizado ✓');
  } else {
    const nid=Date.now();
    habitos.push({id:nid,nombre,emoji:emojiSel,color:colorSel});
    const d=hoyStr(); if(hist[d]) hist[d][nid]=false;
    salvar('ht2',hist);
    toast('Hábito añadido ✓');
  }
  salvar('h2',habitos);
  cerrarModal();
  renderHabitos();
  verificarLogros();
}

document.getElementById('modal').addEventListener('click',function(e){if(e.target===this)cerrarModal();});
document.getElementById('btn-add').addEventListener('click',function(){editId=null;abrirModal();});

// ── LOGROS ─────────────────────────────────────────
function getDatos(){
  let tot=0,perf=0;
  Object.keys(hist).forEach(dia=>{
    const h=habitos.filter(x=>hist[dia]&&hist[dia][x.id]).length;
    tot+=h; if(habitos.length>0&&h===habitos.length) perf++;
  });
  return {racha:racha.actual,tot,perf,propios:habitos.filter(h=>h.id>5).length};
}

function verificarLogros(){
  const datos=getDatos();
  LOGROS.forEach(l=>{
    if(!unlock.includes(l.id)&&l.fn(datos)){
      unlock.push(l.id); salvar('ul2',unlock);
      toast('🏆 Logro desbloqueado: '+l.name);
    }
  });
}

function renderLogros(){
  const grid=document.getElementById('badges');
  grid.innerHTML='';
  LOGROS.forEach(l=>{
    const ok=unlock.includes(l.id);
    const div=document.createElement('div');
    div.className='badge-card'+(ok?'':' locked');
    div.innerHTML=
      '<div class="badge-ico">'+l.ico+'</div>'+
      '<div class="badge-name">'+l.name+'</div>'+
      '<div class="badge-desc">'+l.desc+'</div>'+
      (ok?'<div class="badge-ok">✓ Conseguido</div>':'');
    grid.appendChild(div);
  });
}

// ── TOAST ──────────────────────────────────────────
let toastTimer;
function toast(msg){
  const t=document.getElementById('toast');
  t.textContent=msg; t.classList.add('show');
  clearTimeout(toastTimer);
  toastTimer=setTimeout(()=>t.classList.remove('show'),2800);
}

// ── CONFETI ────────────────────────────────────────
function confeti(){
  const colores=['#7c3aed','#a855f7','#f59e0b','#10b981','#3b82f6','#f97316','#ef4444'];
  for(let i=0;i<80;i++){
    const p=document.createElement('div');
    p.className='conf-particle';
    p.style.cssText='left:'+Math.random()*100+'%;background:'+colores[Math.floor(Math.random()*colores.length)]+';animation-delay:'+Math.random()*.8+'s;width:'+(Math.random()*8+4)+'px;height:'+(Math.random()*8+4)+'px;';
    document.body.appendChild(p);
    setTimeout(()=>p.remove(),2500);
  }
}

// ── INICIO ─────────────────────────────────────────
initHoy();
renderHoy();
verificarLogros();
</script>
</body>
</html>
