<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Missão: Cinema — Denise</title>
<link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#050505;
  --accent:#ffd24d;
  --maxw:480px;
}
*{box-sizing:border-box;}
body,html{margin:0;padding:0;height:100%;font-family:'Press Start 2P', monospace;background:var(--bg);color:#fff;overflow:hidden;}
.wrap{display:flex;justify-content:center;align-items:center;width:100%;height:100%;}
.game{position:relative;width:100%;max-width:var(--maxw);background:#0a0a0a;border:4px solid var(--accent);border-radius:12px;padding:16px;overflow:hidden;}
h1,h2,p{margin:0;text-align:center;}
h1{font-size:14px;color:var(--accent);}
p{font-size:9px;color:#bbb;line-height:1.3;}

.start-screen, .final-card, .transition{position:absolute;inset:0;display:flex;flex-direction:column;justify-content:center;align-items:center;z-index:30;}
.start-screen{background:rgba(0,0,0,0.85);}
.final-card{background:rgba(0,0,0,0.95);border:2px solid #ffd24d;border-radius:12px;z-index:50;display:none;}
.transition{background:#fff;opacity:0;z-index:40;pointer-events:none;}
.transition.show{animation:flash 0.4s ease forwards;}
@keyframes flash{0%{opacity:1;}100%{opacity:0;}}

.btn{background:var(--accent);color:#000;border:none;padding:10px 12px;border-radius:8px;cursor:pointer;font-size:10px;margin-top:12px;}
.btn:active{transform:translateY(1px);}
#gameStage{position:relative;width:100%;height:380px;overflow:hidden;}
#character{position:absolute;width:32px;height:32px;bottom:40px;left:40px;transition:transform .1s linear;}
.obstacle{position:absolute;width:24px;height:24px;background:#ff6b6b;bottom:40px;animation:moveLeft linear infinite;}
.item{position:absolute;width:24px;height:24px;bottom:40px;background-size:cover;}
.particle{position:absolute;width:6px;height:6px;background:#ffd24d;border-radius:50%;pointer-events:none;animation:particleAnim 0.6s forwards;}
@keyframes particleAnim{0%{opacity:1;transform:translate(0,0);}100%{opacity:0;transform:translate(var(--x),var(--y));}}

.accept-btn,.restart-btn{background:#ff6b6b;color:#fff;border:none;padding:10px 14px;border-radius:10px;cursor:pointer;margin-top:10px;font-size:12px;}
.restart-btn{background:#00bcd4;}
.volume-container{display:flex;justify-content:center;align-items:center;margin-top:8px;font-size:10px;color:#bbb;}
.volume-container input[type=range]{-webkit-appearance:none;width:120px;height:6px;background:#111;border-radius:4px;margin-left:8px;cursor:pointer;}
.volume-container input[type=range]::-webkit-slider-thumb{-webkit-appearance:none;width:12px;height:12px;background:var(--accent);border-radius:50%;cursor:pointer;}
@keyframes moveLeft{0%{left:100%;}100%{left:-30px;}}
</style>
</head>
<body>

<div class="wrap">
  <div class="game">
    <div class="start-screen" id="start">
      <h1>MISSÃO: CINEMA</h1>
      <p>Corra, pule e colete os itens para desbloquear o convite!</p>
      <button class="btn" id="startBtn">INICIAR MISSÃO</button>
    </div>

    <div id="gameStage">
      <div id="character"></div>
    </div>

    <div class="transition" id="transition"></div>

    <div id="final" class="final-card">
      <h2>🎬 MISSÃO CONCLUÍDA</h2>
      <p>Você desbloqueou o convite secreto</p>
      <p style="color:#ffd;">💛 Com amor, Denise 💛</p>
      <button class="accept-btn" onclick="acceptInvite()">ACEITAR CONVITE</button>
      <button class="restart-btn" onclick="restartGame()">REINICIAR MISSÃO</button>
      <div class="volume-container">
        <span>Volume</span>
        <input type="range" id="volumeControl" min="0" max="1" step="0.05" value="1">
      </div>
    </div>
  </div>
</div>

<!-- Áudios -->
<audio id="sJump" src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_59b1998050.mp3?filename=jump-28321.mp3" preload="auto"></audio>
<audio id="sCollect" src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_6dff331a22.mp3?filename=coin-7783.mp3" preload="auto"></audio>
<audio id="sHit" src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_2acb7e3265.mp3?filename=beep-126.mp3" preload="auto"></audio>
<audio id="sFinal" src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_cba6cc9efb.mp3?filename=success-1-6297.mp3" preload="auto"></audio>

<script>
const startBtn=document.getElementById('startBtn');
const startScreen=document.getElementById('start');
const character=document.getElementById('character');
const gameStage=document.getElementById('gameStage');
const finalCard=document.getElementById('final');
const volumeControl=document.getElementById('volumeControl');
const transition=document.getElementById('transition');

let jumpSound=document.getElementById('sJump');
let collectSound=document.getElementById('sCollect');
let hitSound=document.getElementById('sHit');
let finalSound=document.getElementById('sFinal');
let audioElements=[jumpSound,collectSound,hitSound,finalSound];

let keys={};
let items=[], obstacles=[], doors=[], currentPhase=1;
let score=0, gameInterval, obstacleInterval;
let gravity=4, isJumping=false, charBottom=40;

startBtn.addEventListener('click',startGame);
volumeControl.addEventListener('input',()=>audioElements.forEach(a=>a.volume=volumeControl.value));
document.addEventListener('keydown',e=>keys[e.code]=true);
document.addEventListener('keyup',e=>keys[e.code]=false);

function playSound(audioEl){try{audioEl.currentTime=0;audioEl.play().catch(()=>{});}catch(e){}}

function startGame(){
  startScreen.style.display='none';
  character.style.bottom=charBottom+'px';
  character.style.left='40px';
  score=0;
  currentPhase=1;
  items=[]; obstacles=[]; doors=[];
  gameStage.innerHTML=''; gameStage.appendChild(character);
  startPhase1();
}

// -------- Fase 1 --------
function startPhase1(){
  createItems();
  gameInterval=setInterval(phase1Loop,20);
  obstacleInterval=setInterval(spawnObstacle,2000);
}

function createItems(){
  let itemImgs=['https://cdn-icons-png.flaticon.com/512/992/992703.png','https://cdn-icons-png.flaticon.com/512/733/733935.png','https://cdn-icons-png.flaticon.com/512/1046/1046784.png'];
  for(let i=0;i<itemImgs.length;i++){
    let item=document.createElement('div');
    item.className='item';
    item.style.left=(300+i*80)+'px';
    item.style.backgroundImage=`url(${itemImgs[i]})`;
    gameStage.appendChild(item);
    items.push(item);
  }
}

function spawnObstacle(){
  let obs=document.createElement('div');
  obs.className='obstacle';
  obs.style.bottom='40px';
  obs.style.left=gameStage.offsetWidth+'px';
  gameStage.appendChild(obs);
  obstacles.push(obs);
  setTimeout(()=>{obs.remove(); obstacles.shift();},8000);
}

function phase1Loop(){
  if(keys['ArrowUp'] && !isJumping){isJumping=true;playSound(jumpSound); jump();}
  let charLeft=parseInt(character.style.left);
  if(keys['ArrowRight'] && charLeft<gameStage.offsetWidth-32){character.style.left=charLeft+5+'px';}
  if(keys['ArrowLeft'] && charLeft>0){character.style.left=charLeft-5+'px';}

  items.forEach((item,i)=>{
    if(item&&checkCollision(character,item)){
      playSound(collectSound);
      createParticles(item);
      item.remove();
      items.splice(i,1);
      score++;
      if(score===3){phase1Completed();}
    }
  });

  obstacles.forEach(obs=>{
    if(checkCollision(character,obs)){
      playSound(hitSound);
      restartPhase1();
    }
  });
}

function createParticles(element){
  for(let i=0;i<10;i++){
    let p=document.createElement('div');
    p.className='particle';
    let x=(Math.random()-0.5)*50+'px';
    let y=(Math.random()-0.5)*50+'px';
    p.style.setProperty('--x',x);
    p.style.setProperty('--y',y);
    p.style.left=element.offsetLeft+'px';
    p.style.top=element.offsetTop+'px';
    gameStage.appendChild(p);
    setTimeout(()=>p.remove(),600);
  }
}

function jump(){
  let jumpHeight=80, upInterval=setInterval(()=>{
    if(charBottom>=jumpHeight+40){clearInterval(upInterval); down(); return;}
    charBottom+=6; character.style.bottom=charBottom+'px';
  },20);
  function down(){
    let downInterval=setInterval(()=>{
      if(charBottom<=40){charBottom=40; character.style.bottom=charBottom+'px'; clearInterval(downInterval); isJumping=false; return;}
      charBottom-=6; character.style.bottom=charBottom+'px';
    },20);
  }
}

function checkCollision(a,b){
  let rect1=a.getBoundingClientRect();
  let rect2=b.getBoundingClientRect();
  return !(rect1.top>rect2.bottom || rect1.bottom<rect2.top || rect1.right<rect2.left || rect1.left>rect2.right);
}

function phase1Completed(){
  clearInterval(gameInterval);
  clearInterval(obstacleInterval);
  showTransition(startPhase2);
}

// -------- Fase 2 --------
function startPhase2(){
  currentPhase=2;
  gameStage.innerHTML=''; character.style.left='40px'; character.style.bottom='40px'; gameStage.appendChild(character);
  doors=[];
  createDoors();
  gameInterval=setInterval(phase2Loop,20);
}

function createDoors(){
  for(let i=0;i<3;i++){
    let door=document.createElement('div');
    door.className='item';
    door.style.bottom='40px';
    door.style.left=(150+i*100)+'px';
    door.style.width='40px';
    door.style.height='60px';
    door.style.backgroundColor=i===1?'#ffd24d':'#555';
    if(i===1) door.style.boxShadow='0 0 10px #ffd24d';
    gameStage.appendChild(door);
    doors.push(door);
  }
}

function phase2Loop(){
  let charLeft=parseInt(character.style.left);
  if(keys['ArrowRight'] && charLeft<gameStage.offsetWidth-32){character.style.left=charLeft+5+'px';}
  if(keys['ArrowLeft'] && charLeft>0){character.style.left=charLeft-5+'px';}
  if(keys['ArrowUp'] && !isJumping){isJumping=true;playSound(jumpSound); jump();}

  doors.forEach((door,i)=>{
    if(checkCollision(character,door)){
      if(i===1){showTransition(startPhase3);}
      else{playSound(hitSound); character.style.left='40px';}
    }
  });
}

// -------- Fase 3 --------
function startPhase3(){
  currentPhase=3;
  gameStage.innerHTML=''; character.style.left='40px'; character.style.bottom='40px'; gameStage.appendChild(character);
  spawnTicket();
  gameInterval=setInterval(phase3Loop,20);
}

function spawnTicket(){
  let ticket=document.createElement('div');
  ticket.className='item';
  ticket.style.bottom='80px';
  ticket.style.left=Math.random()*(gameStage.offsetWidth-40)+'px';
  ticket.style.width='32px';
  ticket.style.height='32px';
  ticket.style.backgroundImage='url(https://cdn-icons-png.flaticon.com/512/3112/3112946.png)';
  gameStage.appendChild(ticket);
  items=[ticket];
}

function phase3Loop(){
  let charLeft=parseInt(character.style.left);
  if(keys['ArrowRight'] && charLeft<gameStage.offsetWidth-32){character.style.left=charLeft+5+'px';}
  if(keys['ArrowLeft'] && charLeft>0){character.style.left=charLeft-5+'px';}
  if(keys['ArrowUp'] && !isJumping){isJumping=true;playSound(jumpSound); jump();}

  items.forEach((item,i)=>{
    if(checkCollision(character,item)){
      playSound(finalSound);
      createParticles(item);
      endGame();
    }
  });
}

// -------- Funções gerais --------
function showTransition(callback){
  transition.classList.add('show');
  setTimeout(()=>{transition.classList.remove('show'); callback();},400);
}

function endGame(){
  clearInterval(gameInterval);
  finalCard.style.display='flex';
}

function acceptInvite(){alert("Convite aceito! 💛");}
function restartGame(){finalCard.style.display='none';startGame();}
function restartPhase1(){clearInterval(gameInterval);clearInterval(obstacleInterval);startPhase1();}
</script>
</body>
</html>

