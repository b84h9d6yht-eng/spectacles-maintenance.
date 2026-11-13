# spectacles-maintenance.
<!DOCTYPE html>
<html lang="it">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SPECTACLES MAINTENANCE – Gestionale Industriale</title>
<style>
:root{
  --red:#d62828; --red-dark:#a31f1f; --dark:#1c1c1e; --gray:#8e8e93;
  --bg:#f4f4f6; --card:#ffffff; --line:#e4e4e7;
  --orange:#f59e0b; --blue:#2563eb; --green:#16a34a;
}
*{margin:0;padding:0;box-sizing:border-box;font-family:'Segoe UI',Arial,sans-serif}
body{background:var(--bg);color:var(--dark)}
#app{display:flex;min-height:100vh}
aside{width:230px;background:var(--dark);color:#fff;position:fixed;top:0;bottom:0;left:0;display:flex;flex-direction:column;z-index:100}
.logo{padding:18px 16px;border-bottom:1px solid #333;font-weight:800;font-size:17px;letter-spacing:1px}
.logo span{color:var(--red)}
.logo small{display:block;font-weight:400;font-size:10px;color:#aaa;letter-spacing:2px;margin-top:3px}
nav{flex:1;overflow-y:auto;padding:10px 0}
nav a{display:flex;align-items:center;gap:11px;padding:12px 16px;color:#d5d5d5;text-decoration:none;font-size:14px;border-left:3px solid transparent}
nav a:hover{background:#2c2c2e;color:#fff}
nav a.active{background:#2c2c2e;color:#fff;border-left-color:var(--red)}
nav a .ic{width:20px;text-align:center}
main{margin-left:230px;flex:1;padding:24px;max-width:calc(100% - 230px)}
header.topbar{display:flex;justify-content:space-between;align-items:center;margin-bottom:20px;flex-wrap:wrap;gap:10px}
header.topbar h1{font-size:22px}
header.topbar .date{font-size:13px;color:var(--gray)}
#burger{display:none;background:none;border:none;color:#fff;font-size:24px;padding:10px 14px}
.cards{display:grid;grid-template-columns:repeat(auto-fit,minmax(160px,1fr));gap:14px;margin-bottom:22px}
.kpi{background:var(--card);border-radius:12px;padding:16px;border-left:5px solid var(--red);box-shadow:0 1px 4px rgba(0,0,0,.07)}
.kpi .n{font-size:30px;font-weight:800}
.kpi .t{font-size:12px;color:var(--gray);text-transform:uppercase;letter-spacing:.5px;margin-top:4px}
.kpi.c-red{border-color:var(--red)} .kpi.c-orange{border-color:var(--orange)}
.kpi.c-blue{border-color:var(--blue)} .kpi.c-green{border-color:var(--green)}
.kpi.c-dark{border-color:var(--dark)} .kpi.c-gray{border-color:var(--gray)}
.panel{background:var(--card);border-radius:12px;padding:18px;margin-bottom:20px;box-shadow:0 1px 4px rgba(0,0,0,.07)}
.panel h2{font-size:16px;margin-bottom:14px;display:flex;justify-content:space-between;align-items:center;gap:10px;flex-wrap:wrap}
table{width:100%;border-collapse:collapse;font-size:13px}
th{text-align:left;padding:9px 8px;background:#fafafa;border-bottom:2px solid var(--line);font-size:11px;text-transform:uppercase;color:var(--gray);letter-spacing:.5px}
td{padding:9px 8px;border-bottom:1px solid var(--line);vertical-align:top}
tr:hover td{background:#fafafa}
.btn{display:inline-block;background:var(--red);color:#fff;border:none;border-radius:8px;padding:8px 14px;font-size:13px;cursor:pointer;text-decoration:none}
.btn:hover{background:var(--red-dark)}
.btn.sec{background:#3a3a3c}.btn.sec:hover{background:#2c2c2e}
.btn.sm{padding:4px 9px;font-size:12px;border-radius:6px}
.btn.ghost{background:#fff;color:var(--dark);border:1px solid var(--line)}.btn.ghost:hover{background:#f2f2f2}
input,select,textarea{padding:8px 10px;border:1px solid #cfcfd4;border-radius:8px;font-size:13px;width:100%;background:#fff;color:var(--dark)}
input:focus,select:focus,textarea:focus{outline:none;border-color:var(--red)}
.form-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:12px;margin-bottom:12px}
.form-grid label{font-size:11px;color:var(--gray);display:block;margin-bottom:4px;text-transform:uppercase;letter-spacing:.5px}
.form-grid .full{grid-column:1/-1}
.badge{display:inline-block;padding:3px 9px;border-radius:20px;font-size:11px;font-weight:600;color:#fff}
.b-scaduto{background:var(--red)} .b-scadenza{background:var(--orange)} .b-prog{background:var(--blue)}
.b-comp{background:var(--green)} .b-aperto{background:var(--red)} .b-lav{background:var(--orange)}
.b-ok{background:var(--green)} .b-bassa{background:var(--green)} .b-media{background:var(--orange)} .b-alta{background:var(--red)}
.searchbar{display:flex;gap:10px;margin-bottom:14px;flex-wrap:wrap}
.searchbar input,.searchbar select{max-width:280px}
.modal{position:fixed;inset:0;background:rgba(0,0,0,.5);display:none;align-items:center;justify-content:center;z-index:200;padding:16px}
.modal.open{display:flex}
.modal-box{background:#fff;border-radius:14px;padding:20px;width:100%;max-width:640px;max-height:90vh;overflow-y:auto}
.modal-box h3{margin-bottom:14px;font-size:17px}
.checklist-item{display:flex;gap:8px;margin-bottom:6px;align-items:center}
.checklist-item input[type=text]{flex:1}
.checklist-item input[type=checkbox]{width:auto}
.bar{height:8px;background:#eee;border-radius:6px;overflow:hidden;margin-top:6px}
.bar>div{height:100%;background:var(--red)}
.grid2{display:grid;grid-template-columns:1fr 1fr;gap:20px}
@media(max-width:900px){.grid2{grid-template-columns:1fr}}
@media(max-width:768px){
  aside{width:100%;position:fixed;transform:translateY(-100%);transition:.25s}
  aside.open{transform:translateY(0)}
  #burger{display:block;align-self:flex-end}
  main{margin-left:0;padding:14px;max-width:100%}
  .cards{grid-template-columns:repeat(2,1fr)}
  th:nth-child(4),td:nth-child(4){display:none}
}
/* CALENDARIO */
.cal-nav{display:flex;gap:8px;align-items:center;margin-bottom:14px;flex-wrap:wrap}
.cal-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:6px}
.cal-grid .dow{font-size:11px;text-align:center;color:var(--gray);text-transform:uppercase;font-weight:700;padding:4px 0}
.cal-cell{min-height:82px;border:1px solid var(--line);border-radius:8px;padding:5px;font-size:12px;cursor:pointer;background:#fff;overflow:hidden}
.cal-cell:hover{border-color:var(--red)}
.cal-cell.today{outline:2px solid var(--red)}
.cal-cell .dn{font-weight:700;margin-bottom:3px}
.cal-ev{border-radius:5px;padding:2px 5px;font-size:10px;color:#fff;margin-bottom:2px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.cal-week{display:grid;grid-template-columns:70px repeat(7,1fr);gap:6px}
.cal-week .hour{font-size:10px;color:var(--gray);text-align:right;padding-top:8px}
.cal-week .slot{border:1px solid var(--line);min-height:34px;border-radius:6px;padding:2px}
.stat-row{display:flex;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--line);font-size:13px}
.toast{position:fixed;bottom:20px;right:20px;background:var(--dark);color:#fff;padding:12px 18px;border-radius:10px;font-size:13px;display:none;z-index:300;border-left:4px solid var(--red)}
.empty{padding:24px;text-align:center;color:var(--gray);font-size:13px}
</style>
</head>
<body>
<div id="app">
<aside id="sidebar">
  <button id="burger" onclick="document.getElementById('sidebar').classList.toggle('open')">☰</button>
  <div class="logo">SPECTACLES<span>⚙</span><small>MAINTENANCE CMMS</small></div>
  <nav id="nav">
    <a href="#" data-v="dashboard" class="active"><span class="ic">📊</span>Dashboard</a>
    <a href="#" data-v="macchinari"><span class="ic">🏭</span>Macchinari</a>
    <a href="#" data-v="manutenzioni"><span class="ic">🛠</span>Manutenzioni</a>
    <a href="#" data-v="calendario"><span class="ic">📅</span>Calendario</a>
    <a href="#" data-v="guasti"><span class="ic">⚠</span>Guasti</a>
    <a href="#" data-v="magazzino"><span class="ic">📦</span>Magazzino</a>
    <a href="#" data-v="storico"><span class="ic">🗂</span>Storico & Report</a>
    <a href="#" data-v="dati"><span class="ic">💾</span>Dati & Backup</a>
  </nav>
</aside>
<main><header class="topbar"><h1 id="pageTitle">Dashboard</h1><span class="date" id="todayLbl"></span></header><div id="view"></div></main>
</div>
<div class="modal" id="modal"><div class="modal-box" id="modalBox"></div></div>
<div class="toast" id="toast"></div>

<script>
const K='spectacles_cmms_v1';
let DB=load();
function load(){try{const d=localStorage.getItem(K);if(d)return JSON.parse(d)}catch(e){}return seed()}
function save(){localStorage.setItem(K,JSON.stringify(DB))}
function uid(p){return p+'_'+Date.now().toString(36)+Math.random().toString(36).slice(2,6)}
function seed(){
 const today=new Date(), d=n=>{const x=new Date(today);x.setDate(x.getDate()+n);return x.toISOString().slice(0,10)};
 return {
  machines:[
   {id:'m1',code:'CNC-01',name:'CNC 01',dept:'Lavorazioni',brand:'Haas',model:'VF-2',loc:'Linea A',status:'Attivo',desc:'Centro di lavoro verticale',history:[]},
   {id:'m2',code:'CNC-02',name:'CNC 02',dept:'Lavorazioni',brand:'DMG Mori',model:'CTX 800',loc:'Linea A',status:'Attivo',desc:'Tornio CNC',history:[]},
   {id:'m3',code:'FRE-01',name:'Fresa 01',dept:'Officina',brand:'Lagun',model:'G-Cosmos',loc:'Officina 2',status:'Attivo',desc:'Fresa universale',history:[]},
   {id:'m4',code:'PRE-01',name:'Pressa 01',dept:'Stampaggio',brand:'OMERA',model:'OPI-420',loc:'Linea B',status:'Attivo',desc:'Pressa idraulica 420t',history:[]},
   {id:'m5',code:'COM-01',name:'Compressore 01',dept:'Utilities',brand:'Atlas Copco',model:'GA18',loc:'Locale compressori',status:'Attivo',desc:'Compressore a vite',history:[]},
   {id:'m6',code:'ASP-01',name:'Aspiratore industriale',dept:'Utilities',brand:'Fami',model:'ECO-4',loc:'Linea A',status:'Manutenzione',desc:'Impianto aspirazione trucioli',history:[]}
  ],
  maintenances:[
   {id:uid('mt'),machine:'m5',desc:'Controllo livello olio e filtro aspirazione',date:d(0),time:'08:00',freq:'Giornaliera',tech:'Mario Rossi',priority:'Media',eta:'15',notes:'',checklist:[{t:'Verificare livello olio',ok:false},{t:'Ispezionare filtro',ok:false}],status:'programmata',done:null},
   {id:uid('mt'),machine:'m1',desc:'Lubrificazione guide e viti',date:d(-3),time:'09:00',freq:'Settimanale',tech:'Luca Bianchi',priority:'Alta',eta:'45',notes:'',checklist:[{t:'Lubrificare guide',ok:false},{t:'Controllare viti a ricircolo',ok:false}],status:'scaduta',done:null},
   {id:uid('mt'),machine:'m4',desc:'Controllo impianto idraulico',date:d(5),time:'10:00',freq:'Mensile',tech:'Mario Rossi',priority:'Media',eta:'60',notes:'Verificare tenute',checklist:[{t:'Controllo tenute',ok:false},{t:'Prova pressione',ok:false}],status:'programmata',done:null},
   {id:uid('mt'),machine:'m6',desc:'Sostituzione filtro a cartuccia',date:d(0),time:'14:00',freq:'Mensile',tech:'Anna Verdi',priority:'Alta',eta:'30',notes:'',checklist:[{t:'Smontare filtro vecchio',ok:false},{t:'Montare nuovo filtro',ok:false}],status:'programmata',done:null},
   {id:uid('mt'),machine:'m2',desc:'Revisione mandrino',date:d(-12),time:'08:30',freq:'Semestrale',tech:'Luca Bianchi',priority:'Alta',eta:'180',notes:'',checklist:[{t:'Smontaggio',ok:true},{t:'Controllo cuscinetti',ok:true}],status:'scaduta',done:null},
   {id:uid('mt'),machine:'m3',desc:'Livellamento banco',date:d(-20),time:'11:00',freq:'Annuale',tech:'Anna Verdi',priority:'Bassa',eta:'90',notes:'',checklist:[{t:'Controllo livello',ok:true}],status:'completata',done:d(-20)}
  ],
  faults:[
   {id:uid('gf'),num:'INT-1001',machine:'m6',date:d(-2),desc:'Rumore anomalo ventilatore',priority:'Alta',tech:'Luca Bianchi',diag:'',work:'',parts:'',status:'in_lavorazione'},
   {id:uid('gf'),num:'INT-1002',machine:'m2',desc:'Perdita olio riduttore',priority:'Alta',tech:'',diag:'',work:'',parts:'',status:'aperto'}
  ],
  parts:[
   {id:uid('rp'),code:'RIC-001',name:'Filtro olio ISO 22',cat:'Filtri',qty:4,min:3,loc:'Scaffale A1',supplier:'SKF'},
   {id:uid('rp'),code:'RIC-002',name:'Cinghia trapezoidale SPB',cat:'Trasmissioni',qty:2,min:4,loc:'Scaffale B2',supplier:'Chiaravalli'},
   {id:uid('rp'),code:'RIC-003',name:'Cuscinetto 6205-2RS',cat:'Cuscinetti',qty:12,min:5,loc:'Scaffale A3',supplier:'FAG'},
   {id:uid('rp'),code:'RIC-004',name:'Guarnizione OR-120',cat:'Tenute',qty:8,min:6,loc:'Scaffale C1',supplier:'Eriks'}
  ],
  counters:{maint:0,fault:1002}
 };
}
function mById(id){return DB.machines.find(m=>m.id===id)}
function esc(s){return String(s==null?'':s).replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]))}
function toast(msg){const t=document.getElementById('toast');t.textContent=msg;t.style.display='block';setTimeout(()=>t.style.display='none',2500)}
function openModal(html){document.getElementById('modalBox').innerHTML=html;document.getElementById('modal').classList.add('open')}
function closeModal(){document.getElementById('modal').classList.remove('open')}
document.getElementById('modal').addEventListener('click',e=>{if(e.target.id==='modal')closeModal()});
function fmt(dt){return dt?(dt.split('-').reverse().join('/')):'—'}
function addDays(iso,n){const d=new Date(iso+'T00:00:00');d.setDate(d.getDate()+n);return d.toISOString().slice(0,10)}
function nextDate(date,freq){const map={'Giornaliera':1,'Settimanale':7,'Mensile':30,'Trimestrale':91,'Semestrale':182,'Annuale':365};return addDays(date,map[freq]||30)}
function mStatus(m){
 if(m.status==='completata')return['completata','Completata','b-comp'];
 const today=new Date().toISOString().slice(0,10);
 if(m.date<today)return['scaduta','Scaduta','b-scaduto'];
 if(m.date===today)return['in_scadenza','Oggi','b-scadenza'];
 const soon=addDays(today,3);
 if(m.date<=soon)return['in_scadenza','In scadenza','b-scadenza'];
 return['programmata','Programmata','b-prog'];
}
const titles={dashboard:'Dashboard',macchinari:'Macchinari',manutenzioni:'Manutenzioni Programmate',calendario:'Calendario',guasti:'Gestione Guasti',magazzino:'Magazzino Ricambi',storico:'Storico & Report',dati:'Dati & Backup'};
let CUR={v:'dashboard',date:new Date().toISOString().slice(0,10),mode:'month'};
document.getElementById('todayLbl').textContent=new Date().toLocaleDateString('it-IT',{weekday:'long',day:'numeric',month:'long',year:'numeric'});
document.getElementById('nav').addEventListener('click',e=>{
 const a=e.target.closest('a');if(!a)return;e.preventDefault();
 document.querySelectorAll('#nav a').forEach(x=>x.classList.remove('active'));a.classList.add('active');
 CUR.v=a.dataset.v;document.getElementById('sidebar').classList.remove('open');render();
});
/* ---------- VIEWS ---------- */
function render(){
 document.getElementById('pageTitle').textContent=titles[CUR.v];
 const v=document.getElementById('view');
 ({dashboard:vDash,macchinari:vMachines,manutenzioni:vMaint,calendario:vCal,guasti:vFaults,magazzino:vParts,storico:vHist,dati:vData})[CUR.v](v);
}
function kpi(n,t,cls){return `<div class="kpi ${cls}"><div class="n">${n}</div><div class="t">${t}</div></div>`}
function vDash(v){
 const today=new Date().toISOString().slice(0,10);
 const ms=DB.maintenances, flt=DB.faults;
 const scad=ms.filter(m=>mStatus(m)[0]==='scaduta').length;
 const oggi=ms.filter(m=>m.date===today&&m.status!=='completata').length;
 const prog=ms.filter(m=>mStatus(m)[0]==='programmata'||mStatus(m)[0]==='in_scadenza').length;
 const comp=ms.filter(m=>m.status==='completata').length;
 const guastiA=flt.filter(f=>f.status!=='risolto').length;
 const low=DB.parts.filter(p=>p.qty<p.min).length;
 let last=ms.filter(m=>m.status==='completata').sort((a,b)=>(b.done||'').localeCompare(a.done||'')).slice(0,6);
 v.innerHTML=`
 <div class="cards">
  ${kpi(DB.machines.length,'Macchinari','c-dark')}
  ${kpi(oggi,'Da fare oggi','c-orange')}
  ${kpi(prog,'Programmate','c-blue')}
  ${kpi(scad,'Scadute','c-red')}
  ${kpi(guastiA,'Guasti aperti','c-red')}
  ${kpi(comp,'Interventi completati','c-green')}
 </div>
 <div class="grid2">
 <div class="panel"><h2>Ultimi lavori effettuati</h2>
  ${last.length?`<table><tr><th>Data</th><th>Macchina</th><th>Descrizione</th><th>Tecnico</th></tr>${last.map(m=>`<tr><td>${fmt(m.done||m.date)}</td><td>${esc(mById(m.machine)?.name||'?')}</td><td>${esc(m.desc)}</td><td>${esc(m.tech)}</td></tr>`).join('')}</table>`:'<div class="empty">Nessun intervento completato</div>'}
 </div>
 <div class="panel"><h2>Panoramica guasti <span class="badge b-aperto">${guastiA} aperti</span></h2>
  ${flt.length?`<table><tr><th>N°</th><th>Macchina</th><th>Problema</th><th>Stato</th></tr>${flt.slice(0,6).map(f=>`<tr><td>${f.num}</td><td>${esc(mById(f.machine)?.name||'?')}</td><td>${esc(f.desc)}</td><td>${badgeFault(f.status)}</td></tr>`).join('')}</table>`:'<div class="empty">Nessun guasto registrato</div>'}
 </div></div>
 <div class="panel"><h2>Scorte sotto il minimo</h2>${low?`<table><tr><th>Codice</th><th>Nome</th><th>Qtà</th><th>Minimo</th><th>Fornitore</th></tr>${DB.parts.filter(p=>p.qty<p.min).map(p=>`<tr><td>${esc(p.code)}</td><td>${esc(p.name)}</td><td><b style="color:var(--red)">${p.qty}</b></td><td>${p.min}</td><td>${esc(p.supplier)}</td></tr>`).join('')}</table>`:'<div class="empty">✓ Tutte le scorte sono a posto</div>'}</div>`;
}
function badgeFault(s){return {aperto:'<span class="badge b-aperto">Aperto</span>',in_lavorazione:'<span class="badge b-lav">In lavorazione</span>',risolto:'<span class="badge b-ok">Risolto</span>'}[s]||s}
function badgePri(p){return {Bassa:'<span class="badge b-bassa">Bassa</span>',Media:'<span class="badge b-media">Media</span>',Alta:'<span class="badge b-alta">Alta</span>'}[p]||esc(p)}
</script>
<script>
/* ---------- MACCHINARI ---------- */
function vMachines(v,filter){
 const q=(filter||'').toLowerCase();
 const list=DB.machines.filter(m=>!q||[m.code,m.name,m.dept,m.brand,m.loc].join(' ').toLowerCase().includes(q));
 v.innerHTML=`
 <div class="searchbar">
  <input id="mq" placeholder="🔍 Cerca macchina (codice, nome, reparto...)" value="${esc(filter||'')}" oninput="vMachines(document.getElementById('view'),this.value)">
  <button class="btn" onclick="machineForm()">+ Aggiungi macchinario</button>
 </div>
 <div class="panel"><table><tr><th>Codice</th><th>Nome</th><th>Reparto</th><th>Marca/Modello</th><th>Posizione</th><th>Stato</th><th></th></tr>
 ${list.map(m=>`<tr><td><b>${esc(m.code)}</b></td><td>${esc(m.name)}</td><td>${esc(m.dept)}</td><td>${esc(m.brand)} ${esc(m.model)}</td><td>${esc(m.loc)}</td><td>${m.status==='Attivo'?'<span class="badge b-ok">Attivo</span>':'<span class="badge b-lav">'+esc(m.status)+'</span>'}</td>
 <td style="white-space:nowrap"><button class="btn sm ghost" onclick="machineForm('${m.id}')">✏</button> <button class="btn sm sec" onclick="delMachine('${m.id}')">🗑</button></td></tr>`).join('')||'<tr><td colspan="7" class="empty">Nessun macchinario trovato</td></tr>'}
 </table></div>`;
}
function machineForm(id){
 const m=id?mById(id):{code:'',name:'',dept:'',brand:'',model:'',loc:'',status:'Attivo',desc:''};
 openModal(`<h3>${id?'Modifica':'Nuovo'} macchinario</h3>
 <div class="form-grid">
  <div><label>Codice *</label><input id="f_code" value="${esc(m.code)}"></div>
  <div><label>Nome *</label><input id="f_name" value="${esc(m.name)}"></div>
  <div><label>Reparto</label><input id="f_dept" value="${esc(m.dept)}"></div>
  <div><label>Marca</label><input id="f_brand" value="${esc(m.brand)}"></div>
  <div><label>Modello</label><input id="f_model" value="${esc(m.model)}"></div>
  <div><label>Posizione</label><input id="f_loc" value="${esc(m.loc)}"></div>
  <div><label>Stato</label><select id="f_status">${['Attivo','Manutenzione','Fermo'].map(s=>`<option ${m.status===s?'selected':''}>${s}</option>`).join('')}</select></div>
  <div class="full"><label>Descrizione</label><textarea id="f_desc" rows="2">${esc(m.desc)}</textarea></div>
 </div>
 <button class="btn" onclick="saveMachine('${id||''}')">Salva</button> <button class="btn ghost" onclick="closeModal()">Annulla</button>`);
}
function saveMachine(id){
 const g=x=>document.getElementById(x).value.trim();
 const data={code:g('f_code'),name:g('f_name'),dept:g('f_dept'),brand:g('f_brand'),model:g('f_model'),loc:g('f_loc'),status:document.getElementById('f_status').value,desc:g('f_desc')};
 if(!data.code||!data.name)return toast('Codice e nome sono obbligatori');
 if(id){Object.assign(mById(id),data)}else{data.id=uid('m');data.history=[];DB.machines.push(data)}
 save();closeModal();toast('Macchinario salvato ✓');vMachines(document.getElementById('view'));
}
function delMachine(id){
 if(!confirm('Eliminare questo macchinario? Le manutenzioni collegate verranno rimosse.'))return;
 DB.machines=DB.machines.filter(m=>m.id!==id);
 DB.maintenances=DB.maintenances.filter(m=>m.machine!==id);
 DB.faults=DB.faults.filter(f=>f.machine!==id);
 save();toast('Macchinario eliminato');vMachines(document.getElementById('view'));
}
</script>
<script>
/* ---------- MANUTENZIONI ---------- */
function vMaint(v){
 const ms=[...DB.maintenances].sort((a,b)=>(a.date+a.time).localeCompare(b.date+b.time));
 v.innerHTML=`
 <div class="searchbar">
  <button class="btn" onclick="maintForm()">+ Nuova manutenzione</button>
 </div>
 <div class="panel"><table><tr><th>Data/Ora</th><th>Macchina</th><th>Descrizione</th><th>Frequenza</th><th>Tecnico</th><th>Priorità</th><th>Stato</th><th></th></tr>
 ${ms.map(m=>{const st=mStatus(m);return `<tr><td>${fmt(m.date)}<br><small>${esc(m.time)}</small></td><td>${esc(mById(m.machine)?.name||'?')}</td><td>${esc(m.desc)}</td><td>${esc(m.freq)}</td><td>${esc(m.tech)}</td><td>${badgePri(m.priority)}</td><td><span class="badge ${st[2]}">${st[1]}</span></td>
 <td style="white-space:nowrap"><button class="btn sm ghost" onclick="maintForm('${m.id}')">✏</button> ${m.status!=='completata'?`<button class="btn sm" onclick="completeMaint('${m.id}')">✓ Completa</button>`:''} <button class="btn sm sec" onclick="delMaint('${m.id}')">🗑</button></td></tr>`}).join('')||'<tr><td colspan="8" class="empty">Nessuna manutenzione pianificata</td></tr>'}
 </table></div>`;
}
function maintForm(id){
 const m=id?DB.maintenances.find(x=>x.id===id):{machine:'',desc:'',date:new Date().toISOString().slice(0,10),time:'08:00',freq:'Mensile',tech:'',priority:'Media',eta:'',notes:'',checklist:[]};
 openModal(`<h3>${id?'Modifica':'Nuova'} manutenzione programmata</h3>
 <div class="form-grid">
  <div><label>Macchinario *</label><select id="f_machine">${DB.machines.map(x=>`<option value="${x.id}" ${m.machine===x.id?'selected':''}>${esc(x.code)} – ${esc(x.name)}</option>`).join('')}</select></div>
  <div><label>Data *</label><input id="f_date" type="date" value="${m.date}"></div>
  <div><label>Ora</label><input id="f_time" type="time" value="${m.time}"></div>
  <div><label>Frequenza</label><select id="f_freq">${['Giornaliera','Settimanale','Mensile','Trimestrale','Semestrale','Annuale'].map(f=>`<option ${m.freq===f?'selected':''}>${f}</option>`).join('')}</select></div>
  <div><label>Manutentore</label><input id="f_tech" value="${esc(m.tech)}" placeholder="Nome e cognome"></div>
  <div><label>Priorità</label><select id="f_priority">${['Bassa','Media','Alta'].map(p=>`<option ${m.priority===p?'selected':''}>${p}</option>`).join('')}</select></div>
  <div><label>Tempo previsto (min)</label><input id="f_eta" type="number" value="${esc(m.eta)}"></div>
  <div class="full"><label>Descrizione lavoro *</label><input id="f_desc" value="${esc(m.desc)}"></div>
  <div class="full"><label>Note</label><textarea id="f_notes" rows="2">${esc(m.notes)}</textarea></div>
  <div class="full"><label>Checklist operazioni</label><div id="cl">${m.checklist.map(c=>clItem(c.t)).join('')}</div>
   <button class="btn sm ghost" onclick="document.getElementById('cl').insertAdjacentHTML('beforeend',clItem(''))">+ Aggiungi voce</button></div>
 </div>
 <button class="btn" onclick="saveMaint('${id||''}')">Salva</button> <button class="btn ghost" onclick="closeModal()">Annulla</button>`);
}
function clItem(t){return `<div class="checklist-item"><input type="text" value="${esc(t)}" placeholder="Operazione..."><button class="btn sm sec" onclick="this.parentElement.remove()">✕</button></div>`}
function saveMaint(id){
 const g=x=>document.getElementById(x).value.trim();
 const checklist=[...document.querySelectorAll('#cl input[type=text]')].map(i=>({t:i.value.trim(),ok:false})).filter(c=>c.t);
 const data={machine:document.getElementById('f_machine').value,date:g('f_date'),time:g('f_time'),freq:document.getElementById('f_freq').value,tech:g('f_tech'),priority:document.getElementById('f_priority').value,eta:g('f_eta'),desc:g('f_desc'),notes:g('f_notes'),checklist};
 if(!data.desc||!data.date)return toast('Descrizione e data sono obbligatorie');
 if(id){Object.assign(DB.maintenances.find(x=>x.id===id),data)}else{data.id=uid('mt');data.status='programmata';data.done=null;DB.maintenances.push(data)}
 save();closeModal();toast('Manutenzione salvata ✓');render();
}
function delMaint(id){
 if(!confirm('Eliminare questa manutenzione?'))return;
 DB.maintenances=DB.maintenances.filter(m=>m.id!==id);
 save();toast('Eliminata');render();
}
function completeMaint(id){
 const m=DB.maintenances.find(x=>x.id===id);
 openModal(`<h3>Completa: ${esc(m.desc)}</h3>
 <div class="form-grid">
 <div class="full"><label>Checklist – spunta le operazioni eseguite</label>
 ${m.checklist.length?m.checklist.map((c,i)=>`<div class="checklist-item"><input type="checkbox" id="ck${i}" ${c.ok?'checked':''}><input type="text" value="${esc(c.t)}" id="ct${i}"></div>`).join(''):'<div class="empty">Nessuna checklist</div>'}
 </div>
 <div class="full"><label>Note di chiusura</label><textarea id="f_cnote" rows="2">${esc(m.notes)}</textarea></div>
 </div>
 <button class="btn" onclick="doComplete('${id}')">✓ Conferma completamento</button> <button class="btn ghost" onclick="closeModal()">Annulla</button>`);
}
function doComplete(id){
 const m=DB.maintenances.find(x=>x.id===id);
 const today=new Date().toISOString().slice(0,10);
 m.checklist=m.checklist.map((c,i)=>({t:(document.getElementById('ct'+i)?.value||c.t),ok:document.getElementById('ck'+i)?.checked||false}));
 m.notes=document.getElementById('f_cnote').value;
 m.status='completata';m.done=today;
 DB.counters.maint++;
 mById(m.machine)?.history.push({date:today,desc:m.desc,tech:m.tech});
 save();closeModal();toast('Manutenzione completata ✓');
 // rigenera la prossima scadenza per manutenzioni periodiche
 if(m.freq!=='Giornaliera'||confirm('Frequenza '+m.freq+' — generare la prossima scadenza?')){
  DB.maintenances.push({...m,id:uid('mt'),date:nextDate(m.date,m.freq),checklist:m.checklist.map(c=>({t:c.t,ok:false})),status:'programmata',done:null,notes:m.notes});
  save();toast('Prossima scadenza: '+fmt(nextDate(m.date,m.freq)));
 }
 render();
}
</script>
<script>
/* ---------- CALENDARIO ---------- */
function evColor(m){const s=mStatus(m)[0];return s==='scaduta'?'#d62828':s==='in_scadenza'?'#f59e0b':s==='completata'?'#16a34a':'#2563eb'}
function vCal(v){
 const d=new Date(CUR.date+'T00:00:00');
 const label=d.toLocaleDateString('it-IT',{month:'long',year:'numeric'});
 let body='';
 if(CUR.mode==='month'){
  const first=new Date(d.getFullYear(),d.getMonth(),1);
  const start=(first.getDay()+6)%7; // lun=0
  const days=new Date(d.getFullYear(),d.getMonth()+1,0).getDate();
  const today=new Date().toISOString().slice(0,10);
  body='<div class="cal-grid">'+['Lun','Mar','Mer','Gio','Ven','Sab','Dom'].map(x=>`<div class="dow">${x}</div>`).join('');
  for(let i=0;i<start;i++)body+='<div></div>';
  for(let day=1;day<=days;day++){
   const iso=`${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,'0')}-${String(day).padStart(2,'0')}`;
   const evs=DB.maintenances.filter(m=>m.date===iso).slice(0,3);
   body+=`<div class="cal-cell ${iso===today?'today':''}" onclick="CUR.date='${iso}';CUR.mode='day';render()">
    <div class="dn">${day}</div>${evs.map(m=>`<div class="cal-ev" style="background:${evColor(m)}">${esc(m.time)} ${esc(m.desc.slice(0,18))}</div>`).join('')}</div>`;
  }
  body+='</div>';
 }else if(CUR.mode==='week'){
  const dow=(d.getDay()+6)%7; const mon=addDays(CUR.date,-dow);
  const hours=[6,7,8,9,10,11,12,13,14,15,16,17,18];
  body='<div class="cal-week"><div></div>'+[0,1,2,3,4,5,6].map(i=>{const dt=addDays(mon,i);const dd=new Date(dt+'T00:00:00');return `<div class="dow">${dd.toLocaleDateString('it-IT',{weekday:'short'})} ${dd.getDate()}</div>`}).join('');
  hours.forEach(h=>{
   body+=`<div class="hour">${String(h).padStart(2,'0')}:00</div>`;
   [0,1,2,3,4,5,6].forEach(i=>{
    const dt=addDays(mon,i);
    const evs=DB.maintenances.filter(m=>m.date===dt&&parseInt(m.time)===h);
    body+=`<div class="slot">${evs.map(m=>`<div class="cal-ev" style="background:${evColor(m)}" onclick="maintForm('${m.id}')">${esc(m.desc.slice(0,20))}</div>`).join('')}</div>`;
   });
  });
  body+='</div>';
 }else{
  const today=new Date().toISOString().slice(0,10);
  const evs=DB.maintenances.filter(m=>m.date===CUR.date);
  body=`<div class="panel"><h2>${d.toLocaleDateString('it-IT',{weekday:'long',day:'numeric',month:'long'})}</h2>
  ${evs.length?`<table><tr><th>Ora</th><th>Macchina</th><th>Descrizione</th><th>Tecnico</th><th>Priorità</th><th>Stato</th><th></th></tr>${evs.map(m=>{const st=mStatus(m);return `<tr><td>${esc(m.time)}</td><td>${esc(mById(m.machine)?.name||'?')}</td><td>${esc(m.desc)}</td><td>${esc(m.tech)}</td><td>${badgePri(m.priority)}</td><td><span class="badge ${st[2]}">${st[1]}</span></td><td>${m.status!=='completata'?`<button class="btn sm" onclick="completeMaint('${m.id}')">✓ Completa</button>`:''}</td></tr>`}).join('')}</table>`:'<div class="empty">Nessuna manutenzione prevista in questa data</div>'}
  </div>
  <div class="panel"><h2>Guasti in questa data</h2>${DB.faults.filter(f=>f.date===CUR.date).map(f=>`<div class="stat-row"><span><b>${f.num}</b> – ${esc(mById(f.machine)?.name||'?')} – ${esc(f.desc)}</span>${badgeFault(f.status)}</div>`).join('')||'<div class="empty">Nessun guasto</div>'}</div>`;
 }
 v.innerHTML=`
 <div class="cal-nav">
  <button class="btn ghost sm" onclick="shiftCal(-1)">←</button>
  <button class="btn ghost sm" onclick="CUR.date='${new Date().toISOString().slice(0,10)}';render()">Oggi</button>
  <button class="btn ghost sm" onclick="shiftCal(1)">→</button>
  <b style="text-transform:capitalize">${CUR.mode==='day'?'':label}</b>
  <span style="flex:1"></span>
  ${['day','week','month'].map(m=>`<button class="btn sm ${CUR.mode===m?'':'ghost'}" onclick="CUR.mode='${m}';render()">${{day:'Giornaliera',week:'Settimanale',month:'Mensile'}[m]}</button>`).join('')}
 </div>
 <div class="panel">${body}</div>
 <div style="font-size:12px;color:var(--gray)">Legenda: <span class="badge b-scaduto">Scaduta</span> <span class="badge b-scadenza">In scadenza</span> <span class="badge b-prog">Programmata</span> <span class="badge b-comp">Completata</span></div>`;
}
function shiftCal(n){
 const d=new Date(CUR.date+'T00:00:00');
 if(CUR.mode==='month')d.setMonth(d.getMonth()+n);
 else if(CUR.mode==='week')d.setDate(d.getDate()+7*n);
 else d.setDate(d.getDate()+n);
 CUR.date=d.toISOString().slice(0,10);render();
}
</script>
<script>
/* ---------- GUASTI ---------- */
function vFaults(v){
 const fs=[...DB.faults].sort((a,b)=>b.num.localeCompare(a.num));
 v.innerHTML=`
 <div class="searchbar"><button class="btn" onclick="faultForm()">+ Registra guasto</button></div>
 <div class="panel"><table><tr><th>N° Intervento</th><th>Data</th><th>Macchina</th><th>Problema</th><th>Priorità</th><th>Tecnico</th><th>Stato</th><th></th></tr>
 ${fs.map(f=>`<tr><td><b>${esc(f.num)}</b></td><td>${fmt(f.date)}</td><td>${esc(mById(f.machine)?.name||'?')}</td><td>${esc(f.desc)}</td><td>${badgePri(f.priority)}</td><td>${esc(f.tech)||'—'}</td><td>${badgeFault(f.status)}</td>
 <td style="white-space:nowrap"><button class="btn sm ghost" onclick="faultForm('${f.id}')">✏</button> <button class="btn sm sec" onclick="delFault('${f.id}')">🗑</button></td></tr>`).join('')||'<tr><td colspan="8" class="empty">Nessun guasto registrato</td></tr>'}
 </table></div>`;
}
function faultForm(id){
 const f=id?DB.faults.find(x=>x.id===id):{machine:'',date:new Date().toISOString().slice(0,10),desc:'',priority:'Alta',tech:'',diag:'',work:'',parts:'',status:'aperto'};
 openModal(`<h3>${id?'Gestisci guasto':'Registra guasto'} <span style="color:var(--red)">${id?esc(f.num):'(n° automatico)'}</span></h3>
 <div class="form-grid">
  <div><label>Macchinario *</label><select id="f_machine">${DB.machines.map(x=>`<option value="${x.id}" ${f.machine===x.id?'selected':''}>${esc(x.code)} – ${esc(x.name)}</option>`).join('')}</select></div>
  <div><label>Data</label><input id="f_date" type="date" value="${f.date}"></div>
  <div><label>Priorità</label><select id="f_priority">${['Bassa','Media','Alta'].map(p=>`<option ${f.priority===p?'selected':''}>${p}</option>`).join('')}</select></div>
  <div><label>Manutentore</label><input id="f_tech" value="${esc(f.tech)}"></div>
  <div class="full"><label>Descrizione del problema *</label><textarea id="f_desc" rows="2">${esc(f.desc)}</textarea></div>
  <div class="full"><label>Diagnosi</label><textarea id="f_diag" rows="2">${esc(f.diag)}</textarea></div>
  <div class="full"><label>Lavoro eseguito</label><textarea id="f_work" rows="2">${esc(f.work)}</textarea></div>
  <div class="full"><label>Ricambi utilizzati</label><textarea id="f_parts" rows="2" placeholder="Es. RIC-003 × 2">${esc(f.parts)}</textarea></div>
  <div><label>Stato</label><select id="f_status">${[['aperto','Aperto'],['in_lavorazione','In lavorazione'],['risolto','Risolto']].map(([v,t])=>`<option value="${v}" ${f.status===v?'selected':''}>${t}</option>`).join('')}</select></div>
 </div>
 <button class="btn" onclick="saveFault('${id||''}')">Salva</button> <button class="btn ghost" onclick="closeModal()">Annulla</button>`);
}
function saveFault(id){
 const g=x=>document.getElementById(x).value.trim();
 const data={machine:document.getElementById('f_machine').value,date:g('f_date'),priority:document.getElementById('f_priority').value,tech:g('f_tech'),desc:g('f_desc'),diag:g('f_diag'),work:g('f_work'),parts:g('f_parts'),status:document.getElementById('f_status').value};
 if(!data.desc)return toast('Descrizione del problema obbligatoria');
 if(id){Object.assign(DB.faults.find(x=>x.id===id),data)}else{
  DB.counters.fault++;data.id=uid('gf');data.num='INT-'+DB.counters.fault;DB.faults.push(data);
  toast('Guasto registrato: '+data.num);
 }
 save();closeModal();if(!id)toast('Salvato ✓');render();
}
function delFault(id){
 if(!confirm('Eliminare questo intervento?'))return;
 DB.faults=DB.faults.filter(f=>f.id!==id);save();toast('Eliminato');render();
}
/* ---------- MAGAZZINO ---------- */
function vParts(v){
 const low=p=>p.qty<p.min;
 v.innerHTML=`
 <div class="searchbar"><button class="btn" onclick="partForm()">+ Aggiungi ricambio</button></div>
 <div class="panel"><table><tr><th>Codice</th><th>Nome</th><th>Categoria</th><th>Qtà</th><th>Minimo</th><th>Posizione</th><th>Fornitore</th><th></th></tr>
 ${DB.parts.map(p=>`<tr><td><b>${esc(p.code)}</b></td><td>${esc(p.name)} ${low(p)?'<span class="badge b-scaduto">Sotto scorta!</span>':''}</td><td>${esc(p.cat)}</td><td>${low(p)?`<b style="color:var(--red)">${p.qty}</b>`:p.qty}</td><td>${p.min}</td><td>${esc(p.loc)}</td><td>${esc(p.supplier)}</td>
 <td style="white-space:nowrap"><button class="btn sm ghost" onclick="partForm('${p.id}')">✏</button> <button class="btn sm sec" onclick="delPart('${p.id}')">🗑</button></td></tr>`).join('')||'<tr><td colspan="8" class="empty">Magazzino vuoto</td></tr>'}
 </table></div>`;
}
function partForm(id){
 const p=id?DB.parts.find(x=>x.id===id):{code:'',name:'',cat:'',qty:0,min:0,loc:'',supplier:''};
 openModal(`<h3>${id?'Modifica':'Nuovo'} ricambio</h3><div class="form-grid">
 <div><label>Codice *</label><input id="f_code" value="${esc(p.code)}"></div>
 <div><label>Nome *</label><input id="f_name" value="${esc(p.name)}"></div>
 <div><label>Categoria</label><input id="f_cat" value="${esc(p.cat)}"></div>
 <div><label>Quantità</label><input id="f_qty" type="number" value="${p.qty}"></div>
 <div><label>Scorta minima</label><input id="f_min" type="number" value="${p.min}"></div>
 <div><label>Posizione</label><input id="f_loc" value="${esc(p.loc)}"></div>
 <div><label>Fornitore</label><input id="f_sup" value="${esc(p.supplier)}"></div></div>
 <button class="btn" onclick="savePart('${id||''}')">Salva</button> <button class="btn ghost" onclick="closeModal()">Annulla</button>`);
}
function savePart(id){
 const g=x=>document.getElementById(x).value.trim();
 const data={code:g('f_code'),name:g('f_name'),cat:g('f_cat'),qty:+g('f_qty')||0,min:+g('f_min')||0,loc:g('f_loc'),supplier:g('f_sup')};
 if(!data.code||!data.name)return toast('Codice e nome obbligatori');
 if(id){Object.assign(DB.parts.find(x=>x.id===id),data)}else{data.id=uid('rp');DB.parts.push(data)}
 save();closeModal();toast('Ricambio salvato ✓');render();
}
function delPart(id){
 if(!confirm('Eliminare questo ricambio?'))return;
 DB.parts=DB.parts.filter(p=>p.id!==id);save();toast('Eliminato');render();
}
</script>
<script>
/* ---------- STORICO & REPORT ---------- */
let HIST={machine:'',from:'',to:'',tech:'',type:'tutte',status:'tutti'};
function vHist(v){
 let rows=[];
 DB.maintenances.filter(m=>m.status==='completata').forEach(m=>rows.push({date:m.done||m.date,machine:mById(m.machine)?.name||'?',desc:m.desc,tech:m.tech,type:'Manutenzione '+m.freq,status:'completata',ref:m.id}));
 DB.faults.forEach(f=>rows.push({date:f.date,machine:mById(f.machine)?.name||'?',desc:f.desc,tech:f.tech||'—',type:'Guasto '+f.num,status:f.status,ref:f.id}));
 rows=rows.filter(r=>
  (!HIST.machine||r.machine.toLowerCase().includes(HIST.machine.toLowerCase()))&&
  (!HIST.from||r.date>=HIST.from)&&(!HIST.to||r.date<=HIST.to)&&
  (!HIST.tech||r.tech.toLowerCase().includes(HIST.tech.toLowerCase()))&&
  (HIST.type==='tutte'||r.type.toLowerCase().startsWith(HIST.type))&&
  (HIST.status==='tutti'||r.status===HIST.status)
 ).sort((a,b)=>b.date.localeCompare(a.date));
 const techs=[...new Set([...DB.maintenances.map(m=>m.tech),...DB.faults.map(f=>f.tech)].filter(Boolean))];
 const compM=DB.maintenances.filter(m=>m.status==='completata').length;
 const openF=DB.faults.filter(f=>f.status!=='risolto').length;
 const resF=DB.faults.filter(f=>f.status==='risolto').length;
 v.innerHTML=`
 <div class="grid2">
  <div class="panel"><h2>Statistiche manutenzioni</h2>
   <div class="stat-row"><span>Completate</span><b>${compM}</b></div>
   <div class="stat-row"><span>Scadute</span><b style="color:var(--red)">${DB.maintenances.filter(m=>mStatus(m)[0]==='scaduta').length}</b></div>
   <div class="stat-row"><span>Programmate / in scadenza</span><b style="color:var(--blue)">${DB.maintenances.filter(m=>mStatus(m)[0]!=='scaduta'&&m.status!=='completata').length}</b></div>
   <div class="stat-row"><span>Tempo totale stimato (min)</span><b>${DB.maintenances.filter(m=>m.status==='completata').reduce((s,m)=>s+(+m.eta||0),0)}</b></div>
  </div>
  <div class="panel"><h2>Statistiche guasti</h2>
   <div class="stat-row"><span>Aperti</span><b style="color:var(--red)">${openF}</b></div>
   <div class="stat-row"><span>Risolti</span><b style="color:var(--green)">${resF}</b></div>
   <div class="stat-row"><span>Tasso risoluzione</span><b>${DB.faults.length?Math.round(resF/DB.faults.length*100):0}%</b></div>
   <div class="stat-row"><span>Ricambi sotto scorta</span><b style="color:var(--orange)">${DB.parts.filter(p=>p.qty<p.min).length}</b></div>
  </div>
 </div>
 <div class="panel"><h2>Filtri</h2><div class="searchbar">
  <input placeholder="Macchinario" value="${esc(HIST.machine)}" oninput="HIST.machine=this.value;vHist(document.getElementById('view'))">
  <input type="date" value="${HIST.from}" onchange="HIST.from=this.value;vHist(document.getElementById('view'))" title="Dal">
  <input type="date" value="${HIST.to}" onchange="HIST.to=this.value;vHist(document.getElementById('view'))" title="Al">
  <select onchange="HIST.tech=this.value;vHist(document.getElementById('view'))"><option value="">Tecnico: tutti</option>${techs.map(t=>`<option ${HIST.tech===t?'selected':''}>${esc(t)}</option>`).join('')}</select>
  <select onchange="HIST.type=this.value;vHist(document.getElementById('view'))"><option value="tutte">Tipologia: tutte</option><option value="manutenzione" ${HIST.type==='manutenzione'?'selected':''}>Manutenzioni</option><option value="guasto" ${HIST.type==='guasto'?'selected':''}>Guasti</option></select>
  <select onchange="HIST.status=this.value;vHist(document.getElementById('view'))"><option value="tutti">Stato: tutti</option><option ${HIST.status==='completata'?'selected':''}>completata</option><option ${HIST.status==='risolto'?'selected':''}>risolto</option><option ${HIST.status==='aperto'?'selected':''}>aperto</option><option ${HIST.status==='in_lavorazione'?'selected':''}>in_lavorazione</option></select>
 </div>
 <table><tr><th>Data</th><th>Macchina</th><th>Descrizione</th><th>Tecnico</th><th>Tipologia</th><th>Stato</th></tr>
 ${rows.slice(0,300).map(r=>`<tr><td>${fmt(r.date)}</td><td>${esc(r.machine)}</td><td>${esc(r.desc)}</td><td>${esc(r.tech)}</td><td>${esc(r.type)}</td><td>${r.status==='completata'?'<span class="badge b-comp">Completata</span>':r.status==='risolto'?'<span class="badge b-ok">Risolto</span>':badgeFault(r.status)}</td></tr>`).join('')||'<tr><td colspan="6" class="empty">Nessun risultato con questi filtri</td></tr>'}
 </table></div>`;
}
/* ---------- DATI & BACKUP ---------- */
function vData(v){
 v.innerHTML=`
 <div class="grid2">
 <div class="panel"><h2>💾 Esporta backup</h2>
  <p style="font-size:13px;color:var(--gray);margin-bottom:12px">Scarica tutti i dati (macchinari, manutenzioni, guasti, ricambi) in formato JSON.</p>
  <button class="btn" onclick="exportJSON()">Esporta JSON</button>
 </div>
 <div class="panel"><h2>📥 Importa backup</h2>
  <p style="font-size:13px;color:var(--gray);margin-bottom:12px">Ripristina un file JSON esportato in precedenza. <b>I dati attuali verranno sostituiti.</b></p>
  <input type="file" id="impFile" accept=".json,application/json" style="margin-bottom:12px">
  <br><button class="btn" onclick="importJSON()">Importa e ripristina</button>
 </div>
 <div class="panel"><h2>⚠ Zona pericolosa</h2>
  <p style="font-size:13px;color:var(--gray);margin-bottom:12px">Elimina tutti i dati e ripristina quelli dimostrativi iniziali.</p>
  <button class="btn sec" onclick="resetAll()">Ripristina dati dimostrativi</button>
 </div>
 <div class="panel"><h2>ℹ Info</h2>
  <div class="stat-row"><span>Macchinari</span><b>${DB.machines.length}</b></div>
  <div class="stat-row"><span>Manutenzioni</span><b>${DB.maintenances.length}</b></div>
  <div class="stat-row"><span>Guasti</span><b>${DB.faults.length}</b></div>
  <div class="stat-row"><span>Ricambi</span><b>${DB.parts.length}</b></div>
  <div class="stat-row"><span>Salvataggio</span><b>LocalStorage ✓</b></div>
 </div></div>`;
}
function exportJSON(){
 const blob=new Blob([JSON.stringify(DB,null,2)],{type:'application/json'});
 const a=document.createElement('a');a.href=URL.createObjectURL(blob);
 a.download='spectacles_backup_'+new Date().toISOString().slice(0,10)+'.json';a.click();
 toast('Backup esportato ✓');
}
function importJSON(){
 const f=document.getElementById('impFile').files[0];
 if(!f)return toast('Seleziona prima un file JSON');
 const r=new FileReader();
 r.onload=()=>{try{
   const d=JSON.parse(r.result);
   if(!d.machines||!d.maintenzioni&&!d.maintenances)return toast('File non valido');
   d.maintenances=d.maintenances||[];d.faults=d.faults||[];d.parts=d.parts||[];d.counters=d.counters||{maint:0,fault:1000};
   DB=d;save();toast('Backup importato ✓');render();
  }catch(e){toast('Errore: file JSON non valido')}};
 r.readAsText(f);
}
function resetAll(){
 if(!confirm('Tutti i dati attuali verranno eliminati. Continuare?'))return;
 localStorage.removeItem(K);DB=seed();save();toast('Dati ripristinati');render();
}
render();
</script>
</body>
</html>