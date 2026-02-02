# valanitnes-day
chinmin
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>For Chinmin 💖</title>

<style>
  body{
    margin:0;
    height:100vh;
    overflow:hidden;
    font-family:'Poppins',sans-serif;
    background:linear-gradient(135deg,#ff9a9e,#fad0c4);
    display:flex;
    justify-content:center;
    align-items:center;
    transition:1s;
  }

  body.private{
    background:radial-gradient(circle,#2b0f1a,#000);
  }

  body.locked{
    pointer-events:none;
  }

  .backdrop{
    position:fixed;
    inset:0;
    backdrop-filter:blur(0);
    transition:.8s;
    z-index:1;
  }

  body.private .backdrop{
    backdrop-filter:blur(6px);
  }

  .card{
    background:#fff;
    padding:26px;
    border-radius:25px;
    text-align:center;
    width:90%;
    max-width:360px;
    box-shadow:0 25px 50px rgba(0,0,0,.25);
    position:relative;
    z-index:2;
    transition:1s;
  }

  body.whisper .card{
    opacity:0;
    transform:scale(.95);
  }

  .name-only{
    position:absolute;
    inset:0;
    display:flex;
    align-items:center;
    justify-content:center;
    font-size:36px;
    color:#ff7aa2;
    letter-spacing:2px;
    opacity:0;
    transition:1.5s;
    z-index:3;
  }

  body.whisper .name-only{
    opacity:1;
  }

  h1{color:#ff4d6d;margin:8px 0}
  p{color:#555;font-size:14px}

  button{
    padding:14px 28px;
    font-size:16px;
    border-radius:30px;
    border:none;
    cursor:pointer;
  }

  #yes{
    background:#ff4d6d;
    color:#fff;
    margin:10px;
  }

  /* FIXED NO BUTTON */
  #no{
    background:#ddd;
    position:absolute;
    left:50%;
    top:65%;
    transform:translateX(-50%);
  }

  .heart{
    position:absolute;
    font-size:22px;
    animation:floatUp 6s linear infinite;
    opacity:.6;
    z-index:0;
  }

  @keyframes floatUp{
    0%{transform:translateY(100vh);opacity:0}
    10%{opacity:1}
    100%{transform:translateY(-10vh) scale(1.4);opacity:0}
  }

  .msg{
    font-size:48px;
    margin-top:12px;
    position:relative;
    cursor:pointer;
  }

  .msg.disabled{
    opacity:.4;
    pointer-events:none;
  }

  .dot{
    position:absolute;
    top:6px;
    right:8px;
    width:12px;
    height:12px;
    background:red;
    border-radius:50%;
  }

  .typing{font-size:13px;color:#888;display:none}
  .secret{
    margin-top:12px;
    background:#fff0f5;
    padding:14px;
    border-radius:15px;
    min-height:95px;
    text-align:left;
    font-size:14px;
    display:none;
    white-space:pre-line;
  }

  .seen{font-size:11px;color:#aaa;display:none;margin-top:5px}
  .hint{font-size:11px;color:#777;margin-top:8px}
  .privacy{font-size:11px;color:#bbb;margin-top:6px;opacity:0}

  body.private .privacy{
    opacity:1;
  }

  /* hidden reset */
  .reset{
    position:fixed;
    bottom:6px;
    right:6px;
    width:20px;
    height:20px;
    opacity:.05;
    z-index:10;
  }
</style>
</head>

<body>

<div class="backdrop"></div>
<div class="name-only">Chinmin</div>

<div class="card" id="card">
  <h1>Chinmin 💕</h1>
  <p>I need your honest answer 🫣</p>
  <h1>Will you be my Valentine? 💘</h1>
  <button id="yes">Yes 💖</button>
  <button id="no">No 🙄</button>
</div>

<div class="reset" id="reset"></div>

<script>
const noBtn = document.getElementById("no");
const yesBtn = document.getElementById("yes");
const card = document.getElementById("card");

/* NO button escape */
function moveNo(){
  noBtn.style.left = Math.random() * (window.innerWidth - 120) + "px";
  noBtn.style.top  = Math.random() * (window.innerHeight - 60) + "px";
}
noBtn.addEventListener("mouseenter", moveNo);
noBtn.addEventListener("touchstart", moveNo);

/* YES */
yesBtn.addEventListener("click", ()=>{
  card.innerHTML = `
    <h1>You said YES 😌💖</h1>
    <p>I like that choice.</p>

    <div class="msg" id="msg">
      💌<div class="dot"></div>
    </div>

    <div class="typing" id="typing">typing…</div>
    <div class="secret" id="secret"></div>
    <div class="seen" id="seen">Seen 👀</div>

    <div class="hint">Tap for messages · Long-press for private mode 😏</div>
    <div class="privacy">Private · maybe don’t screenshot 🫣</div>
  `;

  const msgs = [
    "Still curious? I like that about you 😌",
    "You came back again… I noticed.",
    "Every tap feels intentional.",
    "You’re enjoying this more than you admit 😏",
    "Careful—if you keep going, I take the lead."
  ];

  let index = 0;
  let finalUnlocked = false;

  const msg = document.getElementById("msg");
  const secret = document.getElementById("secret");
  const typing = document.getElementById("typing");
  const seen = document.getElementById("seen");
  const dot = document.querySelector(".dot");

  function vibrate(p){
    if(navigator.vibrate) navigator.vibrate(p);
  }

  function typeText(text){
    secret.style.display = "block";
    typing.style.display = "block";
    seen.style.display = "none";
    secret.innerHTML = "";
    let i = 0;

    const iv = setInterval(()=>{
      secret.innerHTML += text.charAt(i++);
      if(i >= text.length){
        clearInterval(iv);
        typing.style.display = "none";
        setTimeout(()=>seen.style.display="block",600);
      }
    },35);
  }

  msg.addEventListener("click", ()=>{
    dot.style.display = "none";
    typeText(msgs[index]);
    index = (index + 1) % msgs.length;
  });

  /* LONG PRESS FINAL */
  let timer;
  msg.addEventListener("touchstart", ()=>{
    timer = setTimeout(()=>{
      if(finalUnlocked) return;
      finalUnlocked = true;

      document.body.classList.add("private");
      msg.classList.add("disabled");
      vibrate([60,80,60,120]);

      typeText(
        "Enough teasing.\n\nCome closer.\nSlowly.\n\nThis stays between us.\n\nChinmin 💖"
      );

      setTimeout(()=>{
        document.body.classList.add("whisper","locked");
      },5000);
    },1200);
  });
  msg.addEventListener("touchend", ()=>clearTimeout(timer));

  setTimeout(()=>{
    if(!finalUnlocked){
      typeText("Still here? 😏 I like your patience.");
    }
  },10000);
});

/* floating hearts */
function heart(){
  const h = document.createElement("div");
  h.className = "heart";
  h.textContent = "💖";
  h.style.left = Math.random()*100 + "vw";
  h.style.animationDuration = (Math.random()*3+4) + "s";
  document.body.appendChild(h);
  setTimeout(()=>h.remove(),7000);
}
setInterval(heart,300);

/* secret reset (5 taps) */
let taps = 0;
document.getElementById("reset").addEventListener("click", ()=>{
  taps++;
  if(taps >= 5) location.reload();
});
</script>

</body>
</html>
