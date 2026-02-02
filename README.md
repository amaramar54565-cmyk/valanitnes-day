# valanitnes-day
chinmin
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>For Chinmin 💖</title>

<style>
body{
  margin:0;
  height:100vh;
  display:flex;
  justify-content:center;
  align-items:center;
  background:linear-gradient(135deg,#ff9a9e,#fad0c4);
  font-family:Arial, sans-serif;
  overflow:hidden;
}

.card{
  background:white;
  padding:25px;
  border-radius:20px;
  text-align:center;
  width:90%;
  max-width:350px;
  position:relative;
  z-index:2;
}

h1{color:#ff4d6d;}
p{color:#555;}

button{
  padding:12px 22px;
  border:none;
  border-radius:25px;
  font-size:16px;
}

#yes{
  background:#ff4d6d;
  color:white;
  margin:10px;
}

#no{
  background:#ddd;
  position:absolute;
  left:50%;
  top:65%;
  transform:translateX(-50%);
}

/* Hearts */
.heart{
  position:absolute;
  font-size:20px;
  animation:float 6s linear infinite;
}
@keyframes float{
  from{transform:translateY(100vh);opacity:0}
  to{transform:translateY(-10vh);opacity:1}
}

.msg{
  font-size:45px;
  margin-top:10px;
  cursor:pointer;
}

.secret{
  margin-top:10px;
  background:#fff0f5;
  padding:12px;
  border-radius:12px;
  min-height:60px;
  display:none;
  text-align:left;
  font-size:14px;
}
.typing{font-size:12px;color:#888;display:none}
</style>
</head>

<body>

<div class="card" id="card">
  <h1>Chinmin 💕</h1>
  <p>Will you be my Valentine? 💘</p>
  <button id="yes">Yes 💖</button>
  <button id="no">No 🙄</button>
</div>

<script>
const noBtn=document.getElementById("no");
const yesBtn=document.getElementById("yes");
const card=document.getElementById("card");

/* NO runs away */
function moveNo(){
  noBtn.style.left=Math.random()*(window.innerWidth-120)+"px";
  noBtn.style.top=Math.random()*(window.innerHeight-60)+"px";
}
noBtn.addEventListener("mouseenter",moveNo);
noBtn.addEventListener("touchstart",moveNo);

/* YES click */
yesBtn.onclick=()=>{
  card.innerHTML=`
    <h1>You said YES 😌</h1>
    <p>Good choice.</p>
    <div class="msg" id="msg">💌</div>
    <div class="typing" id="typing">typing…</div>
    <div class="secret" id="secret"></div>
    <p style="font-size:12px">Tap the message…</p>
  `;

  const messages=[
    "Hey Chinmin… I like that you said yes 😌",
    "You’re still tapping? Interesting 😏",
    "Each tap makes this feel more dangerous.",
    "You’re enjoying this more than you admit 🫣",
    "Okay… come closer. This one’s just for you 💖"
  ];

  let i=0;
  const msg=document.getElementById("msg");
  const secret=document.getElementById("secret");
  const typing=document.getElementById("typing");

  function typeText(text){
    secret.style.display="block";
    typing.style.display="block";
    secret.innerHTML="";
    let c=0;
    const iv=setInterval(()=>{
      secret.innerHTML+=text.charAt(c++);
      if(c>=text.length){
        clearInterval(iv);
        typing.style.display="none";
      }
    },30);
  }

  msg.onclick=()=>{
    typeText(messages[i]);
    i=Math.min(i+1,messages.length-1);
  };
};

/* hearts */
setInterval(()=>{
  const h=document.createElement("div");
  h.className="heart";
  h.textContent="💖";
  h.style.left=Math.random()*100+"vw";
  document.body.appendChild(h);
  setTimeout(()=>h.remove(),6000);
},400);
</script>

</body>
</html>
