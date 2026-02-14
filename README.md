<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>For Mihi</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;600&display=swap" rel="stylesheet">

<style>
*{
  margin:0;
  padding:0;
  box-sizing:border-box;
  font-family:'Poppins', sans-serif;
}

body{
  min-height:100vh;
  display:flex;
  justify-content:center;
  align-items:center;
  background:linear-gradient(135deg,#ffd6e8,#ffeaf4,#ffc2dd);
  overflow:hidden;
  position:relative;
}

.container{
  width:90%;
  max-width:650px;
  background:rgba(255,255,255,0.95);
  padding:40px;
  border-radius:20px;
  box-shadow:0 20px 40px rgba(0,0,0,0.15);
  text-align:center;
  position:absolute;
  transition:0.6s ease;
}

.hidden{
  opacity:0;
  pointer-events:none;
  transform:scale(0.9);
}

h1{
  color:#d63384;
  margin-bottom:20px;
}

p{
  line-height:1.7;
  margin-bottom:20px;
  color:#444;
}

button{
  padding:12px 25px;
  border:none;
  border-radius:30px;
  margin:10px;
  font-size:1rem;
  cursor:pointer;
  transition:0.3s;
}

.yes-btn{
  background:#ff4d88;
  color:white;
}

.no-btn{
  background:#ddd;
  position:absolute;
}

button:hover{
  transform:scale(1.1);
}

/* Rose Petals */
.petal{
  position:fixed;
  top:-20px;
  width:12px;
  height:18px;
  background:#ff4d6d;
  border-radius:50% 50% 50% 0;
  transform:rotate(45deg);
  opacity:0.8;
  animation:fall linear forwards;
}

@keyframes fall{
  to{
    transform:translateY(110vh) rotate(360deg);
  }
}

/* Final Screen */
#final{
  position:fixed;
  inset:0;
  background:linear-gradient(135deg,#ffb6d5,#ffcce6);
  display:flex;
  justify-content:center;
  align-items:center;
  flex-direction:column;
  text-align:center;
  color:white;
  opacity:0;
  pointer-events:none;
  transition:1s ease;
}

#final.show{
  opacity:1;
  pointer-events:auto;
}

.popMain{
  font-size:3rem;
  font-weight:700;
  animation:pop 1.5s ease forwards;
}

.popSub{
  font-size:1.3rem;
  margin-top:20px;
  animation:fadeIn 2s ease forwards;
}

@keyframes pop{
  0%{transform:scale(0); opacity:0;}
  60%{transform:scale(1.2);}
  100%{transform:scale(1); opacity:1;}
}

@keyframes fadeIn{
  from{opacity:0; transform:translateY(20px);}
  to{opacity:1; transform:translateY(0);}
}

.cat{
  width:240px;
  margin-top:25px;
  border-radius:15px;
}

</style>
</head>

<body>

<audio id="music" loop>
  <source src="music.mp3" type="audio/mpeg">
</audio>

<!-- Page 1 -->
<div class="container" id="page1">
  <h1>Hello Mihi</h1>
  <p>Your so-called boyfriend has something to tell you this Valentine’s Day.
  Would you like to proceed?</p>
  <button class="yes-btn" onclick="startMusic(); nextPage(2)">Yes</button>
  <button class="no-btn" id="noBtn">No</button>
  <br>
  <img class="cat" src="https://media.giphy.com/media/JIX9t2j0ZTN9S/giphy.gif">
</div>

<!-- Page 2 -->
<div class="container hidden" id="page2">
  <h1>Before I Ask You Something</h1>
  <p>
    These past few months changed a lot.  
    But through every shift, you’ve been the best part of it all.  

    I’m not perfect — but I’m becoming better every day.  
    And I’ve never been more certain about anything than I am about this.
  </p>
  <button class="yes-btn" onclick="nextPage(3)">Continue</button>
</div>

<!-- Page 3 -->
<div class="container hidden" id="page3">
  <h1>Will You Be My Valentine?</h1>
  <button class="yes-btn" onclick="celebrate()">Yes</button>
  <button class="yes-btn" onclick="celebrate()">Aama</button>
  <button class="yes-btn" onclick="celebrate()">Avunu</button>
</div>

<!-- Final Screen -->
<div id="final">
  <div class="popMain">I Love U Mihi</div>
  <div class="popSub">And trust me… choosing me will be the best decision you ever made.</div>
  <img class="cat" src="https://media.giphy.com/media/12HZukMBlutpoQ/giphy.gif">
</div>

<script>

function startMusic(){
  const music = document.getElementById("music");
  music.play().catch(() => {
    console.log("User interaction required for audio.");
  });
}

function nextPage(page){
  document.querySelectorAll(".container").forEach(c=>c.classList.add("hidden"));
  document.getElementById("page"+page).classList.remove("hidden");
}

const noBtn=document.getElementById("noBtn");
noBtn.addEventListener("mouseover",()=>{
  const x=Math.random()*(window.innerWidth-100);
  const y=Math.random()*(window.innerHeight-50);
  noBtn.style.left=x+"px";
  noBtn.style.top=y+"px";
});

function createPetal(){
  const petal=document.createElement("div");
  petal.classList.add("petal");
  petal.style.left=Math.random()*100+"vw";
  petal.style.animationDuration=(Math.random()*4+4)+"s";
  document.body.appendChild(petal);
  setTimeout(()=>petal.remove(),8000);
}

function celebrate(){
  for(let i=0;i<50;i++){
    setTimeout(createPetal,i*120);
  }
  setTimeout(()=>{
    document.getElementById("final").classList.add("show");
  },2000);
}

</script>

</body>
</html>

