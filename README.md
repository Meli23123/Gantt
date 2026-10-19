<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Gantt · Work Sample KM Analyst CX</title>
<style>
:root{
  --navy:#2D3277; --navy-d:#1B1F3B; --yellow:#FFE600; --yellow-s:#FFF7B8;
  --bg:#F4F5FB; --card:#fff; --line:#E3E6F2; --line2:#EEF0F8; --mut:#5B6178; --mut2:#8A90A8;
  --red:#D6453D; --red-s:#FCE9E7; --green:#1E8E5A; --green-s:#E3F4EB; --amber:#B7791F; --amber-s:#FFF1D6;
  --r:12px; --sh:0 1px 2px rgba(27,31,59,.06),0 4px 14px rgba(27,31,59,.06);
}
*{box-sizing:border-box}
html,body{margin:0}
body{font-family:"Segoe UI",system-ui,-apple-system,Roboto,Arial,sans-serif;background:var(--bg);color:var(--navy-d);font-size:14px;line-height:1.4}
button,input,select,textarea{font:inherit;color:inherit}
button{cursor:pointer}
.app{max-width:1600px;margin:0 auto;padding:18px 20px 40px}

/* header */
.top{display:flex;flex-wrap:wrap;align-items:center;gap:14px 20px;justify-content:space-between;margin-bottom:14px}
.brand{display:flex;align-items:center;gap:12px}
.logo{width:44px;height:44px;border-radius:12px;background:var(--yellow);display:grid;place-items:center;font-weight:800;color:var(--navy);font-size:18px;box-shadow:var(--sh)}
h1{margin:0;font-size:21px;letter-spacing:-.01em}
.sub{color:var(--mut);font-size:12.5px}
.actions{display:flex;flex-wrap:wrap;gap:8px;align-items:center}
.btn{border:1px solid var(--line);background:#fff;border-radius:9px;padding:8px 12px;font-weight:600;font-size:13px;display:inline-flex;align-items:center;gap:6px;transition:.15s}
.btn:hover{border-color:var(--navy);background:#fafaff}
.btn.pri{background:var(--navy);color:#fff;border-color:var(--navy)}
.btn.pri:hover{background:var(--navy-d)}
.btn.yel{background:var(--yellow);border-color:var(--yellow);color:var(--navy-d)}
.btn.sm{padding:5px 9px;font-size:12px}
.btn.dng{color:var(--red);border-color:#f2c4c0}
.btn:focus-visible,.tab:focus-visible,input:focus-visible,select:focus-visible,textarea:focus-visible{outline:2px solid var(--navy);outline-offset:1px}
.saved{font-size:12px;color:var(--mut);display:flex;align-items:center;gap:6px}
.saved i{width:8px;height:8px;border-radius:50%;background:var(--green);display:inline-block}
.saved.err i{background:var(--red)}
.banner{background:var(--red-s);border:1px solid #f2c4c0;color:#8a1f19;border-radius:10px;padding:8px 12px;margin-bottom:12px;font-size:13px;display:none}

/* settings */
.cfg{display:flex;flex-wrap:wrap;gap:10px 18px;align-items:center;background:var(--card);border:1px solid var(--line);border-radius:var(--r);padding:10px 14px;margin-bottom:14px;box-shadow:var(--sh)}
.cfg label{display:flex;align-items:center;gap:8px;font-size:12.5px;color:var(--mut);font-weight:600}
.cfg input[type=date]{border:1px solid var(--line);border-radius:8px;padding:5px 8px;background:#fff}
.cfg .hint{margin-left:auto;font-size:12px;color:var(--mut2)}

/* kpis */
.kpis{display:grid;grid-template-columns:2.1fr repeat(5,1fr);gap:12px;margin-bottom:14px}
.kpi{background:var(--card);border:1px solid var(--line);border-radius:var(--r);padding:12px 14px;box-shadow:var(--sh);text-align:left;display:block;width:100%}
button.kpi:hover{border-color:var(--navy)}
.kpi .l{font-size:11px;font-weight:700;letter-spacing:.05em;text-transform:uppercase;color:var(--mut)}
.kpi .v{font-size:26px;font-weight:800;letter-spacing:-.02em;margin-top:2px}
.kpi .s{font-size:12px;color:var(--mut)}
.kpi.red .v{color:var(--red)} .kpi.green .v{color:var(--green)} .kpi.amber .v{color:var(--amber)}
.kpi.main{background:var(--navy);color:#fff;border-color:var(--navy)}
.kpi.main .l,.kpi.main .s{color:#C9CDF0}
.kpi.main .v{color:var(--yellow)}
.pbar{height:9px;background:rgba(255,255,255,.2);border-radius:99px;overflow:hidden;margin-top:8px}
.pbar b{display:block;height:100%;background:var(--yellow);border-radius:99px;transition:width .3s}
.pbar.lt{background:var(--line2)} .pbar.lt b{background:var(--navy)}

/* toolbar */
.bar{display:flex;flex-wrap:wrap;gap:10px;align-items:center;justify-content:space-between;margin-bottom:10px}
.tabs{display:flex;background:#E7E9F6;border-radius:10px;padding:3px;gap:2px}
.tab{border:0;background:transparent;padding:7px 14px;border-radius:8px;font-weight:700;font-size:13px;color:var(--mut)}
.tab[aria-selected=true]{background:#fff;color:var(--navy);box-shadow:0 1px 3px rgba(0,0,0,.12)}
.filters{display:flex;flex-wrap:wrap;gap:8px;align-items:center}
.filters input[type=search],.filters select{border:1px solid var(--line);border-radius:8px;padding:6px 9px;background:#fff;font-size:13px}
.filters input[type=search]{width:170px}
.chk{display:inline-flex;align-items:center;gap:6px;font-size:13px;color:var(--mut);font-weight:600}
.seg{display:flex;border:1px solid var(--line);border-radius:8px;overflow:hidden;background:#fff}
.seg button{border:0;background:#fff;padding:6px 10px;font-size:12px;font-weight:700;color:var(--mut)}
.seg button[aria-pressed=true]{background:var(--navy);color:#fff}

/* gantt */
.card{background:var(--card);border:1px solid var(--line);border-radius:var(--r);box-shadow:var(--sh)}
.gwrap{overflow:auto;max-height:calc(100vh - 150px);min-height:420px;position:relative;border-radius:var(--r)}
.ginner{position:relative}
.ghead{position:sticky;top:0;z-index:6;display:flex;background:#fff;border-bottom:1px solid var(--line)}
.gh-left{position:sticky;left:0;z-index:7;background:#fff;border-right:1px solid var(--line);display:flex;align-items:flex-end;padding:0 12px 8px;font-size:11px;font-weight:700;color:var(--mut);letter-spacing:.05em;text-transform:uppercase;justify-content:space-between}
.gh-right{position:relative}
.mrow,.drow{display:flex}
.mrow>div{font-size:11px;font-weight:800;color:var(--navy);padding:4px 8px;border-left:1px solid var(--line);background:#F7F8FD;overflow:hidden;white-space:nowrap}
.drow>div{text-align:center;font-size:10.5px;color:var(--mut);border-left:1px solid var(--line2);padding:3px 0;line-height:1.2}
.drow>div b{display:block;font-size:12px;color:var(--navy-d)}
.drow>div.we{background:#F6F6FA;color:var(--mut2)}
.drow>div.td{background:var(--yellow);color:var(--navy-d);font-weight:800}
.gbody{display:flex;position:relative}
.gleft{position:sticky;left:0;z-index:4;background:#fff;border-right:1px solid var(--line)}
.gright{position:relative}
.lrow{display:flex;align-items:center;gap:8px;padding:0 10px;border-bottom:1px solid var(--line2);position:relative}
.lrow.ph{background:#F3F4FB;font-weight:800;border-bottom:1px solid var(--line)}
.lrow.task:hover{background:#FAFAFF}
.lrow .nm{flex:1;min-width:0;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;cursor:pointer;background:none;border:0;text-align:left;padding:0;font-size:13px}
.lrow .nm:hover{text-decoration:underline}
.lrow.done .nm{color:var(--mut2);text-decoration:line-through}
.lrow .pc{font-size:11.5px;font-weight:700;color:var(--mut);min-width:34px;text-align:right}
.dot{width:9px;height:9px;border-radius:50%;flex:none}
.tag{font-size:10px;font-weight:800;border-radius:99px;padding:1px 7px;flex:none;letter-spacing:.02em}
.tag.od{background:var(--red-s);color:var(--red)} .tag.ds{background:var(--amber-s);color:var(--amber)} .tag.bl{background:#EDEEF5;color:var(--mut)}
.cb{width:18px;height:18px;border-radius:5px;border:2px solid #B9BED6;background:#fff;display:grid;place-items:center;flex:none;padding:0}
.cb[aria-checked=true]{background:var(--green);border-color:var(--green)}
.cb[aria-checked=true]::after{content:"";width:5px;height:9px;border:solid #fff;border-width:0 2px 2px 0;transform:rotate(45deg) translate(-1px,-1px)}
.cb:focus-visible{outline:2px solid var(--navy);outline-offset:2px}
.caret{border:0;background:none;padding:0;width:18px;height:18px;display:grid;place-items:center;color:var(--navy);font-size:11px;transition:transform .15s;flex:none}
.caret.c{transform:rotate(-90deg)}
.rl{position:absolute;left:0;right:0;border-bottom:1px solid var(--line2);pointer-events:none}
.rl.ph{background:#F8F9FD}
.we-col{position:absolute;top:0;bottom:0;background:rgba(91,97,120,.05);pointer-events:none}
.tl{position:absolute;top:0;bottom:0;width:2px;background:var(--navy);z-index:2;pointer-events:none}
.tl::before{content:"HOY";position:absolute;top:0;left:-14px;background:var(--navy);color:#fff;font-size:9px;font-weight:800;padding:1px 5px;border-radius:0 0 5px 5px;margin-left:0}
.dl{position:absolute;top:0;bottom:0;width:0;border-left:2px dashed var(--red);z-index:2;pointer-events:none}
.dl::before{content:"ENTREGA";position:absolute;top:0;left:3px;background:var(--red);color:#fff;font-size:9px;font-weight:800;padding:1px 5px;border-radius:0 0 5px 5px}
.bar-t{position:absolute;height:24px;border-radius:7px;z-index:3;display:flex;align-items:center;cursor:grab;touch-action:none;user-select:none;overflow:hidden;border:1.5px solid}
.bar-t:active{cursor:grabbing}
.bar-t .fill{position:absolute;left:0;top:0;bottom:0;opacity:.95}
.bar-t .lb{position:relative;z-index:1;font-size:11px;font-weight:800;padding:0 8px;white-space:nowrap;color:#fff;text-shadow:0 1px 1px rgba(0,0,0,.25)}
.bar-t .h{position:absolute;top:0;bottom:0;width:8px;cursor:ew-resize;z-index:2}
.bar-t .h.l{left:0}.bar-t .h.r{right:0}
.bar-t.od{box-shadow:0 0 0 2px var(--red)}
.bar-t.bl{background-image:repeating-linear-gradient(45deg,rgba(255,255,255,.35) 0 6px,transparent 6px 12px)!important}
.bar-t.rev{border-style:dashed}
.bar-t.done{opacity:.72}
.ms{position:absolute;width:20px;height:20px;transform:rotate(45deg);border-radius:4px;z-index:3;cursor:grab;border:2px solid;touch-action:none}
.ms.od{box-shadow:0 0 0 2px var(--red)}
.ms.done::after{content:"";position:absolute;left:5px;top:1px;width:4px;height:8px;border:solid #fff;border-width:0 2px 2px 0;transform:rotate(0deg)}
.phbar{position:absolute;height:10px;border-radius:3px;z-index:2;opacity:.9}
.phbar::before,.phbar::after{content:"";position:absolute;top:8px;border:4px solid transparent}
.phbar::before{left:0;border-left-color:inherit}
.deps{position:absolute;left:0;top:0;pointer-events:none;z-index:2;overflow:visible}
.legend{display:flex;flex-wrap:wrap;gap:6px 16px;padding:9px 12px;border-top:1px solid var(--line);font-size:12px;color:var(--mut)}
.legend span{display:inline-flex;align-items:center;gap:6px}
.legend i{display:inline-block;width:16px;height:10px;border-radius:3px}

/* list */
.tbl{width:100%;border-collapse:separate;border-spacing:0;font-size:13px}
.tbl th{position:sticky;top:0;background:#F7F8FD;text-align:left;font-size:11px;letter-spacing:.05em;text-transform:uppercase;color:var(--mut);padding:9px 8px;border-bottom:1px solid var(--line);z-index:2;white-space:nowrap}
.tbl td{padding:6px 8px;border-bottom:1px solid var(--line2);vertical-align:middle}
.tbl tr.phr td{background:#F3F4FB;font-weight:800;padding:8px}
.tbl tr.done td.nmc{color:var(--mut2);text-decoration:line-through}
.tbl input[type=date],.tbl select,.tbl input[type=number]{border:1px solid transparent;background:transparent;border-radius:7px;padding:4px 5px;width:100%;font-size:13px}
.tbl input:hover,.tbl select:hover{border-color:var(--line);background:#fff}
.tbl input[type=number]{width:62px}
.tbl td select{min-width:112px}
.tbl .pcw{display:flex;align-items:center;gap:6px;min-width:130px}
.tbl .pcw input[type=range]{width:80px;accent-color:var(--navy)}
.badge{display:inline-flex;align-items:center;gap:6px;border-radius:99px;padding:2px 9px;font-size:11.5px;font-weight:700;white-space:nowrap}
.tscroll{overflow:auto;max-height:calc(100vh - 150px);border-radius:var(--r)}

/* panel */
.pgrid{display:grid;grid-template-columns:repeat(auto-fit,minmax(310px,1fr));gap:12px}
.pcard{padding:14px}
.pcard h3{margin:0 0 8px;font-size:13px;letter-spacing:.04em;text-transform:uppercase;display:flex;align-items:center;gap:8px;justify-content:space-between}
.pcard h3 em{font-style:normal;background:var(--line2);border-radius:99px;padding:1px 9px;font-size:12px}
.pcard.red h3{color:var(--red)} .pcard.amber h3{color:var(--amber)}
.item .tx{flex:1;min-width:0;display:flex;flex-direction:column;gap:1px}
.item{display:flex;align-items:flex-start;gap:9px;padding:7px 0;border-top:1px solid var(--line2)}
.item:first-of-type{border-top:0}
.item .nm{background:none;border:0;text-align:left;padding:0;cursor:pointer;font-size:13px}
.item .nm:hover{text-decoration:underline}
.item small{color:var(--mut);font-size:11.5px;white-space:nowrap}
.empty{color:var(--mut2);font-size:13px;padding:6px 0}
.ph-row{display:grid;grid-template-columns:150px 1fr 70px;align-items:center;gap:10px;padding:6px 0;font-size:13px}

/* modal */
.ov{position:fixed;inset:0;background:rgba(27,31,59,.45);display:none;align-items:flex-start;justify-content:center;padding:4vh 14px;z-index:50;overflow:auto}
.ov.on{display:flex}
.modal{background:#fff;border-radius:16px;width:min(680px,100%);box-shadow:0 20px 60px rgba(0,0,0,.3);overflow:hidden}
.mh{padding:14px 18px;background:var(--navy);color:#fff;display:flex;justify-content:space-between;align-items:center}
.mh h2{margin:0;font-size:16px}
.mh button{background:none;border:0;color:#fff;font-size:22px;line-height:1}
.mb{padding:16px 18px;display:grid;grid-template-columns:1fr 1fr;gap:12px 14px}
.mb .f{display:flex;flex-direction:column;gap:4px}
.mb .f.w{grid-column:1/-1}
.mb label{font-size:11.5px;font-weight:700;color:var(--mut);text-transform:uppercase;letter-spacing:.04em}
.mb input,.mb select,.mb textarea{border:1px solid var(--line);border-radius:8px;padding:8px 10px;background:#fff;width:100%}
.mb textarea{min-height:64px;resize:vertical}
.mb .rg{display:flex;align-items:center;gap:10px}
.mb .rg input[type=range]{accent-color:var(--navy);padding:0}
.mb .rg output{font-weight:800;min-width:42px}
.dpl{max-height:150px;overflow:auto;border:1px solid var(--line);border-radius:8px;padding:6px 8px}
.dpl .g{font-size:11px;font-weight:800;color:var(--mut);margin:6px 0 2px;text-transform:uppercase}
.dpl label{display:flex;gap:8px;align-items:center;font-size:13px;text-transform:none;letter-spacing:0;font-weight:500;color:var(--navy-d);padding:2px 0}
.dpl label input{width:auto}
.mf{display:flex;gap:8px;justify-content:space-between;padding:12px 18px;border-top:1px solid var(--line);background:#FAFAFE}
.warn{grid-column:1/-1;background:var(--amber-s);border:1px solid #f1d49b;color:#7a5410;border-radius:8px;padding:8px 10px;font-size:12.5px;display:none}
.toast{position:fixed;left:50%;bottom:22px;transform:translateX(-50%) translateY(20px);background:var(--navy-d);color:#fff;padding:10px 16px;border-radius:10px;font-weight:600;font-size:13px;opacity:0;transition:.25s;z-index:80;pointer-events:none;max-width:90vw}
.toast.on{opacity:1;transform:translateX(-50%)}

@media (max-width:1100px){.kpis{grid-template-columns:repeat(3,1fr)}.kpi.main{grid-column:1/-1}}
@media (max-width:640px){.app{padding:12px}.kpis{grid-template-columns:1fr 1fr}.mb{grid-template-columns:1fr}}
@media print{
  body{background:#fff}.actions,.bar,.cfg,.legend,.toast,.banner{display:none!important}
  .gwrap,.tscroll{max-height:none;overflow:visible}.card,.kpi{box-shadow:none}
  @page{size:A3 landscape;margin:10mm}
}
</style>
</head>
<body>
<div class="app">
  <header class="top">
    <div class="brand">
      <div class="logo">KM</div>
      <div>
        <h1>Work Sample · Knowledge Management Analyst, CX</h1>
        <div class="sub">Plan y seguimiento hasta la entrega final · Mercado Libre</div>
      </div>
    </div>
    <div class="actions">
      <span class="saved" id="saved" role="status"><i></i><span>Guardado</span></span>
      <button class="btn yel" id="bAddT">＋ Actividad</button>
      <button class="btn" id="bAddP">＋ Fase</button>
      <button class="btn" id="bAdj" title="Mueve hacia adelante las actividades que empiezan antes de que termine su predecesora">⇄ Ajustar dependencias</button>
      <button class="btn" id="bExp">⭳ Exportar</button>
      <button class="btn" id="bImp">⭱ Importar</button>
      <button class="btn" id="bPrint">⎙ Imprimir</button>
      <button class="btn dng" id="bReset">↺ Restablecer</button>
      <input type="file" id="fImp" accept="application/json,.json" hidden>
    </div>
  </header>
  <div class="banner" id="banner">No se pudo guardar en este navegador (modo privado o almacenamiento bloqueado). Usa <b>Exportar</b> con frecuencia para no perder tus cambios.</div>

  <section class="cfg" aria-label="Fechas del proyecto">
    <label>Inicio del proyecto <input type="date" id="cStart"></label>
    <label>Entrega final <input type="date" id="cDue"></label>
    <span class="hint">La fecha de entrega es provisional: ajústala a la fecha real indicada por Mercado Libre. Los cambios se guardan solos.</span>
  </section>

  <section class="kpis" id="kpis" aria-label="Indicadores"></section>

  <div class="bar">
    <div class="tabs" role="tablist" id="tabs">
      <button class="tab" role="tab" data-v="gantt">Cronograma</button>
      <button class="tab" role="tab" data-v="list">Lista editable</button>
      <button class="tab" role="tab" data-v="panel">Qué sigue</button>
    </div>
    <div class="filters" id="filters">
      <input type="search" id="fQ" placeholder="Buscar actividad…" aria-label="Buscar">
      <select id="fPh" aria-label="Fase"></select>
      <select id="fSt" aria-label="Estado"></select>
      <select id="fPr" aria-label="Prioridad"></select>
      <label class="chk"><input type="checkbox" id="fOd"> Solo atrasadas</label>
      <span id="ganttCtl" style="display:flex;gap:8px;align-items:center">
        <div class="seg" role="group" aria-label="Zoom"><button data-z="56">Amplio</button><button data-z="34">Día</button><button data-z="20">Compacto</button></div>
        <button class="btn sm" id="bToday">Ir a hoy</button>
        <button class="btn sm" id="bFold">Plegar fases</button>
        <label class="chk"><input type="checkbox" id="fDep"> Dependencias</label>
        <label class="chk" title="Al mover una actividad, empuja las que dependen de ella"><input type="checkbox" id="fCas"> Arrastre empuja sucesoras</label>
      </span>
    </div>
  </div>

  <main id="view"></main>
</div>

<div class="ov" id="ov" aria-hidden="true"><div class="modal" role="dialog" aria-modal="true" aria-labelledby="mt" id="modal"></div></div>
<div class="toast" id="toast" role="status"></div>

<script>
"use strict";
/* ============ utilidades de fecha (días enteros, sin zona horaria) ============ */
const DAY=864e5, KEY="ws-km-gantt-v1";
const d2n=s=>{const p=s.split("-").map(Number);return Math.round(Date.UTC(p[0],p[1]-1,p[2])/DAY)};
const n2d=n=>{const t=new Date(n*DAY);return t.getUTCFullYear()+"-"+String(t.getUTCMonth()+1).padStart(2,"0")+"-"+String(t.getUTCDate()).padStart(2,"0")};
const todayN=()=>{const t=new Date();return Math.round(Date.UTC(t.getFullYear(),t.getMonth(),t.getDate())/DAY)};
const fmt=(n,o)=>new Date(n*DAY).toLocaleDateString("es-CO",Object.assign({weekday:"short",day:"numeric",month:"short",timeZone:"UTC"},o||{}));
const isWE=n=>{const w=new Date(n*DAY).getUTCDay();return w===0||w===6};

/* ============ metadatos ============ */
const ST={pendiente:{l:"Pendiente",c:"#6B7280",bg:"#EDEEF5"},en_curso:{l:"En curso",c:"#2D3277",bg:"#E4E6F8"},revision:{l:"En revisión",c:"#B7791F",bg:"#FFF1D6"},completada:{l:"Completada",c:"#1E8E5A",bg:"#E3F4EB"},bloqueada:{l:"Bloqueada",c:"#D6453D",bg:"#FCE9E7"}};
const PR={alta:{l:"Alta",c:"#D6453D",o:0},media:{l:"Media",c:"#E0A100",o:1},baja:{l:"Baja",c:"#8A90A8",o:2}};
const TY={task:"Actividad",review:"Revisión",milestone:"Hito"};

/* ============ datos iniciales (derivados del PDF del work sample) ============ */
function seed(){
  const P=[
    ["p0","0 · Preparación","#6B7280"],
    ["p1","1 · Material de entrenamiento","#3F51B5"],
    ["p2","2 · Análisis de CSAT","#0E8F6E"],
    ["p3","3 · Plan de acción","#D9822B"],
    ["p4","4 · Uso de IA","#8E44AD"],
    ["p5","5 · Revisiones","#C2410C"],
    ["p6","6 · Formulario y entrega final","#1B1F3B"]
  ];
  // id, fase, tipo, nombre, inicio, fin, prioridad, estado, %, deps, notas
  const T=[
   ["t1","p0","task","Leer instrucciones y criterios de evaluación","2026-10-14","2026-10-14","alta","completada",100,[],"Se valora: claridad del razonamiento, priorización, criterio metodológico, límites de los datos y comunicación visual."],
   ["t2","p0","task","Reunir insumos: lección en Grid, base de CSAT de septiembre","2026-10-14","2026-10-15","alta","completada",100,["t1"],""],
   ["t3","p0","task","Definir la estructura de la presentación (4 partes identificadas)","2026-10-15","2026-10-15","media","completada",100,["t1"],"Una sola presentación en Google Slides, con las cuatro partes incluidas e identificadas."],

   ["t4","p1","task","Revisar la lección de Viaje del Paquete en Grid","2026-10-15","2026-10-15","alta","completada",100,["t2"],""],
   ["t5","p1","task","Listar los problemas metodológicos con ejemplos del material","2026-10-15","2026-10-16","alta","completada",100,["t4"],"Pide: «lista todos los que encuentres». Cada justificación con ejemplos concretos."],
   ["t6","p1","task","Definir ajustes: estructura, secuencia, explicaciones, práctica y comprobación","2026-10-16","2026-10-16","alta","completada",100,["t5"],""],
   ["t7","p1","task","Identificar qué falta para garantizar el aprendizaje y justificar","2026-10-16","2026-10-16","media","completada",100,["t5"],""],
   ["t8","p1","task","Dar la recomendación: aprobar, pedir ajustes o no publicar todavía","2026-10-16","2026-10-16","alta","completada",100,["t6","t7"],"Recomendación actual: ajustes mayores, no publicar todavía."],
   ["t9","p1","task","Diapositiva: estructura actual vs. estructura propuesta","2026-10-16","2026-10-17","alta","completada",100,["t6"],""],
   ["t10","p1","task","Corregir la lección propuesta (HTML / Grid) según la estructura de la Situación 1","2026-10-18","2026-10-20","alta","en_curso",60,["t6"],"El último HTML adjunto era una plantilla vacía de Grid: re-exportar la lección desde Grid. Hay versión corregida (Entrenamiento_v2.html)."],
   ["t11","p1","task","Pulir el diseño de las diapositivas de la Parte 1","2026-10-17","2026-10-19","media","en_curso",80,["t8","t9"],""],

   ["t12","p2","task","Revisar la base: 28 filas y procesos con nombre repetido","2026-10-15","2026-10-15","alta","completada",100,["t2"],"Post Compra Funcionalidades Vendedor aparece repetido con distinto GAP: no consolidar, tienen targets distintos."],
   ["t13","p2","task","Calcular GAP e impacto = (CSAT − target) × encuestas ÷ 136.434","2026-10-16","2026-10-16","alta","completada",100,["t12"],""],
   ["t14","p2","task","Ordenar los 4 procesos más críticos y justificar (GAP + volumen de encuestas)","2026-10-16","2026-10-17","alta","en_curso",85,["t12","t13"],"Ojo: en la diapositiva actual el 4.º lugar es Drivers (+0,57 pp, por encima de su target). Decidir si es criticidad o solo oportunidad por volumen."],
   ["t15","p2","task","Elegir 1.ª y 2.ª prioridad y explicar el motivo","2026-10-17","2026-10-17","alta","completada",100,["t14"],"1.ª Post Compra Funcionalidades Vendedor · 2.ª Viaje del paquete – Comprador."],
   ["t16","p2","task","Gráfico de cascada editable del impacto por proceso","2026-10-17","2026-10-18","media","completada",100,["t13"],""],
   ["t17","p2","task","Limitaciones, supuestos y datos adicionales necesarios (10 datos)","2026-10-17","2026-10-18","alta","completada",100,["t14"],"Experticia, LDAP rep/TL, oficina, detalle por ID de caso, CDU, histórico 3 meses, site, Copilot, Estilo Meli."],
   ["t18","p2","task","Corregir el 4.º proceso de la priorización en la diapositiva","2026-10-19","2026-10-19","alta","pendiente",0,["t14"],"Drivers supera su target: revisar si debe ir en el top 4 de criticidad o explicarlo como oportunidad por volumen."],

   ["t19","p3","task","Definir público destinatario y objetivo de aprendizaje observable","2026-10-17","2026-10-17","alta","completada",100,["t15"],""],
   ["t20","p3","task","Elegir formato (sincrónico / asincrónico) y justificar por qué","2026-10-17","2026-10-17","alta","completada",100,["t19"],""],
   ["t21","p3","task","Agenda de 60 min: duración, modalidad, propósito y acciones de participante y facilitador","2026-10-17","2026-10-18","alta","completada",100,["t20"],""],
   ["t22","p3","task","Qué validar y con quién antes de producir el contenido (CS, Producto, BPO, QS)","2026-10-18","2026-10-18","media","completada",100,["t20"],""],
   ["t23","p3","task","Definir cómo medir la efectividad (4 niveles y regla de decisión)","2026-10-18","2026-10-18","alta","completada",100,["t21"],"Versión sencilla lista (v9). Falta reemplazar la diapositiva en la presentación actual."],
   ["t24","p3","task","Plan semana a semana (PDA) y herramientas de apoyo","2026-10-18","2026-10-19","media","en_curso",80,["t21"],""],

   ["t25","p4","task","Registrar las herramientas usadas (Claude, ChatGPT, Gemini) y para qué","2026-10-18","2026-10-19","alta","en_curso",50,[],"Sé específica con lo que hizo cada herramienta: puede preguntarse en la entrevista."],
   ["t26","p4","task","Validar con ChatGPT y Gemini los puntos clave (cálculos, priorización, plan)","2026-10-19","2026-10-20","alta","pendiente",0,["t25"],""],
   ["t27","p4","task","Documentar un ejemplo concreto revisado, validado o modificado","2026-10-20","2026-10-20","alta","pendiente",0,["t26"],"Pide: un ejemplo de algo que revisaste, validaste o modificaste de la respuesta de la IA."],
   ["t28","p4","task","Agregar la diapositiva de IA al final de la presentación","2026-10-20","2026-10-20","alta","pendiente",0,["t27","t23"],"La presentación actual termina en «Gracias» y no incluye la diapositiva de IA."],

   ["t40","p5","milestone","Hito · Borrador completo listo para revisión","2026-10-20","2026-10-20","alta","pendiente",0,["t11","t18","t24","t28"],""],
   ["t29","p5","review","Revisión 1 · Consistencia de cifras (80,82% · 80,12% · −0,70 pp · 136.434 enc.)","2026-10-20","2026-10-21","alta","pendiente",0,["t40"],"Las mismas cifras en todas las diapositivas."],
   ["t30","p5","review","Revisión 2 · Ortografía y redacción (ej. «informació», «a el rep»)","2026-10-20","2026-10-21","media","pendiente",0,["t40"],""],
   ["t31","p5","review","Revisión 3 · Diseño y legibilidad (letra, orden, identificación de las 4 partes)","2026-10-21","2026-10-21","media","pendiente",0,["t29","t30"],""],
   ["t32","p5","review","Revisión externa: feedback de un colega o líder","2026-10-21","2026-10-22","media","pendiente",0,["t31"],"Opcional, pero recomendable."],
   ["t33","p5","task","Aplicar los ajustes finales","2026-10-22","2026-10-22","alta","pendiente",0,["t32"],""],

   ["t34","p6","task","Responder: ¿cuáles son tus 3 principales motivos de interés en la posición?","2026-10-19","2026-10-21","alta","pendiente",0,[],"Pregunta del formulario."],
   ["t35","p6","task","Responder: según el desafío del rol, ¿qué consideras que puedes aportar?","2026-10-19","2026-10-21","alta","pendiente",0,[],"Pregunta del formulario."],
   ["t36","p6","task","Pasar la presentación a Google Slides y revisar el formato","2026-10-22","2026-10-22","alta","pendiente",0,["t31","t33"],"Al importar el .pptx pueden moverse textos y formas: revisar diapositiva por diapositiva."],
   ["t37","p6","review","Verificar enlace y permisos de la presentación (probar con otra cuenta)","2026-10-22","2026-10-22","alta","pendiente",0,["t36"],""],
   ["t38","p6","task","Cargar el archivo en «Anexos» y revisar todo el formulario","2026-10-23","2026-10-23","alta","pendiente",0,["t37","t34","t35"],""],
   ["t39","p6","milestone","ENTREGA FINAL · Enviar Work Sample","2026-10-23","2026-10-23","alta","pendiente",0,["t38"],"Botón «Enviar Work Sample» del formulario."]
  ];
  return {
    v:1,
    cfg:{start:"2026-10-14",due:"2026-10-23"},
    phases:P.map(p=>({id:p[0],name:p[1],color:p[2]})),
    tasks:T.map(t=>({id:t[0],phase:t[1],type:t[2],name:t[3],start:t[4],end:t[5],prio:t[6],status:t[7],pct:t[8],deps:t[9],notes:t[10],prev:null})),
    ui:{view:"gantt",zoom:56,deps:true,collapsed:{},q:"",ph:"",st:"",pr:"",od:false,cas:false}
  };
}

/* ============ estado y guardado ============ */
let S, storageOK=true;
const KS={keep:false};let GG=null;
function load(){
  try{
    const r=localStorage.getItem(KEY);
    if(r){const o=JSON.parse(r);if(o&&Array.isArray(o.tasks)&&Array.isArray(o.phases)&&o.cfg){o.ui=Object.assign(seed().ui,o.ui||{});return o}}
  }catch(e){storageOK=false}
  return seed();
}
function save(){
  try{localStorage.setItem(KEY,JSON.stringify(S));storageOK=true}catch(e){storageOK=false}
  const el=document.getElementById("saved"),b=document.getElementById("banner");
  el.classList.toggle("err",!storageOK);
  el.lastChild.textContent=storageOK?"Guardado "+new Date().toLocaleTimeString("es-CO",{hour:"2-digit",minute:"2-digit"}):"Sin guardar";
  b.style.display=storageOK?"none":"block";
}
const $=id=>document.getElementById(id);
function el(tag,attrs,kids){
  const e=document.createElement(tag);
  if(attrs)for(const k in attrs){const v=attrs[k];if(v==null||v===false)continue;
    if(k==="class")e.className=v;else if(k==="style")e.style.cssText=v;else if(k.startsWith("on"))e.addEventListener(k.slice(2),v);else if(k==="text")e.textContent=v;else if(v===true)e.setAttribute(k,"");else e.setAttribute(k,v)}
  (kids||[]).forEach(c=>{if(c==null)return;e.appendChild(typeof c==="string"?document.createTextNode(c):c)});
  return e;
}
let toastT;
function toast(m){const t=$("toast");t.textContent=m;t.classList.add("on");clearTimeout(toastT);toastT=setTimeout(()=>t.classList.remove("on"),2600)}

/* ============ lógica de tareas ============ */
const byId=id=>S.tasks.find(t=>t.id===id);
const ph=id=>S.phases.find(p=>p.id===id)||{name:"—",color:"#999"};
const sN=t=>d2n(t.start), eN=t=>d2n(t.end);
const isDone=t=>t.status==="completada";
const isOd=t=>!isDone(t)&&eN(t)<todayN();
const isSoon=t=>!isDone(t)&&eN(t)>=todayN()&&eN(t)<=todayN()+3;
const waiting=t=>!isDone(t)&&t.deps.some(d=>{const p=byId(d);return p&&!isDone(p)})&&sN(t)<=todayN();
const depBad=t=>t.deps.some(d=>{const p=byId(d);return p&&sN(t)<eN(p)});
const nid=()=>"t"+Date.now().toString(36)+Math.floor(Math.random()*1e3).toString(36);

function setPct(t,p){
  p=Math.max(0,Math.min(100,Math.round(p/5)*5||0));
  t.pct=p;
  if(p===100){if(!isDone(t))t.prev=null;t.status="completada"}
  else if(isDone(t)){t.status="en_curso"}
  else if(p>0&&t.status==="pendiente"){t.status="en_curso"}
  else if(p===0&&t.status==="en_curso"){t.status="pendiente"}
}
function setStatus(t,s){
  if(s==="completada"&&!isDone(t)){t.prev=t.pct<100?t.pct:null;t.pct=100}
  else if(s!=="completada"&&isDone(t)){t.pct=t.prev!=null?t.prev:(s==="pendiente"?0:50)}
  else if(s==="pendiente"&&t.pct>0&&t.pct<100){t.pct=0}
  else if(s==="en_curso"&&t.pct===0){t.pct=10}
  t.status=s;
}
function toggleDone(t){if(isDone(t)){setStatus(t,t.prev!=null&&t.prev>0?"en_curso":"pendiente")}else setStatus(t,"completada")}
function wouldCycle(id,dep){ // ¿dep depende (directa o indirectamente) de id?
  const seen=new Set();const st=[dep];
  while(st.length){const x=st.pop();if(x===id)return true;if(seen.has(x))continue;seen.add(x);const t=byId(x);if(t)t.deps.forEach(d=>st.push(d))}
  return false;
}
function adjust(){
  let moved=new Set(),guard=0,ch=true;
  while(ch&&guard++<300){
    ch=false;
    S.tasks.forEach(t=>{
      if(isDone(t))return;
      let need=-1e9;t.deps.forEach(d=>{const p=byId(d);if(p)need=Math.max(need,eN(p))});
      if(need>-1e9&&sN(t)<need){const sh=need-sN(t);t.start=n2d(sN(t)+sh);t.end=n2d(eN(t)+sh);moved.add(t.id);ch=true}
    });
  }
  return moved.size;
}
function overall(){
  let w=0,s=0;S.tasks.forEach(t=>{const wt=t.type==="milestone"?1:Math.max(1,eN(t)-sN(t)+1);w+=wt;s+=wt*(isDone(t)?100:t.pct)});
  return w?Math.round(s/w):0;
}
function phaseStats(pid){
  const ts=S.tasks.filter(t=>t.phase===pid);
  let w=0,s=0;ts.forEach(t=>{const wt=t.type==="milestone"?1:Math.max(1,eN(t)-sN(t)+1);w+=wt;s+=wt*(isDone(t)?100:t.pct)});
  return {n:ts.length,done:ts.filter(isDone).length,pct:w?Math.round(s/w):0,ts};
}
function matches(t){
  const u=S.ui;
  if(u.ph&&t.phase!==u.ph)return false;
  if(u.st&&t.status!==u.st)return false;
  if(u.pr&&t.prio!==u.pr)return false;
  if(u.od&&!isOd(t))return false;
  if(u.q&&!(t.name+" "+t.notes).toLowerCase().includes(u.q.toLowerCase()))return false;
  return true;
}
const filtering=()=>{const u=S.ui;return !!(u.ph||u.st||u.pr||u.od||u.q)};

/* ============ KPIs ============ */
function renderKPIs(){
  const T=S.tasks,tot=T.length,done=T.filter(isDone).length,od=T.filter(isOd).length,soon=T.filter(isSoon).length,pend=tot-done;
  const left=d2n(S.cfg.due)-todayN(),p=overall();
  const k=$("kpis");k.innerHTML="";
  k.appendChild(el("div",{class:"kpi main"},[el("div",{class:"l",text:"Progreso general"}),el("div",{class:"v",text:p+"%"}),el("div",{class:"pbar"},[el("b",{style:"width:"+p+"%"})]),el("div",{class:"s",text:done+" de "+tot+" tareas completadas · ponderado por duración"})]));
  const card=(cls,l,v,s,fn)=>k.appendChild(el(fn?"button":"div",{class:"kpi "+cls,onclick:fn,title:fn?"Clic para filtrar":null},[el("div",{class:"l",text:l}),el("div",{class:"v",text:v}),el("div",{class:"s",text:s})]));
  card("green","Completadas",String(done),"de "+tot+" actividades");
  card("","Pendientes por hacer",String(pend),T.filter(t=>t.status==="en_curso"||t.status==="revision").length+" en curso o revisión");
  card(od?"red":"","Atrasadas",String(od),od?"Clic para ver solo estas":"Todo al día",()=>{S.ui.od=!S.ui.od;save();render()});
  card(soon?"amber":"","Vencen en 3 días",String(soon),"según su fecha de fin");
  card(left<0?"red":left<=2?"amber":"","Entrega final",left<0?"Vencida":left===0?"Hoy":left+" d",fmt(d2n(S.cfg.due),{year:"numeric"}));
}

/* ============ filtros / barra ============ */
function renderBar(){
  const opt=(v,l)=>el("option",{value:v,text:l});
  const f=(id,list,cur)=>{const s=$(id);s.innerHTML="";list.forEach(o=>s.appendChild(opt(o[0],o[1])));s.value=cur};
  f("fPh",[["","Todas las fases"]].concat(S.phases.map(p=>[p.id,p.name])),S.ui.ph);
  f("fSt",[["","Todos los estados"]].concat(Object.keys(ST).map(k=>[k,ST[k].l])),S.ui.st);
  f("fPr",[["","Toda prioridad"]].concat(Object.keys(PR).map(k=>[k,PR[k].l])),S.ui.pr);
  $("fQ").value=S.ui.q;$("fOd").checked=S.ui.od;$("fCas").checked=S.ui.cas;$("fDep").checked=S.ui.deps!==false;
  document.querySelectorAll("#tabs .tab").forEach(b=>{b.setAttribute("aria-selected",b.dataset.v===S.ui.view)});
  document.querySelectorAll(".seg button").forEach(b=>b.setAttribute("aria-pressed",String(+b.dataset.z===S.ui.zoom)));
  $("ganttCtl").style.display=S.ui.view==="gantt"?"flex":"none";
  $("bFold").textContent=Object.values(S.ui.collapsed).some(Boolean)?"Desplegar fases":"Plegar fases";
}

/* ============ vista: cronograma (Gantt) ============ */
const LW=400,RH=40,PH=34,HH=60;
function renderGantt(){
  const dw=S.ui.zoom,TD=todayN();
  let min=Math.min(d2n(S.cfg.start),TD-1),max=Math.max(d2n(S.cfg.due),TD+1);
  S.tasks.forEach(t=>{min=Math.min(min,sN(t));max=Math.max(max,eN(t))});
  min-=1;max+=3;
  const avail=Math.max(0,($("view").clientWidth||window.innerWidth)-LW-4);
  if((max-min+1)*dw<avail)max=min+Math.ceil(avail/dw)-1;
  const days=max-min+1,W=days*dw;
  /* filas visibles */
  const rows=[];
  S.phases.forEach(p=>{
    const ts=S.tasks.filter(t=>t.phase===p.id&&matches(t)).sort((a,b)=>sN(a)-sN(b)||eN(a)-eN(b));
    if(filtering()&&!ts.length)return;
    rows.push({k:"ph",p,ts});
    if(!S.ui.collapsed[p.id])ts.forEach(t=>rows.push({k:"t",t,p}));
  });
  let y=0;rows.forEach(r=>{r.y=y;r.h=r.k==="ph"?PH:RH;y+=r.h});
  const H=y;
  const wrap=el("div",{class:"gwrap",id:"gwrap"});
  const inner=el("div",{class:"ginner",style:"width:"+(LW+W)+"px"});
  /* cabecera */
  const mr=el("div",{class:"mrow"}),dr=el("div",{class:"drow"});
  let i=0;
  while(i<days){
    const n=min+i,d=new Date(n*DAY);let j=i;
    while(j<days&&new Date((min+j)*DAY).getUTCMonth()===d.getUTCMonth())j++;
    const mn=d.toLocaleDateString("es-CO",{month:"long",year:"numeric",timeZone:"UTC"});mr.appendChild(el("div",{style:"width:"+((j-i)*dw)+"px",text:mn.charAt(0).toUpperCase()+mn.slice(1)}));
    i=j;
  }
  for(let k=0;k<days;k++){
    const n=min+k,c=el("div",{class:(isWE(n)?"we ":"")+(n===TD?"td":""),style:"width:"+dw+"px"});
    const dn=new Date(n*DAY);
    c.appendChild(el("b",{text:String(dn.getUTCDate())}));
    if(dw>=30)c.appendChild(document.createTextNode(dn.toLocaleDateString("es-CO",{weekday:"short",timeZone:"UTC"}).slice(0,2)));
    dr.appendChild(c);
  }
  const ghl=el("div",{class:"gh-left",style:"width:"+LW+"px;height:"+HH+"px"},[el("span",{text:"Actividad"}),el("span",{text:"Avance"})]);
  const ghr=el("div",{class:"gh-right",style:"width:"+W+"px"},[mr,dr]);
  inner.appendChild(el("div",{class:"ghead",style:"height:"+HH+"px"},[ghl,ghr]));
  /* cuerpo */
  const gl=el("div",{class:"gleft",style:"width:"+LW+"px;height:"+H+"px"});
  const gr=el("div",{class:"gright",style:"width:"+W+"px;height:"+H+"px;background-image:linear-gradient(to right,#EEF0F8 1px,transparent 1px);background-size:"+dw+"px 100%"});
  for(let k=0;k<days;k++){const n=min+k;if(isWE(n))gr.appendChild(el("div",{class:"we-col",style:"left:"+(k*dw)+"px;width:"+dw+"px"}))}
  const pos={}; // id -> {x1,x2,yc}
  rows.forEach(r=>{
    gr.appendChild(el("div",{class:"rl"+(r.k==="ph"?" ph":""),style:"top:"+(r.y+r.h-1)+"px;height:0"}));
    if(r.k==="ph"){
      const st=phaseStats(r.p.id),col=r.p.color,coll=!!S.ui.collapsed[r.p.id];
      gl.appendChild(el("div",{class:"lrow ph",style:"height:"+r.h+"px"},[
        el("button",{class:"caret"+(coll?" c":""),"aria-label":(coll?"Desplegar ":"Plegar ")+r.p.name,"aria-expanded":String(!coll),onclick:()=>{S.ui.collapsed[r.p.id]=!coll;save();render()},text:"▼"}),
        el("span",{class:"dot",style:"background:"+col}),
        el("span",{style:"flex:1;min-width:0;overflow:hidden;text-overflow:ellipsis;white-space:nowrap",text:r.p.name}),
        el("span",{class:"tag bl",text:st.done+"/"+st.n}),
        el("span",{class:"pc",text:st.pct+"%"}),
        el("button",{class:"btn sm",title:"Agregar actividad a esta fase","aria-label":"Agregar actividad a "+r.p.name,style:"padding:1px 7px",onclick:()=>openTask(null,{phase:r.p.id}),text:"＋"})
      ]));
      if(r.ts.length){
        const s0=Math.min.apply(null,r.ts.map(sN)),e0=Math.max.apply(null,r.ts.map(eN));
        const b=el("div",{class:"phbar",style:"left:"+((s0-min)*dw)+"px;width:"+((e0-s0+1)*dw)+"px;top:"+(r.y+10)+"px;background:"+col+"33;border:1.5px solid "+col+";color:"+col},[el("div",{style:"height:100%;width:"+st.pct+"%;background:"+col+";border-radius:2px"})]);
        b.title=r.p.name+" · "+st.pct+"%";gr.appendChild(b);
      }
    }else{
      const t=r.t,col=r.p.color,od=isOd(t),soon=isSoon(t),done=isDone(t),ms=t.type==="milestone";
      const row=el("div",{class:"lrow task"+(done?" done":""),style:"height:"+r.h+"px"});
      row.appendChild(el("button",{class:"cb",role:"checkbox","aria-checked":String(done),"aria-label":"Marcar «"+t.name+"» como "+(done?"pendiente":"completada"),onclick:()=>{toggleDone(t);save();render()}}));
      row.appendChild(el("span",{class:"dot",style:"background:"+PR[t.prio].c,title:"Prioridad "+PR[t.prio].l}));
      row.appendChild(el("button",{class:"nm",title:t.name,onclick:()=>openTask(t.id),text:(ms?"◆ ":t.type==="review"?"✎ ":"")+t.name}));
      if(od)row.appendChild(el("span",{class:"tag od",text:"ATRASADA"}));
      else if(soon)row.appendChild(el("span",{class:"tag ds",text:"PRONTO"}));
      else if(t.status==="bloqueada")row.appendChild(el("span",{class:"tag bl",text:"BLOQUEADA"}));
      if(depBad(t)&&!done)row.appendChild(el("span",{class:"tag od",title:"Empieza antes de que termine una predecesora",text:"⚠"}));
      row.appendChild(el("span",{class:"pc",text:(done?100:t.pct)+"%"}));
      gl.appendChild(row);
      const s=sN(t),e=eN(t),yc=r.y+r.h/2;
      if(ms){
        const cx=(e-min)*dw+dw/2;
        const m=el("div",{class:"ms"+(od?" od":"")+(done?" done":""),"data-id":t.id,"data-m":"move",style:"left:"+(cx-10)+"px;top:"+(yc-10)+"px;background:"+(done?"#1E8E5A":col)+";border-color:"+col,title:t.name+" · "+fmt(e)});
        gr.appendChild(m);pos[t.id]={x1:cx-14,x2:cx+14,yc};
      }else{
        const w=(e-s+1)*dw,x=(s-min)*dw;
        const b=el("div",{class:"bar-t"+(od?" od":"")+(done?" done":"")+(t.status==="bloqueada"?" bl":"")+(t.type==="review"?" rev":""),"data-id":t.id,"data-m":"move",style:"left:"+x+"px;width:"+w+"px;top:"+(yc-12)+"px;background:"+col+"40;border-color:"+col,title:t.name+" · "+fmt(s)+" → "+fmt(e)+" · "+(done?100:t.pct)+"%"},[
          el("div",{class:"fill",style:"width:"+(done?100:t.pct)+"%;background:"+col}),
          el("span",{class:"lb",text:w>=46?((done?"✓ ":"")+(done?100:t.pct)+"%"):""}),
          el("div",{class:"h l","data-m":"l"}),el("div",{class:"h r","data-m":"r"})
        ]);
        gr.appendChild(b);pos[t.id]={x1:x,x2:x+w,yc};
      }
    }
  });
  /* líneas hoy / entrega */
  gr.appendChild(el("div",{class:"tl",style:"left:"+((TD-min)*dw+dw/2-1)+"px"}));
  gr.appendChild(el("div",{class:"dl",style:"left:"+((d2n(S.cfg.due)-min+1)*dw)+"px"}));
  /* dependencias */
  const NS="http://www.w3.org/2000/svg";
  const svg=document.createElementNS(NS,"svg");svg.setAttribute("class","deps");svg.setAttribute("width",W);svg.setAttribute("height",H);
  svg.innerHTML='<defs><marker id="ar" viewBox="0 0 8 8" refX="7" refY="4" markerWidth="7" markerHeight="7" orient="auto"><path d="M0 0 L8 4 L0 8z" fill="#8A90A8"/></marker><marker id="arr" viewBox="0 0 8 8" refX="7" refY="4" markerWidth="7" markerHeight="7" orient="auto"><path d="M0 0 L8 4 L0 8z" fill="#D6453D"/></marker></defs>';
  if(S.ui.deps!==false)S.tasks.forEach(t=>{
    const b=pos[t.id];if(!b)return;
    t.deps.forEach(d=>{
      const a=pos[d],p=byId(d);if(!a||!p)return;
      const bad=sN(t)<eN(p)&&!isDone(t);
      const x1=a.x2,y1=a.yc,x2=b.x1,y2=b.yc,g=8;
      let dd;
      if(x2>=x1+2*g)dd=`M${x1} ${y1} H${x1+g} V${y2} H${x2}`;
      else{const ym=y2>y1?y1+RH/2:y1-RH/2;dd=`M${x1} ${y1} H${x1+g} V${ym} H${x2-g} V${y2} H${x2}`}
      const path=document.createElementNS(NS,"path");
      path.setAttribute("d",dd);path.setAttribute("fill","none");path.setAttribute("stroke",bad?"#D6453D":"#9AA0BC");path.setAttribute("stroke-width",bad?"1.6":"1.1");
      path.setAttribute("marker-end","url(#"+(bad?"arr":"ar")+")");
      svg.appendChild(path);
    });
  });
  gr.appendChild(svg);
  inner.appendChild(el("div",{class:"gbody"},[gl,gr]));
  wrap.appendChild(inner);
  const card=el("div",{class:"card"},[wrap,el("div",{class:"legend"},[
    el("span",{},[el("i",{style:"background:#3F51B5"}),"Barra = actividad (relleno = avance)"]),
    el("span",{},[el("i",{style:"border:2px dashed #C2410C;background:none"}),"Revisión"]),
    el("span",{text:"◆ Hito"}),
    el("span",{},[el("i",{style:"background:none;border:2px solid #D6453D"}),"Atrasada"]),
    el("span",{style:"color:#D6453D",text:"→ Flecha roja: la sucesora empieza antes de que termine su predecesora"}),
    el("span",{text:"Arrastra una barra para moverla y sus bordes para cambiar la duración · clic para editar"})
  ])]);
  if(!rows.length)wrap.appendChild(el("div",{class:"empty",style:"padding:30px;text-align:center",text:"No hay actividades con estos filtros."}));
  const v=$("view");
  const oldWrap=$("gwrap"),sl=oldWrap?oldWrap.scrollLeft:null,st=oldWrap?oldWrap.scrollTop:0;
  v.innerHTML="";v.appendChild(card);
  if(sl!=null&&KS.keep){wrap.scrollLeft=sl;wrap.scrollTop=st}
  else{wrap.scrollLeft=Math.max(0,(TD-min)*dw-120)}
  KS.keep=false;
  GG={min,dw};
  wrap.addEventListener("pointerdown",onDown);
}
/* arrastre */
let drag=null;
function onDown(e){
  const bar=e.target.closest("[data-id]");if(!bar||e.button>0)return;
  const t=byId(bar.dataset.id);if(!t)return;
  const mode=(e.target.dataset&&e.target.dataset.m&&e.target.dataset.m!=="move")?e.target.dataset.m:"move";
  drag={t,bar,mode,x0:e.clientX,s:sN(t),e:eN(t),moved:false,d:0};
  bar.setPointerCapture(e.pointerId);
  bar.addEventListener("pointermove",onMove);bar.addEventListener("pointerup",onUp);bar.addEventListener("pointercancel",onUp);
}
function onMove(e){
  if(!drag)return;const dw=GG.dw,dx=e.clientX-drag.x0;
  if(Math.abs(dx)>3)drag.moved=true;if(!drag.moved)return;
  let d=Math.round(dx/dw),s=drag.s,en=drag.e;
  if(drag.t.type==="milestone"){s+=d;en+=d}
  else if(drag.mode==="move"){s+=d;en+=d}
  else if(drag.mode==="l"){s=Math.min(s+d,en);d=s-drag.s}
  else{en=Math.max(en+d,s);d=en-drag.e}
  drag.d=d;drag.ns=s;drag.ne=en;
  const b=drag.bar,min=GG.min;
  if(drag.t.type==="milestone"){b.style.left=((en-min)*dw+dw/2-10)+"px"}
  else{b.style.left=((s-min)*dw)+"px";b.style.width=((en-s+1)*dw)+"px"}
  b.title=fmt(s)+" → "+fmt(en);
}
function onUp(e){
  if(!drag)return;const b=drag.bar;
  b.removeEventListener("pointermove",onMove);b.removeEventListener("pointerup",onUp);b.removeEventListener("pointercancel",onUp);
  const dr=drag;drag=null;
  if(!dr.moved){openTask(dr.t.id);return}
  if(dr.d!==0||dr.ns!==dr.s||dr.ne!==dr.e){
    dr.t.start=n2d(dr.ns);dr.t.end=n2d(dr.ne);
    let msg="Fechas actualizadas";
    if(S.ui.cas){const n=adjust();if(n)msg+=" · "+n+" sucesora(s) movida(s)"}
    else if(depBad(dr.t))msg="⚠ Empieza antes de que termine una predecesora";
    save();KS.keep=true;render();toast(msg);
  }else{KS.keep=true;render()}
}

/* ============ vista: lista editable ============ */
function renderList(){
  const tb=el("table",{class:"tbl"});
  tb.appendChild(el("thead",{},[el("tr",{},["✓","Actividad","Tipo","Inicio","Fin","Prioridad","Estado","Avance","Depende de",""].map(h=>el("th",{text:h})))]));
  const body=el("tbody");let any=false;
  S.phases.forEach(p=>{
    const ts=S.tasks.filter(t=>t.phase===p.id&&matches(t)).sort((a,b)=>sN(a)-sN(b)||eN(a)-eN(b));
    if(filtering()&&!ts.length)return;
    const st=phaseStats(p.id);any=true;
    body.appendChild(el("tr",{class:"phr"},[el("td",{colspan:"10"},[
      el("div",{style:"display:flex;align-items:center;gap:10px"},[
        el("span",{class:"dot",style:"background:"+p.color}),el("span",{text:p.name}),
        el("span",{class:"tag bl",text:st.done+"/"+st.n+" · "+st.pct+"%"}),
        el("button",{class:"btn sm",onclick:()=>openTask(null,{phase:p.id}),text:"＋ Actividad"}),
        el("button",{class:"btn sm",onclick:()=>openPhase(p.id),text:"Editar fase"})
      ])])]));
    ts.forEach(t=>{
      const tr=el("tr",{class:isDone(t)?"done":""});
      const upd=(fn)=>()=>{fn();save();KS.keep=true;render()};
      tr.appendChild(el("td",{},[el("button",{class:"cb",role:"checkbox","aria-checked":String(isDone(t)),"aria-label":"Completar «"+t.name+"»",onclick:upd(()=>toggleDone(t))})]));
      const nm=el("td",{class:"nmc",style:"min-width:260px"},[el("button",{class:"nm",style:"background:none;border:0;text-align:left;padding:0;cursor:pointer;color:inherit;text-decoration:inherit",onclick:()=>openTask(t.id),text:t.name})]);
      if(isOd(t))nm.appendChild(el("span",{class:"tag od",style:"margin-left:8px",text:"ATRASADA"}));
      else if(isSoon(t))nm.appendChild(el("span",{class:"tag ds",style:"margin-left:8px",text:"PRONTO"}));
      if(depBad(t)&&!isDone(t))nm.appendChild(el("span",{class:"tag od",style:"margin-left:6px",title:"Empieza antes de que termine una predecesora",text:"⚠"}));
      tr.appendChild(nm);
      tr.appendChild(el("td",{text:TY[t.type],style:"color:#5B6178;white-space:nowrap"}));
      const di=(k)=>{const i=el("input",{type:"date",value:t[k],"aria-label":(k==="start"?"Inicio":"Fin")+" de "+t.name});i.addEventListener("change",()=>{if(!i.value)return;t[k]=i.value;if(d2n(t.end)<d2n(t.start)){if(k==="start")t.end=t.start;else t.start=t.end}if(t.type==="milestone"){t.start=t.end=i.value}save();KS.keep=true;render()});return el("td",{},[i])};
      tr.appendChild(di("start"));tr.appendChild(di("end"));
      const sel=(map,key,fn)=>{const s=el("select",{"aria-label":key+" de "+t.name});Object.keys(map).forEach(k=>s.appendChild(el("option",{value:k,text:map[k].l})));s.value=t[key];s.addEventListener("change",()=>{fn(s.value);save();KS.keep=true;render()});return s};
      tr.appendChild(el("td",{},[sel(PR,"prio",v=>t.prio=v)]));
      const stSel=sel(ST,"status",v=>setStatus(t,v));
      tr.appendChild(el("td",{},[stSel]));
      const rg=el("input",{type:"range",min:"0",max:"100",step:"5",value:String(t.pct),"aria-label":"Avance de "+t.name});
      const lab=el("span",{text:t.pct+"%",style:"font-weight:700;min-width:36px"});
      rg.addEventListener("input",()=>lab.textContent=rg.value+"%");
      rg.addEventListener("change",()=>{setPct(t,+rg.value);save();KS.keep=true;render()});
      tr.appendChild(el("td",{},[el("div",{class:"pcw"},[rg,lab])]));
      tr.appendChild(el("td",{style:"color:#5B6178;font-size:12px;max-width:200px"},[t.deps.map(d=>{const p=byId(d);return p?p.name.split(" ").slice(0,3).join(" ")+"…":""}).join(" · ")||"—"]));
      tr.appendChild(el("td",{},[el("button",{class:"btn sm",onclick:()=>openTask(t.id),text:"Editar"})]));
      body.appendChild(tr);
    });
  });
  tb.appendChild(body);
  const v=$("view");v.innerHTML="";
  v.appendChild(el("div",{class:"card"},[el("div",{class:"tscroll"},[tb]),any?null:el("div",{class:"empty",style:"padding:30px;text-align:center",text:"No hay actividades con estos filtros."})]));
}

/* ============ vista: qué sigue ============ */
function renderPanel(){
  const T=S.tasks.filter(matches),TD=todayN();
  const item=t=>{
    const c=ph(t.phase).color;
    return el("div",{class:"item"},[
      el("button",{class:"cb",role:"checkbox","aria-checked":String(isDone(t)),"aria-label":"Completar «"+t.name+"»",onclick:()=>{toggleDone(t);save();render()}}),
      el("span",{class:"dot",style:"background:"+PR[t.prio].c+";margin-top:6px",title:"Prioridad "+PR[t.prio].l}),
      el("div",{class:"tx"},[el("button",{class:"nm",onclick:()=>openTask(t.id),text:t.name,title:ph(t.phase).name}),
      el("small",{text:(eN(t)<TD?"Venció ":"Vence ")+fmt(eN(t))+" · avance "+t.pct+"%"})])
    ]);
  };
  const box=(cls,title,list,empty)=>el("div",{class:"card pcard "+cls},[el("h3",{},[el("span",{text:title}),el("em",{text:String(list.length)})]),list.length?el("div",{},list.map(item)):el("div",{class:"empty",text:empty})]);
  const od=T.filter(isOd).sort((a,b)=>eN(a)-eN(b));
  const soon=T.filter(isSoon).sort((a,b)=>eN(a)-eN(b));
  const run=T.filter(t=>!isDone(t)&&(t.status==="en_curso"||t.status==="revision")&&!isOd(t));
  const next=T.filter(t=>!isDone(t)&&!isOd(t)&&!isSoon(t)&&t.status==="pendiente"&&sN(t)<=TD+7).sort((a,b)=>sN(a)-sN(b)||PR[a.prio].o-PR[b.prio].o);
  const blocked=T.filter(t=>!isDone(t)&&(t.status==="bloqueada"||waiting(t)));
  const dueN=d2n(S.cfg.due);
  const g=el("div",{class:"pgrid"},[
    box("red","Atrasadas",od,"Nada atrasado. Buen ritmo."),
    box("amber","Vencen en los próximos 3 días",soon,"Nada vence en los próximos 3 días."),
    box("","En curso / en revisión",run,"Nada en curso ahora mismo."),
    box("","Por empezar (próximos 7 días)",next,"No hay actividades por empezar esta semana."),
    box("","Esperando una predecesora o bloqueadas",blocked,"Ninguna actividad está esperando a otra."),
  ]);
  const phc=el("div",{class:"card pcard"},[el("h3",{},[el("span",{text:"Avance por fase"})])]);
  S.phases.forEach(p=>{const st=phaseStats(p.id);phc.appendChild(el("div",{class:"ph-row"},[
    el("span",{style:"display:flex;gap:8px;align-items:center;min-width:0"},[el("span",{class:"dot",style:"background:"+p.color}),el("span",{style:"white-space:nowrap;overflow:hidden;text-overflow:ellipsis",text:p.name,title:p.name})]),
    el("div",{class:"pbar lt"},[el("b",{style:"width:"+st.pct+"%;background:"+p.color})]),
    el("span",{style:"font-weight:800;text-align:right",text:st.pct+"% · "+st.done+"/"+st.n})]))});
  g.appendChild(phc);
  /* próximas fechas límite */
  const up=S.tasks.filter(t=>!isDone(t)&&eN(t)>=TD).sort((a,b)=>eN(a)-eN(b)).slice(0,8);
  const dl=el("div",{class:"card pcard"},[el("h3",{},[el("span",{text:"Próximas fechas límite"})])]);
  up.forEach(t=>dl.appendChild(el("div",{class:"item"},[el("small",{style:"min-width:78px;font-weight:700;color:#1B1F3B",text:fmt(eN(t))}),el("button",{class:"nm",onclick:()=>openTask(t.id),text:t.name})])));
  dl.appendChild(el("div",{class:"item"},[el("small",{style:"min-width:78px;font-weight:800;color:#D6453D",text:fmt(dueN)}),el("span",{style:"font-weight:800;color:#D6453D",text:"Entrega final (fecha del proyecto)"})]));
  g.appendChild(dl);
  const v=$("view");v.innerHTML="";v.appendChild(g);
}

/* ============ modal: actividad ============ */
function closeModal(){$("ov").classList.remove("on");$("ov").setAttribute("aria-hidden","true");$("modal").innerHTML=""}
function showModal(title,body,foot){
  const m=$("modal");m.innerHTML="";
  m.appendChild(el("div",{class:"mh"},[el("h2",{id:"mt",text:title}),el("button",{"aria-label":"Cerrar",onclick:closeModal,text:"×"})]));
  m.appendChild(body);m.appendChild(foot);
  $("ov").classList.add("on");$("ov").setAttribute("aria-hidden","false");
  const f=m.querySelector("input,select,textarea");if(f)f.focus();
}
function fld(label,node,cls){return el("div",{class:"f"+(cls?" "+cls:"")},[el("label",{text:label}),node])}
function openTask(id,defs){
  const isNew=!id,t=isNew?{id:nid(),phase:(defs&&defs.phase)||S.phases[0].id,type:"task",name:"",start:n2d(todayN()),end:n2d(todayN()+1),prio:"media",status:"pendiente",pct:0,deps:[],notes:"",prev:null}:JSON.parse(JSON.stringify(byId(id)));
  const nm=el("input",{type:"text",value:t.name,placeholder:"¿Qué hay que hacer?",maxlength:"160"});
  const phs=el("select");S.phases.forEach(p=>phs.appendChild(el("option",{value:p.id,text:p.name})));phs.value=t.phase;
  const ty=el("select");Object.keys(TY).forEach(k=>ty.appendChild(el("option",{value:k,text:TY[k]})));ty.value=t.type;
  const sd=el("input",{type:"date",value:t.start}),ed=el("input",{type:"date",value:t.end});
  const pr=el("select");Object.keys(PR).forEach(k=>pr.appendChild(el("option",{value:k,text:PR[k].l})));pr.value=t.prio;
  const stt=el("select");Object.keys(ST).forEach(k=>stt.appendChild(el("option",{value:k,text:ST[k].l})));stt.value=t.status;
  const rg=el("input",{type:"range",min:"0",max:"100",step:"5",value:String(t.pct)}),out=el("output",{text:t.pct+"%"});
  rg.addEventListener("input",()=>{out.textContent=rg.value+"%";if(+rg.value===100)stt.value="completada";else if(stt.value==="completada")stt.value="en_curso";else if(+rg.value>0&&stt.value==="pendiente")stt.value="en_curso";else if(+rg.value===0&&stt.value==="en_curso")stt.value="pendiente"});
  stt.addEventListener("change",()=>{if(stt.value==="completada"){rg.value=100;out.textContent="100%"}else if(stt.value==="pendiente"){rg.value=0;out.textContent="0%"}else if(+rg.value===100){rg.value=50;out.textContent="50%"}else if(stt.value==="en_curso"&&+rg.value===0){rg.value=10;out.textContent="10%"}});
  const notes=el("textarea",{placeholder:"Notas, enlaces, decisiones…"});notes.value=t.notes;
  const dp=el("div",{class:"dpl"});const chosen=new Set(t.deps);
  S.phases.forEach(p=>{
    const ts=S.tasks.filter(x=>x.phase===p.id&&x.id!==t.id&&!wouldCycle(t.id,x.id));
    if(!ts.length)return;
    dp.appendChild(el("div",{class:"g",text:p.name}));
    ts.forEach(x=>{const c=el("input",{type:"checkbox",value:x.id});c.checked=chosen.has(x.id);c.addEventListener("change",()=>{c.checked?chosen.add(x.id):chosen.delete(x.id);chk()});dp.appendChild(el("label",{},[c,x.name]))});
  });
  const warn=el("div",{class:"warn"});
  function chk(){
    const e1=d2n(ed.value||t.end),s1=d2n(sd.value||t.start);let bad=[];
    chosen.forEach(d=>{const p=byId(d);if(p&&s1<d2n(p.end))bad.push(p.name)});
    if(e1<s1){warn.style.display="block";warn.textContent="La fecha de fin es anterior al inicio."}
    else if(bad.length){warn.style.display="block";warn.textContent="Empieza antes de que termine «"+bad[0]+"»"+(bad.length>1?" y "+(bad.length-1)+" más":"")+". Puedes guardar y usar «Ajustar dependencias»."}
    else warn.style.display="none";
  }
  [sd,ed].forEach(i=>i.addEventListener("change",chk));
  ty.addEventListener("change",()=>{if(ty.value==="milestone"){sd.value=ed.value;chk()}});
  const body=el("div",{class:"mb"},[
    fld("Actividad",nm,"w"),
    fld("Fase",phs),fld("Tipo",ty),
    fld("Inicio",sd),fld("Fin / fecha límite",ed),
    fld("Prioridad",pr),fld("Estado",stt),
    fld("Avance",el("div",{class:"rg"},[rg,out]),"w"),
    fld("Depende de (debe terminar antes)",dp,"w"),
    warn,
    fld("Notas",notes,"w")
  ]);
  chk();
  const foot=el("div",{class:"mf"},[
    isNew?el("span"):el("button",{class:"btn dng",onclick:()=>{if(confirm("¿Eliminar esta actividad?")){S.tasks=S.tasks.filter(x=>x.id!==t.id);S.tasks.forEach(x=>x.deps=x.deps.filter(d=>d!==t.id));save();closeModal();render();toast("Actividad eliminada")}},text:"Eliminar"}),
    el("div",{style:"display:flex;gap:8px"},[
      el("button",{class:"btn",onclick:closeModal,text:"Cancelar"}),
      el("button",{class:"btn pri",onclick:()=>{
        const name=nm.value.trim();if(!name){nm.focus();nm.style.borderColor="#D6453D";return}
        if(!sd.value||!ed.value)return;
        let s=sd.value,e=ed.value;if(d2n(e)<d2n(s))e=s;if(ty.value==="milestone")s=e;
        const real=isNew?t:byId(t.id);
        const wasDone=isDone(real);
        Object.assign(real,{name,phase:phs.value,type:ty.value,start:s,end:e,prio:pr.value,notes:notes.value.trim(),deps:Array.from(chosen)});
        const wantStatus=stt.value,wantPct=+rg.value;
        if(wantStatus==="completada"&&!wasDone){real.prev=real.pct<100?real.pct:null}
        real.status=wantStatus;real.pct=wantStatus==="completada"?100:wantPct;
        if(isNew)S.tasks.push(real);
        save();closeModal();KS.keep=true;render();toast(isNew?"Actividad agregada":"Cambios guardados");
      },text:"Guardar"})
    ])
  ]);
  showModal(isNew?"Nueva actividad":"Editar actividad",body,foot);
  nm.addEventListener("keydown",e=>{if(e.key==="Enter")foot.querySelector(".pri").click()});
}
function openPhase(id){
  const isNew=!id,p=isNew?{id:"p"+Date.now().toString(36),name:"",color:"#3F51B5"}:Object.assign({},ph(id));
  const nm=el("input",{type:"text",value:p.name,placeholder:"Nombre de la fase",maxlength:"60"});
  const co=el("input",{type:"color",value:p.color,style:"padding:2px;height:38px"});
  const body=el("div",{class:"mb"},[fld("Nombre",nm,"w"),fld("Color",co)]);
  const foot=el("div",{class:"mf"},[
    isNew?el("span"):el("button",{class:"btn dng",onclick:()=>{const n=S.tasks.filter(t=>t.phase===id).length;if(confirm("¿Eliminar la fase"+(n?" y sus "+n+" actividades":"")+"?")){S.tasks.filter(t=>t.phase===id).forEach(t=>S.tasks.forEach(x=>x.deps=x.deps.filter(d=>d!==t.id)));S.tasks=S.tasks.filter(t=>t.phase!==id);S.phases=S.phases.filter(x=>x.id!==id);if(S.ui.ph===id)S.ui.ph="";save();closeModal();render();toast("Fase eliminada")}},text:"Eliminar fase"}),
    el("div",{style:"display:flex;gap:8px"},[el("button",{class:"btn",onclick:closeModal,text:"Cancelar"}),el("button",{class:"btn pri",onclick:()=>{
      const name=nm.value.trim();if(!name){nm.focus();return}
      if(isNew)S.phases.push({id:p.id,name,color:co.value});else{const r=ph(id);r.name=name;r.color=co.value}
      save();closeModal();render();toast("Fase guardada")},text:"Guardar"})])
  ]);
  showModal(isNew?"Nueva fase":"Editar fase",body,foot);
}

/* ============ render principal ============ */
function render(){
  const cs=$("cStart"),cd=$("cDue");cs.value=S.cfg.start;cd.value=S.cfg.due;
  renderKPIs();renderBar();
  if(S.ui.view==="gantt")renderGantt();else if(S.ui.view==="list")renderList();else renderPanel();
}

/* ============ eventos ============ */
function init(){
  S=load();save();
  document.querySelectorAll("#tabs .tab").forEach(b=>b.addEventListener("click",()=>{S.ui.view=b.dataset.v;save();render()}));
  document.querySelectorAll(".seg button").forEach(b=>b.addEventListener("click",()=>{S.ui.zoom=+b.dataset.z;save();render()}));
  $("fQ").addEventListener("input",e=>{S.ui.q=e.target.value;save();render();const q=$("fQ");q.focus();q.setSelectionRange(q.value.length,q.value.length)});
  $("fPh").addEventListener("change",e=>{S.ui.ph=e.target.value;save();render()});
  $("fSt").addEventListener("change",e=>{S.ui.st=e.target.value;save();render()});
  $("fPr").addEventListener("change",e=>{S.ui.pr=e.target.value;save();render()});
  $("fOd").addEventListener("change",e=>{S.ui.od=e.target.checked;save();render()});
  $("fCas").addEventListener("change",e=>{S.ui.cas=e.target.checked;save()});
  $("fDep").addEventListener("change",e=>{S.ui.deps=e.target.checked;save();KS.keep=true;render()});
  $("bToday").addEventListener("click",()=>{const w=$("gwrap");if(w&&GG)w.scrollTo({left:Math.max(0,(todayN()-GG.min)*GG.dw-160),behavior:"smooth"})});
  $("bFold").addEventListener("click",()=>{const any=Object.values(S.ui.collapsed).some(Boolean);S.phases.forEach(p=>S.ui.collapsed[p.id]=!any);save();render()});
  $("cStart").addEventListener("change",e=>{if(e.target.value){S.cfg.start=e.target.value;save();render()}});
  $("cDue").addEventListener("change",e=>{if(e.target.value){S.cfg.due=e.target.value;save();render()}});
  $("bAddT").addEventListener("click",()=>openTask(null));
  $("bAddP").addEventListener("click",()=>openPhase(null));
  $("bAdj").addEventListener("click",()=>{const n=adjust();save();render();toast(n?n+" actividad(es) reprogramada(s) según sus dependencias":"Las dependencias ya estaban en orden")});
  $("bPrint").addEventListener("click",()=>window.print());
  $("bExp").addEventListener("click",()=>{
    const blob=new Blob([JSON.stringify(S,null,2)],{type:"application/json"});
    const a=document.createElement("a");a.href=URL.createObjectURL(blob);a.download="gantt-work-sample-"+n2d(todayN())+".json";document.body.appendChild(a);a.click();a.remove();setTimeout(()=>URL.revokeObjectURL(a.href),500);toast("Copia de seguridad descargada");
  });
  $("bImp").addEventListener("click",()=>$("fImp").click());
  $("fImp").addEventListener("change",e=>{
    const f=e.target.files[0];if(!f)return;const r=new FileReader();
    r.onload=()=>{try{const o=JSON.parse(r.result);if(!o||!Array.isArray(o.tasks)||!Array.isArray(o.phases)||!o.cfg)throw 0;if(!confirm("Esto reemplaza el plan actual por el archivo importado. ¿Continuar?"))return;o.ui=Object.assign(seed().ui,o.ui||{});S=o;save();render();toast("Plan importado")}catch(x){alert("El archivo no es un respaldo válido de este Gantt.")}};
    r.readAsText(f);e.target.value="";
  });
  $("bReset").addEventListener("click",()=>{if(confirm("Se perderán tus cambios y volverá el plan inicial. ¿Restablecer? (Exporta antes si quieres conservar una copia)")){S=seed();save();render();toast("Plan restablecido")}});
  $("ov").addEventListener("mousedown",e=>{if(e.target===$("ov"))closeModal()});
  document.addEventListener("keydown",e=>{if(e.key==="Escape"&&$("ov").classList.contains("on"))closeModal()});
  window.addEventListener("storage",e=>{if(e.key===KEY&&e.newValue){try{S=JSON.parse(e.newValue);render()}catch(x){}}});
  /* re-render al cambiar el día (si la pestaña queda abierta) */
  let lastDay=todayN();setInterval(()=>{if(todayN()!==lastDay){lastDay=todayN();KS.keep=true;render()}},60000);
  render();
}
init();
</script>
</body>
</html>
