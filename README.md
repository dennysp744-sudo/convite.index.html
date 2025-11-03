<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Missão: Cinema — Denise & Geovane</title>

<link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap" rel="stylesheet">

<style>
  :root{
    --bg:#050505;
    --panel:#0b0b0b;
    --accent:#ffd24d;
    --muted:#bfbfbf;
    --maxw:480px;
  }
  *{box-sizing:border-box}
  html,body{height:100%;margin:0;background:var(--bg);font-family:'Press Start 2P',monospace;color:#fff;-webkit-font-smoothing:antialiased}
  .wrap{width:100%;min-height:100vh;display:flex;align-items:center;justify-content:center;padding:18px}
  .game{width:100%;max-width:var(--maxw);background:linear-gradient(180deg,#000 0%, #0a0a0a 100%);border:4px solid var(--accent);border-radius:12px;padding:16px;box-shadow:0 10px 30px rgba(0,0,0,.6);position:relative;overflow:hidden;}
  h1,h2,p{margin:8px 0;text-align:center} h1{font-size:13px;color:var(--accent)} h2{font-size:10px} p{font-size:9px;color:var(--muted);line-height:1.3}

  .start-screen{position:absolute;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center;background:linear-gradient(180deg,rgba(0,0,0,.6),rgba(0,0,0,.85));z-index:30;padding:18px;}
  .btn{background:var(--accent);color:#000;border:none;padding:10px 12px;border-radius:8px;cursor:pointer;font-size:10px;margin-top:12px;}
  .btn:active{transform:translateY(1px)}

  .stage{display:flex;flex-direction:column;align-items:center;justify-content:flex-start;min-height:380px;padding-top:8px}
  .pixel-area{width:100%;max-width:420px;flex:0 0 auto;display:flex;flex-direction:column;align-items:center}

  .character{width:56px;height:56px;margin:10px 0;filter: drop-shadow(0 4px 6px rgba(0,0,0,.6));transition:transform .2s ease;}

  .items{display:flex;gap:12px;justify-content:center;margin:8px 0}
  .item{width:58px;height:58px;border:2px solid rgba(255,255,255,.06);border-radius:8px;background:linear-gradient(180deg,#111,#0a0a0a);display:flex;align-items:center;justify-content:center;touch-action:manipulation;}
  .item img{width:44px;height:44px;cursor:pointer;user-select:none}
  .counter{font-size:10px;margin-top:6px;color:var(--muted)}

  .doors{display:flex;gap:10px;width:100%;padding:8px}
  .door-btn{flex:1;padding:10px;border-radius:8px;background:#111;border:2px solid rgba(255,255,255,.03);cursor:pointer;font-size:12px;}

  .hidden{display:none}

  .final-card{padding:12px;border-radius:10px;background:linear-gradient(180deg,#071018,#0b1622);border:2px solid rgba(255,210,77,.08);text-align:center;}
  .final-card p{font-size:10px;color:#ffd;}
  .accept-btn,.restart-btn{background:#ff6b6b;color:#fff;border:none;padding:10px 14px;border-radius:10px;cursor:pointer;margin-top:10px;font-size:12px}
  .restart-btn{background:#00bcd4}

  .hearts{position:absolute;inset:0;pointer-events:none;overflow:hidden;}
  .heart{position:absolute;width:18px;height:18px;opacity:0;transform:translateY(0) scale(.6);animation:floatUp linear forwards;}
  @keyframes floatUp{0%{opacity:0;transform:translateY(0) scale(.7)}10%{opacity:1}100%{opacity:0;transform:translateY(-220px) scale(1.1)}}

  .volume-container{display:flex;justify-content:center;align-items:center;margin-top:8px;font-size:10px;color:var(--muted)}
  .volume-container input[type=range]{-webkit-appearance:none;width:120px;height:6px;background:#111;border-radius:4px;margin-left:8px;cursor:pointer}
  .volume-container input[type=range]::-webkit-slider-thumb{-webkit-appearance:none;width:12px;height:12px;background:var(--accent);border-radius:50%;cursor:pointer;box-shadow:0 0 2px #fff}
  .volume-container input[type=range]::-moz-range-thumb{width:12px;height:12px;background:var(--accent);border-radius:50%;cursor:pointer}
</style>
</head>
<body>

<div class="wrap">
  <div class="game" role="application" aria-label="Missão Cinema — Denise e Geovane">

    <div class="start-screen" id="start">
      <h1>MISSÃO: CINEMA</h1>
      <p>Complete as fases e desbloqueie o convite secreto.</p>
      <p>Estilo: retrô • Efeitos sonoros ativados</p>
      <button class="btn" id="startBtn">INICIAR MISSÃO</button>
      <p style="font-size:9px;color:#9a9a9a;margin-top:12px">Toque em qualquer item/porta para interagir.</p>
    </div>

    <div class="stage" id="gameStage" aria-live="polite">
      <div style="display:flex;justify-content:space-between;align-items:center">
        <h2>Missão: Cinema</h2>
        <div style="font-size:9px;color:var(--muted)">Fases: 3</div>
      </div>

      <div class="pixel-area">
        <div id="characterWrap">
          <svg class="character" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg">
            <rect x="10" y="2" width="12" height="6" fill="#ffd24d"/>
            <rect x="11" y="4" width="3" height="2" fill="#000"/>
            <rect x="18" y="4" width="3" height="2" fill="#000"/>
            <rect x="9" y="8" width="14" height="10" fill="#ff6b6b"/>
            <rect x="9" y="18" width="5" height="8" fill="#333"/>
            <rect x="18" y="18" width="5" height="8" fill="#333"/>
            <rect x="5" y="10" width="4" height="3" fill="#ff6b6b"/>
            <rect x="23" y="10" width="4" height="3" fill="#ff6b6b"/>
          </svg>
        </div>

        <div id="fase1">
          <p>Fase 1 — A Pipoca Secreta</p>
          <p style="font-size:9px;color:var(--muted)">Toque para coletar: milho, manteiga e sal</p>
          <div class="items">
            <div class="item"><img src="https://cdn-icons-png.flaticon.com/512/992/992703.png" alt="Milho" onclick="collectItem(this)"></div>
            <div class="item"><img src="https://cdn-icons-png.flaticon.com/512/733/733935.png" alt="Manteiga" onclick="collectItem(this)"></div>
            <div class="item"><img src="https://cdn-icons-png.flaticon.com/512/1046/1046784.png" alt="Sal" onclick="collectItem(this)"></div>
          </div>
          <div class="counter" id="counter">Itens coletados: 0 / 3</div>
        </div>

        <div id="fase2" class="hidden">
          <p>Fase 2 — O Caminho Misterioso</p>
          <p style="font-size:9px;color:var(--muted)">Escolha a porta que leva ao cinema</p>
          <div class="doors">
            <button class="door-btn" onclick="doorChoice(false)">🚪 Porta 1</button>
            <button class="door-btn" onclick="doorChoice(true)">🚪 Porta 2</button>
            <button class="door-btn" onclick="doorChoice(false)">🚪 Porta 3</button>
          </div>
        </div>

        <div id="fase3" class="hidden">
          <p>Fase 3 — Encontre o ingresso</p>
          <p style="font-size:9px;color:var(--muted)">Toque no ingresso escondido na tela</p>
          <div style="position:relative;width:100%;height:160px;display:flex;align-items:center;justify-content:center">
            <img id="ticket" src="https://cdn-icons-png.flaticon.com/512/3112/3112946.png" style="width:70px;cursor:pointer" onclick="foundTicket()">
          </div>
        </div>

        <div id="final" class="hidden">
          <div class="final-card">
            <h2>🎬 MISSÃO CONCLUÍDA</h2>
            <p>Você desbloqueou o convite secreto</p>
            <p style="color:#ffd;">💛 Convite especial para o cinema 💛</p>
            <p style="font-size:9px;color:var(--muted)">Com amor,<br><strong>Denise e Geovane</strong></p>
            <button class="accept-btn" onclick="acceptInvite()">ACEITAR CONVITE</button>
            <button class="restart-btn" onclick="restartGame()">REINICIAR MISSÃO</button>
            <div class="volume-container">
              <span>Volume</span>
              <input type="range" id="volumeControl" min="0" max="1" step="0.05" value="1">
            </div>
          </div>
        </div>

      </div>
    </div>

    <div class="hearts" id="hearts"></div>

    <!-- Áudios -->
    <audio id="sCollect" preload="auto" src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_6dff331a22.mp3?filename=coin-7783.mp3"></audio>
    <audio id="sError" preload="auto" src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_2acb7e3265.mp3?filename=beep-126.mp3"></audio>
    <audio id="sSuccess" preload="auto" src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_cba6cc9efb.mp3?filename=success-1-6297.mp3"></audio>
    <audio id="sFinal" preload="auto" src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_25c5423e5f.mp3?filename=dramatic-011-7177.mp3"></audio>

  </div>
</div>

<script>
let collected=0;
const startScreen=document.getElementById('start');
const startBtn=document.getElementById('startBtn');
const fase1=document.getElementById('fase1');
const fase2=document.getElementById('fase2');
const fase3=document.getElementById('fase3');
const finalCard=document.getElementById('final');
const counter=document.getElementById('counter');
const heartsContainer=document.getElementById('hearts');
const volumeControl=document.getElementById('volumeControl');

const sCollect=document.getElementById('sCollect');
const sError=document.getElementById('sError');
const sSuccess=document.getElementById('sSuccess');
const sFinal=document.getElementById('sFinal');
let audioElements=[sCollect,sError,sSuccess,sFinal];

startBtn.addEventListener('click',()=>{
  startScreen.classList.add('hidden');
  playSound(sSuccess);
  showPhase(1);
});

volumeControl.addEventListener('input',()=>{
  audioElements.forEach(a=>a.volume=volumeControl.value);
});

function playSound(audioEl){
  try{audioEl.currentTime=0;audioEl.play().catch(()=>{});}catch(e){}
}

function collectItem(imgEl){
  if(imgEl.dataset.collected==='1')return;
  imgEl.dataset.collected='1';
  imgEl.style.transition='transform .28s ease, opacity .28s ease';
  imgEl.style.transform='scale(.6) translateY(-8px)';
  imgEl.style.opacity='0.08';
  collected++;
  counter.textContent=`Itens coletados: ${collected} / 3`;
  playSound(sCollect);
  if(collected>=3)setTimeout(()=>{playSound(sSuccess);showPhase(2);},520);
}

function doorChoice(correct){
  if(correct){playSound(sSuccess);setTimeout(()=>showPhase(3),450);}
  else{playSound(sError);const doors=document.querySelector('.doors');doors.style.transition='transform .12s';doors.style.transform='translateX(-8px)';setTimeout(()=>doors.style.transform='translateX(8px)',90);setTimeout(()=>doors.style.transform='translateX(0)',180);}
}

function foundTicket(){
  playSound(sSuccess);
  const ticket=document.getElementById('ticket');
  ticket.style.transition='transform .3s ease, opacity .3s';
  ticket.style.transform='scale(.7) rotate(-6deg)';
  ticket.style.opacity='0';
  setTimeout(()=>showFinal(),350);
}

function showPhase(n){
  fase1.classList.add('hidden'); fase2.classList.add('hidden'); fase3.classList.add('hidden'); finalCard.classList.add('hidden');
  if(n===1)fase1.classList.remove('hidden');
  if(n===2)fase2.classList.remove('hidden');
  if(n===3)fase3.classList.remove('hidden');
}

function showFinal(){fase1.classList.add('hidden');fase2.classList.add('hidden');fase3.classList.add('hidden');finalCard.classList.remove('hidden');playSound(sFinal);}

function acceptInvite(){playSound(sSuccess);spawnHearts(16);setTimeout(()=>alert('Convite aceito! Aproveitem a sessão 💛'),600);}

function restartGame(){collected=0;document.querySelectorAll('.item img').forEach(i=>{i.style.opacity='1';i.dataset.collected='0';i.style.transform='scale(1)'});showPhase(1);}

function spawnHearts(count){for(let i=0;i<count;i++){const el=document.createElement('div');el.className='heart';el.innerHTML='<svg viewBox="0 0 24 24" width="18" height="18"><path d="M12 21s-7-4.9-9.2-7.1C-0.2 9.6 3 5 6.4 5c1.6 0 3 .9 3.6 2.1C11.6 5.9 13 5 14.6 5c3.4 0 6.6 4.6 3.6 8.9C19 16.1 12 21 12 21z" fill="#ff6b6b"/></svg>';el.style.left=(Math.random()*80+10)+'%';el.style.animationDuration=(Math.random()*1.6+2.2).toFixed(2)+'s';heartsContainer.appendChild(el);el.addEventListener('animationend',()=>el.remove());}
}

showPhase(1);
</script>
</body>
</html>
