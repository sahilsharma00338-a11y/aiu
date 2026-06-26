<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Will You Go On A Date With Me?</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@600;700&family=Poppins:ital,wght@0,400;0,500;0,600;1,400&display=swap" rel="stylesheet">
<style>
  :root{
    --bg-light:#ffeef5;
    --bg-mid:#ffb3c9;
    --bg-deep:#ff7096;
    --red:#e0144c;
    --red-dark:#b3103c;
    --ink:#6b1530;
    --white:#ffffff;
  }

  *{ box-sizing:border-box; -webkit-tap-highlight-color:transparent; }

  html,body{
    margin:0;
    padding:0;
    height:100%;
    width:100%;
    overflow:hidden;
    background:linear-gradient(160deg,var(--bg-light) 0%, var(--bg-mid) 45%, var(--bg-deep) 100%);
    font-family:'Poppins',sans-serif;
  }

  body{
    position:relative;
    display:flex;
    align-items:center;
    justify-content:center;
  }

  /* ---------- floating hearts ---------- */
  .hearts-container{
    position:fixed;
    inset:0;
    overflow:hidden;
    pointer-events:none;
    z-index:1;
  }

  .heart{
    position:absolute;
    bottom:-10%;
    left:0;
    will-change:transform, opacity;
    animation-name:floatUp;
    animation-timing-function:ease-in-out;
    animation-iteration-count:infinite;
    user-select:none;
  }

  @keyframes floatUp{
    0%   { transform:translate(0,0) rotate(0deg);   opacity:0;   }
    12%  { opacity:0.9; }
    50%  { transform:translate(var(--dx,20px), -55vh) rotate(8deg); }
    85%  { opacity:0.85; }
    100% { transform:translate(calc(var(--dx,20px) * -1), -115vh) rotate(-8deg); opacity:0; }
  }

  /* ---------- main stage ---------- */
  .stage{
    position:relative;
    z-index:2;
    max-width:560px;
    width:90vw;
    max-height:92vh;
    overflow-y:auto;
    text-align:center;
    padding:clamp(28px,5vw,48px) clamp(20px,5vw,40px);
    border-radius:32px;
    background:rgba(255,255,255,0.55);
    backdrop-filter:blur(14px);
    -webkit-backdrop-filter:blur(14px);
    box-shadow:0 20px 60px rgba(179,16,60,0.18);
  }

  .bear{
    font-size:clamp(3rem,10vw,4.4rem);
    display:inline-block;
    animation:bounce 1.6s ease-in-out infinite;
    user-select:none;
  }

  @keyframes bounce{
    0%,100%{ transform:translateY(0); }
    50%    { transform:translateY(-18px); }
  }

  .heading{
    font-family:'Dancing Script',cursive;
    font-weight:700;
    color:var(--ink);
    font-size:clamp(2.1rem,7vw,3.4rem);
    line-height:1.15;
    margin:10px 0 14px;
    text-shadow:0 2px 18px rgba(255,255,255,0.65);
  }

  .subtitle{
    font-style:italic;
    color:var(--ink);
    opacity:0.85;
    font-size:clamp(0.95rem,2.6vw,1.1rem);
    margin:0 0 18px;
  }

  .closing{
    color:var(--ink);
    font-weight:500;
    font-size:clamp(0.95rem,2.6vw,1.05rem);
    margin:0 0 30px;
    opacity:0.9;
  }

  /* ---------- buttons ---------- */
  .button-row{
    display:flex;
    flex-wrap:wrap;
    align-items:center;
    justify-content:center;
    gap:48px;
  }

  button{
    font-family:'Poppins',sans-serif;
    border:none;
    cursor:pointer;
    touch-action:manipulation;
  }

  .btn-yes{
    background:linear-gradient(135deg,#ff6f96,var(--red) 60%,var(--red-dark));
    color:var(--white);
    font-weight:600;
    font-size:clamp(1rem,2.6vw,1.15rem);
    padding:16px 44px;
    border-radius:999px;
    box-shadow:0 10px 25px rgba(179,16,60,0.4);
    transition:transform 0.2s ease, box-shadow 0.2s ease;
  }

  .btn-yes:hover{
    transform:translateY(-3px) scale(1.06);
    box-shadow:0 0 28px 8px rgba(255,55,110,0.65), 0 12px 28px rgba(179,16,60,0.45);
  }

  .btn-yes:focus-visible{
    outline:3px solid var(--ink);
    outline-offset:3px;
  }

  .btn-no{
    background:var(--white);
    color:var(--red);
    font-weight:600;
    font-size:clamp(0.85rem,2.2vw,0.95rem);
    padding:11px 26px;
    border-radius:999px;
    border:2px solid var(--red);
    transition:left 0.18s ease, top 0.18s ease, transform 0.15s ease;
    white-space:nowrap;
  }

  .btn-no:focus-visible{
    outline:3px solid var(--ink);
    outline-offset:3px;
  }

  /* ---------- celebration ---------- */
  .celebration{
    position:fixed;
    inset:0;
    z-index:10;
    display:none;
    flex-direction:column;
    align-items:center;
    justify-content:center;
    text-align:center;
    gap:14px;
    background:linear-gradient(160deg,var(--bg-light) 0%, var(--bg-mid) 45%, var(--bg-deep) 100%);
  }

  .spin-emoji{
    font-size:clamp(3rem,9vw,4.8rem);
    animation:spin 3s linear infinite;
    user-select:none;
  }

  @keyframes spin{ to{ transform:rotate(360deg); } }

  .yay-text{
    font-family:'Dancing Script',cursive;
    font-weight:700;
    color:var(--ink);
    font-size:clamp(3rem,11vw,6rem);
    margin:0;
    text-shadow:0 4px 22px rgba(255,255,255,0.7);
    animation:pulse 1.1s ease-in-out infinite;
  }

  @keyframes pulse{
    0%,100%{ transform:scale(1); }
    50%    { transform:scale(1.15); }
  }

  .celebration-message{
    font-style:italic;
    color:var(--ink);
    font-size:clamp(1rem,3vw,1.25rem);
    margin:0;
    opacity:0.9;
  }

  .confetti-piece{
    position:fixed;
    left:50%;
    top:38%;
    opacity:0;
    pointer-events:none;
    z-index:11;
    will-change:transform, opacity;
    animation-name:confettiBurst;
    animation-timing-function:cubic-bezier(.15,.7,.3,1);
    animation-fill-mode:forwards;
  }

  @keyframes confettiBurst{
    0%   { transform:translate(-50%,-50%) scale(0.3) rotate(0deg); opacity:0; }
    8%   { opacity:1; }
    100% { transform:translate(calc(-50% + var(--dx)), calc(-50% + var(--dy))) scale(1) rotate(var(--rot)); opacity:0; }
  }

  @media (prefers-reduced-motion: reduce){
    *, *::before, *::after{
      animation-duration:0.01ms !important;
      animation-iteration-count:1 !important;
    }
  }
</style>
</head>
<body>

  <div class="hearts-container" id="heartsContainer" aria-hidden="true"></div>

  <main class="stage" id="stage">
    <div class="bear" aria-hidden="true">🐻</div>
    <h1 class="heading">Will You Go On A Date With Me, <span id="valentineName">Monika</span>?</h1>
    <p class="subtitle">You're the closest to heaven that I'll ever be.</p>
    <p class="closing">Every love story is beautiful, but ours is my favourite.</p>

    <div class="button-row" id="buttonRow">
      <button class="btn-yes" id="yesBtn" type="button">Yes 💖</button>
      <button class="btn-no" id="noBtn" type="button">No</button>
    </div>
  </main>

  <section class="celebration" id="celebration" aria-hidden="true">
    <div class="spin-emoji" aria-hidden="true">💖</div>
    <h2 class="yay-text">Yayyy!!</h2>
    <p class="celebration-message">I can't wait to see you!</p>
  </section>

<script>
(function(){
  "use strict";

  /* ---------------- floating hearts ---------------- */
  var heartsContainer = document.getElementById('heartsContainer');
  var HEART_COUNT = 15;

  function rand(min, max){ return Math.random() * (max - min) + min; }

  for (var i = 0; i < HEART_COUNT; i++){
    var heart = document.createElement('span');
    heart.className = 'heart';
    heart.textContent = '❤️';

    var size = rand(16, 42);
    var duration = rand(6, 14);
    var delay = rand(-12, 0);
    var leftPos = rand(2, 96);
    var drift = rand(-40, 40);

    heart.style.left = leftPos + 'vw';
    heart.style.fontSize = size + 'px';
    heart.style.animationDuration = duration + 's';
    heart.style.animationDelay = delay + 's';
    heart.style.setProperty('--dx', drift + 'px');

    heartsContainer.appendChild(heart);
  }

  /* ---------------- "No" button runs away ---------------- */
  var noBtn = document.getElementById('noBtn');
  var yesBtn = document.getElementById('yesBtn');

  var noMessages = [
    'Nope, not an option!',
    'Try again!',
    'You sure about that?',
    'Not happening!',
    'Think again!'
  ];
  var msgIndex = 0;

  function moveNoButton(){
    // cycle the cheeky message
    noBtn.textContent = noMessages[msgIndex % noMessages.length];
    msgIndex++;

    // switch to fixed positioning in place, the first time
    if (noBtn.style.position !== 'fixed'){
      var startRect = noBtn.getBoundingClientRect();
      noBtn.style.position = 'fixed';
      noBtn.style.left = startRect.left + 'px';
      noBtn.style.top = startRect.top + 'px';
      noBtn.style.margin = '0';
    }

    var btnW = noBtn.offsetWidth;
    var btnH = noBtn.offsetHeight;
    var pad = 12;
    var maxX = Math.max(pad, window.innerWidth - btnW - pad);
    var maxY = Math.max(pad, window.innerHeight - btnH - pad);

    var yesRect = yesBtn.getBoundingClientRect();
    var buffer = 24;

    var x, y, tries = 0, overlaps;
    do {
      x = rand(pad, maxX);
      y = rand(pad, maxY);
      overlaps = (
        x < yesRect.right + buffer &&
        x + btnW > yesRect.left - buffer &&
        y < yesRect.bottom + buffer &&
        y + btnH > yesRect.top - buffer
      );
      tries++;
    } while (overlaps && tries < 40);

    noBtn.style.left = x + 'px';
    noBtn.style.top = y + 'px';
  }

  noBtn.addEventListener('click', moveNoButton);

  /* ---------------- "Yes" button celebration ---------------- */
  var stage = document.getElementById('stage');
  var heartsBox = document.getElementById('heartsContainer');
  var celebration = document.getElementById('celebration');

  function spawnConfetti(count){
    var colors = ['#ff5e7e', '#ff8fab', '#ffd166', '#a162e8', '#4cc9f0', '#ffffff', '#e0144c'];
    for (var i = 0; i < count; i++){
      var piece = document.createElement('div');
      piece.className = 'confetti-piece';

      var w = rand(6, 13);
      var h = w * (Math.random() > 0.5 ? 1 : 1.7);
      var angle = rand(0, Math.PI * 2);
      var dist = rand(30, 90);
      var dx = (Math.cos(angle) * dist) + 'vw';
      var dy = (Math.sin(angle) * dist * 0.5 + rand(25, 70)) + 'vh';
      var rot = (rand(360, 1080) * (Math.random() > 0.5 ? 1 : -1)) + 'deg';
      var dur = rand(1.6, 3) + 's';
      var del = rand(0, 0.4) + 's';

      piece.style.width = w + 'px';
      piece.style.height = h + 'px';
      piece.style.background = colors[Math.floor(rand(0, colors.length))];
      piece.style.borderRadius = Math.random() > 0.5 ? '50%' : '2px';
      piece.style.setProperty('--dx', dx);
      piece.style.setProperty('--dy', dy);
      piece.style.setProperty('--rot', rot);
      piece.style.animationDuration = dur;
      piece.style.animationDelay = del;

      celebration.appendChild(piece);
    }
  }

  yesBtn.addEventListener('click', function(){
    stage.style.display = 'none';
    heartsBox.style.display = 'none';
    celebration.style.display = 'flex';
    celebration.setAttribute('aria-hidden', 'false');
    spawnConfetti(120);
  });

})();
</script>
</body>
</html>
