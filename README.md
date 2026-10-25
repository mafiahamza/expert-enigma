# expert-enigma
Mafia fun website with voting and reveals
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Mafia</title>
<meta name="description" content="A pass-the-phone Mafia game. Check your role, choose the victim, find the killers.">
<meta name="theme-color" content="#070606">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&family=Playfair+Display:wght@600;900&display=swap" rel="stylesheet">
<style>
:root{--bg:#070606;--panel:#130c0d;--line:#3b1a1e;--ink:#efe6d8;--mute:#9c8f86;--red:#a50f1c;--red2:#d1202e;--redt:#ff6b73;
--serif:"Playfair Display","Bodoni 72",Didot,"Hoefler Text",Georgia,serif;
--sans:Inter,"Helvetica Neue",Helvetica,Arial,system-ui,sans-serif;color-scheme:dark;
padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
*{box-sizing:border-box}
html{-webkit-text-size-adjust:100%;background:var(--bg)}
body{margin:0;color:var(--ink);font:17px/1.55 var(--sans);min-height:100vh;
background:radial-gradient(120% 55% at 50% -8%,#2b0a0f 0%,#0b0607 55%,#050404 100%) fixed}
[hidden]{display:none!important}
.wrap{max-width:520px;margin:0 auto;padding:22px 22px 56px}
.logo{display:flex;align-items:center;gap:16px;font:900 1.7rem/1 var(--serif);letter-spacing:.34em;padding-left:.34em;justify-content:center}
.logo::before,.logo::after{content:"";flex:1;height:1px;background:linear-gradient(90deg,transparent,var(--red2))}
.logo::after{transform:scaleX(-1)}
.orn{display:flex;align-items:center;gap:12px;color:var(--red2);margin:14px 0 30px;font-size:.8rem}
.orn::before,.orn::after{content:"";flex:1;height:1px;background:var(--line)}
h1{font:900 clamp(2.2rem,9.5vw,3rem)/1.06 var(--serif);margin:0 0 14px;letter-spacing:-.01em}
h2{font:600 1.15rem/1.3 var(--serif);margin:28px 0 10px}
p{margin:0 0 14px}
.sub{color:var(--mute)}
.ctr{text-align:center}
.stack{display:grid;gap:10px;margin-top:22px}
button{font:600 1rem var(--sans);letter-spacing:.02em;cursor:pointer;min-height:54px;padding:12px 18px;border-radius:3px;border:1px solid var(--line);background:var(--panel);color:var(--ink);text-align:center}
button:hover:not(:disabled){border-color:var(--red2)}
button:disabled{opacity:.35;cursor:not-allowed}
button.red{background:linear-gradient(#c3182a,#8d0c18);border-color:#e0404c;box-shadow:inset 0 0 0 1px rgba(255,225,205,.16)}
button.opt{text-align:left;font:600 1.1rem var(--serif);letter-spacing:0;display:flex;justify-content:space-between;align-items:center}
button.opt[aria-pressed="true"]{background:#4e0810;border-color:var(--red2)}
button.opt[aria-pressed="true"]::after{content:"\2713\FE0E";color:var(--redt)}
button.link{background:none;border:0;min-height:44px;color:var(--mute);text-decoration:underline;text-underline-offset:3px;font-weight:400}
:focus-visible{outline:3px solid var(--redt);outline-offset:2px}
.seg{display:flex;gap:8px}
.seg button{flex:1;padding:0;font:600 1.15rem var(--serif)}
.seg button[aria-pressed="true"]{background:var(--ink);color:#0a0606;border-color:var(--ink)}
.step{display:flex;align-items:center;gap:20px}
.step button{width:54px;padding:0;font-size:1.5rem}
.step b{font:900 1.9rem var(--serif);min-width:2ch;text-align:center}
textarea{width:100%;min-height:112px;background:var(--panel);color:var(--ink);border:1px solid var(--line);border-radius:3px;padding:12px 14px;font:inherit;resize:vertical}
.err{color:var(--redt);min-height:1.5em;margin:10px 0 0;font-weight:600}
.back{width:132px;height:188px;margin:4px auto 26px;border:1px solid var(--red);border-radius:8px;position:relative;display:grid;place-items:center;
background:repeating-linear-gradient(45deg,#1c0a0d 0 7px,#2a0d12 7px 14px);box-shadow:0 16px 36px rgba(0,0,0,.65)}
.back::before{content:"";position:absolute;inset:8px;border:1px solid rgba(209,32,46,.55);border-radius:4px}
.back span{width:68px;height:68px;border-radius:50%;display:grid;place-items:center;font-size:2.6rem;color:var(--red2);background:#12080a;border:1px solid var(--red);position:relative}
.card{position:relative;text-align:center;padding:50px 20px 44px;border-radius:5px;margin:8px 0 22px;border:1px solid}
.card::before{content:"";position:absolute;inset:8px;border:1px solid currentColor;opacity:.3;border-radius:2px}
.card i{position:absolute;font-style:normal;font-size:1.15rem}
.card .p1{top:16px;left:20px}.card .p2{bottom:16px;right:20px;transform:rotate(180deg)}
.card small{display:block;opacity:.8;letter-spacing:.1em;font-size:.82rem;margin-bottom:6px}
.card strong{display:block;font:900 3.2rem/1.05 var(--serif)}
.card.m{background:linear-gradient(#80091a,#47050d);color:#ffe9e5;border-color:#d1202e}
.card.c{background:#e9dfcd;color:#140d0d;border-color:#e9dfcd}
@media (prefers-reduced-motion:no-preference){.card{animation:rev .45s ease-out both}@keyframes rev{from{opacity:0;transform:translateY(10px) scale(.97)}}}
.tally{list-style:none;margin:0 0 18px;padding:0;border-top:1px solid var(--line);text-align:left}
.tally li{display:flex;justify-content:space-between;gap:12px;padding:10px 0;border-bottom:1px solid var(--line);font-family:var(--serif)}
.tally .tag{font:400 .9rem var(--sans);color:var(--mute)}
.tally .out span:first-child{text-decoration:line-through;color:var(--mute)}
.credit{margin-top:36px;font-size:.85rem;color:var(--mute);text-align:center}
</style>
</head>
<body>
<div class="wrap">
  <div class="logo">MAFIA</div>
  <div class="orn" aria-hidden="true"><span>&#9830;&#xFE0E;</span></div>
  <main id="app"></main>
  <div class="ctr"><button id="endbtn" class="link" hidden>End game</button></div>
  <p class="credit">Designed by Hamza Quraanye</p>
</div>
<script>
(function(){
const $=id=>document.getElementById(id),app=$('app');
const esc=s=>String(s).replace(/[&<>"]/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;'}[c]));
const SP='\u2660\uFE0E',DI='\u2666\uFE0E';
const S={mafia:2,civ:6,names:'',players:[],round:1,nq:[],nv:[],killed:0,vq:[],votes:{}};
function rnd(n){const m=Math.floor(4294967296/n)*n,a=new Uint32Array(1);do{crypto.getRandomValues(a)}while(a[0]>=m);return a[0]%n}
function shuffle(a){for(let i=a.length-1;i>0;i--){const j=rnd(i+1);[a[i],a[j]]=[a[j],a[i]]}return a}
const alive=f=>S.players.map((p,i)=>({p,i})).filter(x=>x.p.alive&&(!f||f(x.p)));
const card=(role,label)=>{const m=role==='Mafia',s=m?SP:DI;return `<div class="card ${m?'m':'c'}"><i class="p1">${s}</i><i class="p2">${s}</i><small>${label}</small><strong>${role}</strong></div>`};
const back=()=>`<div class="back"><span>${SP}</span></div>`;

function view(h,btns){
  app.innerHTML=h+'<div class="stack" id="b"></div>';
  (btns||[]).forEach(x=>{const e=document.createElement('button');e.textContent=x[0];e.className=x[2]||'';e.onclick=x[1];$('b').appendChild(e)});
  window.scrollTo(0,0);
}

/* setup */
function setup(){
  $('endbtn').hidden=true;
  app.innerHTML=`<h1>Everyone has a secret.</h1>
  <p class="sub">One phone. One table. Somebody in the room is lying.</p>
  <h2>Mafia</h2>
  <div class="seg">${[1,2,3,4,5].map(n=>`<button data-m="${n}" aria-pressed="${n===S.mafia}" aria-label="${n} mafia">${n}</button>`).join('')}</div>
  <h2>Civilians</h2>
  <div class="step"><button data-c="-1" aria-label="Fewer civilians">−</button><b>${S.civ}</b><button data-c="1" aria-label="More civilians">+</button></div>
  <h2><label for="names">Player names</label></h2>
  <p class="sub">Optional. One name per line.</p>
  <textarea id="names" spellcheck="false" autocomplete="off">${esc(S.names)}</textarea>
  <p class="err" id="err">${S.civ<=S.mafia?'You need more civilians than mafia.':''}</p>
  <div class="stack"><button class="red" id="go">Deal the roles</button></div>`;
  app.querySelectorAll('[data-m]').forEach(b=>b.onclick=()=>{S.mafia=+b.dataset.m;setup()});
  app.querySelectorAll('[data-c]').forEach(b=>b.onclick=()=>{S.civ=Math.min(25,Math.max(2,S.civ+ +b.dataset.c));setup()});
  $('names').oninput=e=>{S.names=e.target.value};
  $('go').onclick=()=>{
    if(S.civ<=S.mafia)return;
    const t=S.mafia+S.civ,nm=S.names.split('\n').map(s=>s.trim()).filter(Boolean);
    if(nm.length>t){$('err').textContent='You entered '+nm.length+' names for '+t+' players.';return}
    deal(nm);
  };
}
function deal(nm){
  nm=nm||S.names.split('\n').map(s=>s.trim()).filter(Boolean);
  const t=S.mafia+S.civ,r=shuffle(Array.from({length:t},(_,i)=>i<S.mafia?'Mafia':'Civilian'));
  S.players=r.map((role,i)=>({name:nm[i]||'Player '+(i+1),role,alive:true}));
  S.round=1;$('endbtn').hidden=false;nightStart();
}

/* night: the phone goes round the table, everyone sees their role, mafia choose a victim */
function nightStart(){
  S.nq=alive().map(x=>x.i);S.nv=[];
  view(`<div class="ctr"><p class="sub">Night ${S.round}</p><h1>The phone goes round the table.</h1>
    <p>Check your role in private. If you’re mafia, you’ll see your partners and choose tonight’s victim.</p></div>`,
    [['Begin the night',()=>nightGate(0),'red']]);
}
function nightGate(k){
  const p=S.players[S.nq[k]];
  view(`<div class="ctr"><p class="sub">Night ${S.round} · ${k+1} of ${S.nq.length}</p>${back()}<h1>Pass the phone to ${esc(p.name)}</h1>
    <p class="sub">Make sure only they can see the screen.</p></div>`,[['I’m '+p.name,()=>nightShow(k),'red']]);
}
function nightNext(k){k+1<S.nq.length?nightGate(k+1):nightEnd()}
function nightShow(k){
  const i=S.nq[k],p=S.players[i],last=k===S.nq.length-1,mf=p.role==='Mafia';
  const done=last?'Hide role and end the night':'Hide role and pass on';
  if(!mf){
    view(`<div class="ctr"><p class="sub">${esc(p.name)}</p>${card(p.role,'Your role')}<p class="sub">Keep it to yourself.</p></div>`,[[done,()=>nightNext(k),'red']]);
    return;
  }
  const mates=S.players.filter((q,j)=>q.role==='Mafia'&&j!==i&&q.alive).map(q=>esc(q.name));
  const seen=S.nv.map(v=>`<li><span>${esc(S.players[v.by].name)}</span><span class="tag">chose ${esc(S.players[v.t].name)}</span></li>`).join('');
  let sel=-1;
  app.innerHTML=`<div class="ctr"><p class="sub">${esc(p.name)}</p>${card(p.role,'Your role')}
    <p>${mates.length?'Your partners: <b>'+mates.join(', ')+'</b>':'You are the only mafia left.'}</p></div>
    ${seen?`<ul class="tally">${seen}</ul>`:''}
    <h2>Choose tonight’s victim</h2>
    <div class="stack" style="margin-top:0">${alive(q=>q.role!=='Mafia').map(x=>`<button class="opt" data-t="${x.i}" aria-pressed="false">${esc(x.p.name)}</button>`).join('')}</div>
    <div class="stack"><button class="red" id="ok" disabled>${done}</button></div>`;
  app.querySelectorAll('[data-t]').forEach(b=>b.onclick=()=>{
    sel=+b.dataset.t;app.querySelectorAll('[data-t]').forEach(o=>o.setAttribute('aria-pressed',String(o===b)));$('ok').disabled=false;
  });
  $('ok').onclick=()=>{S.nv.push({by:i,t:sel});nightNext(k)};
  window.scrollTo(0,0);
}
function nightEnd(){
  const c={};S.nv.forEach(v=>c[v.t]=(c[v.t]||0)+1);
  const top=Math.max(...Object.values(c)),tied=Object.keys(c).filter(t=>c[t]===top).map(Number);
  S.killed=tied[rnd(tied.length)];S.players[S.killed].alive=false;
  view(`<div class="ctr"><h1>The night is over.</h1><p class="sub">Everyone, open your eyes.</p></div>`,[['Start the day',morning,'red']]);
}
function morning(){
  const k=S.players[S.killed];
  view(`<div class="ctr"><p class="sub">Day ${S.round}</p><h1>${esc(k.name)} was found dead.</h1>${card(k.role,'They were')}</div>`,
    [['Continue',()=>checkWin(voteStart),'red']]);
}

/* day: tap to vote */
function voteStart(){S.vq=alive().map(x=>x.i);S.votes={};voteGate(0)}
function voteGate(k){
  const p=S.players[S.vq[k]];
  view(`<div class="ctr"><p class="sub">Day ${S.round} vote · ${k+1} of ${S.vq.length}</p>${back()}<h1>Pass the phone to ${esc(p.name)}</h1></div>`,
    [['I’m '+p.name,()=>votePick(k),'red']]);
}
function votePick(k){
  const me=S.vq[k];
  view(`<p class="sub">${esc(S.players[me].name)}</p><h1>Who do you vote out?</h1>`,
    alive().filter(x=>x.i!==me).map(x=>[x.p.name,()=>{S.votes[x.i]=(S.votes[x.i]||0)+1;k+1<S.vq.length?voteGate(k+1):voteResult()},'opt']));
}
function voteResult(){
  const e=Object.keys(S.votes).map(Number).sort((a,b)=>S.votes[b]-S.votes[a]);
  const tally=`<ul class="tally">${e.map(i=>`<li><span>${esc(S.players[i].name)}</span><b>${S.votes[i]}</b></li>`).join('')}</ul>`;
  const tied=e.filter(i=>S.votes[i]===S.votes[e[0]]);
  if(tied.length>1){view(`<div class="ctr"><h1>A tie.</h1><p class="sub">Nobody is voted out.</p></div>${tally}`,[['Continue to night',nextRound,'red']]);return}
  const o=S.players[e[0]];o.alive=false;
  view(`<div class="ctr"><h1>${esc(o.name)} was voted out.</h1>${card(o.role,'They were')}</div>${tally}`,[['Continue',()=>checkWin(nextRound),'red']]);
}
function nextRound(){S.round++;nightStart()}

/* end */
function checkWin(then){
  const m=alive(p=>p.role==='Mafia').length,c=alive().length-m;
  if(m===0)return end('The town wins.','Every mafia member has been found.');
  if(m>=c)return end('The mafia win.','They now match the town in number.');
  then();
}
function end(t,s){
  $('endbtn').hidden=true;
  view(`<div class="ctr"><h1>${t}</h1><p class="sub">${s}</p></div>
    <ul class="tally">${S.players.map(p=>`<li class="${p.alive?'':'out'}"><span>${esc(p.name)}</span><span class="tag">${p.role}</span></li>`).join('')}</ul>`,
    [['Play again',()=>deal(),'red'],['Change setup',setup]]);
}

let endT;
$('endbtn').onclick=()=>{
  const b=$('endbtn');
  if(b.dataset.arm){clearTimeout(endT);b.dataset.arm='';b.textContent='End game';setup();return}
  b.dataset.arm='1';b.textContent='Tap again to end the game';
  endT=setTimeout(()=>{b.dataset.arm='';b.textContent='End game'},4000);
};
setup();
})();
</script>
</body>
</html>
