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
  font-family:'Arial', sans-serif;
  overflow:hidden;
}

.card{
  background:white;
  padding:25px;
  border-radius:22px;
  text-align:center;
  width:90%;
  max-width:360px;
  position:relative;
  z-index:2;
}

h1{
  color:#ff4d6d;
}

p{
  color:#555;
  font-size:15px;
}

button{
  padding:12px 24px;
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

/* hearts */
.heart{
  position:absolute;
  font-size:20px;
  animation:float 6s linear infinite;
}
@keyframes float{
  from{transform:translateY(100vh);opacity:0}
  to{transform:translateY(-10vh);opacity:1}
}

/* big good choice */
.good{
  font-size:32px;
  font-weight:bold;
  color:#ff4d6d;
  margin-bottom:5px;
}

.sticker{
  font-size:60px;
  margin:10px 0;
}

.msg{
  font-size:46px;
  cursor:pointer;
  margin-top:10px;
}

.secret{
  margin-top:12px;
  background:#fff0f5;
  padding:14px;
  border-radius:14px;
  min-height:70px;
  text-align:left;
  font-size:14px;
}
.tap{
  font-size:12px;
  color:#888;
  margin-top:6px;
}
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
const card=document.getElementById("card");
const noBtn=document.getElementById("no");

/* NO runs */
function moveNo(){
  noBtn.style.left=Math.random()*(window.innerWidth-120)+"px";
  noBtn.style.top=Math.random()*(window.innerHeight-60)+"px";
}
noBtn.addEventListener("mouseenter",moveNo);
noBtn.addEventListener("touchstart",moveNo);

/* YES */
document.getElementById("yes").onclick=()=>{
  card.innerHTML=`
    <div class="good">GOOD CHOICE 💖</div>
    <div class="sticker">💑🥰</div>
    <p>You just made my heart very happy.</p>

    <div class="msg" id="msg">💌</div>
    <div class="secret" id="secret"></div>
    <div class="tap">Tap the message 💌</div>
  `;

  const messages=[
    "Hey Chinmin… I really like that you said yes 😌",
    "You tapping again tells me you’re curious 😏",
    "Every tap feels a little more personal.",
    "I hope you know you look cute as my Valentine 🫣",
    "Okay… that smile you’re making? I like it 💖"
  ];

  let index=0;
  const msg=document.getElementById("msg");
  const secret=document.getElementById("secret");

  msg.onclick=()=>{
    secret.textContent=messages[index];
    index++;
    if(index>=messages.length){
      index=messages.length-1; // stay on last
    }
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

