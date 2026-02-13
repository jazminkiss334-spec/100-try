OUR STORY
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>LOVE_PROTOCOL</title>

<style>
body{
    margin:0;
    background:black;
    color:#00ff88;
    font-family:Courier New, monospace;
    text-align:center;
    overflow:hidden;
}

canvas{
    position:fixed;
    top:0;
    left:0;
    z-index:-1;
}

h1{
    margin-top:40px;
    text-shadow:0 0 15px #00ff88;
}

#terminal{
    margin-top:40px;
    min-height:150px;
    font-size:18px;
}

input{
    background:black;
    border:1px solid #00ff88;
    color:#00ff88;
    padding:10px;
    width:400px;
    margin-top:20px;
}

button{
    background:#001a0f;
    border:1px solid #00ff88;
    color:#00ff88;
    padding:10px 20px;
    cursor:pointer;
}

button:hover{
    background:#003322;
}

.glitch{
    animation:glitch 1s infinite;
}

@keyframes glitch{
    0%{text-shadow:2px 2px red;}
    25%{text-shadow:-2px -2px blue;}
    50%{text-shadow:2px -2px lime;}
    75%{text-shadow:-2px 2px magenta;}
    100%{text-shadow:2px 2px red;}
}

.robot{
    font-size:90px;
    animation:float 2s infinite;
}

@keyframes float{
    0%{transform:translateY(0);}
    50%{transform:translateY(-20px);}
    100%{transform:translateY(0);}
}

.floatingHeart{
    position:absolute;
    font-size:28px;
    animation:floatUp 3s linear forwards;
}

@keyframes floatUp{
    0%{transform:translateY(0); opacity:1;}
    100%{transform:translateY(-250px); opacity:0;}
}

#robotArea{
    position:relative;
    height:250px;
}
</style>
</head>

<body>

<canvas id="matrix"></canvas>

<h1 class="glitch">OPERATION: LOVE_PROTOCOL</h1>

<div id="terminal">Booting system...</div>
<input id="answer" placeholder="ENTER COMMAND">
<br>
<button onclick="checkAnswer()">EXECUTE</button>

<script>

/* MATRIX BACKGROUND */
const canvas = document.getElementById("matrix");
const ctx = canvas.getContext("2d");
canvas.height = window.innerHeight;
canvas.width = window.innerWidth;
const letters = "01LOVE";
const fontSize = 14;
const columns = canvas.width/fontSize;
const drops = [];
for(let x=0;x<columns;x++) drops[x]=1;

function drawMatrix(){
    ctx.fillStyle="rgba(0,0,0,0.05)";
    ctx.fillRect(0,0,canvas.width,canvas.height);
    ctx.fillStyle="#00ff88";
    ctx.font=fontSize+"px monospace";
    for(let i=0;i<drops.length;i++){
        const text = letters[Math.floor(Math.random()*letters.length)];
        ctx.fillText(text,i*fontSize,drops[i]*fontSize);
        if(drops[i]*fontSize>canvas.height && Math.random()>0.975)
            drops[i]=0;
        drops[i]++;
    }
}
setInterval(drawMatrix,33);

/* GAME LOGIC */

let level=0;
let fails=0;
const terminal=document.getElementById("terminal");

function normalize(t){return t.toLowerCase().trim();}

function bootSequence(){
    setTimeout(()=>terminal.innerHTML="Loading love.exe ...",1000);
    setTimeout(()=>terminal.innerHTML="Decrypting memories ...",2000);
    setTimeout(()=>terminal.innerHTML="Type <b>start</b> to initialize system.",3000);
}
bootSequence();

function checkAnswer(){
    let input=normalize(document.getElementById("answer").value);

    if(level===0){
        if(input==="start"){
            level=1;
            terminal.innerHTML="SYSTEM INITIALIZED ✔<br><br>LEVEL 1:<br>What was the first thing I asked you NOT to do at the beginning?";
        } else fail();
    }

    else if(level===1){
        if(input.includes("not put") && input.includes("floor")){
            level=2;
            terminal.innerHTML="LEVEL 1 COMPLETE ✔<br><br>LEVEL 2:<br>First drink together and where?";
        } else fail();
    }

    else if(level===2){
        if(input.includes("tea") && input.includes("billy")){
            level=3;
            terminal.innerHTML="LEVEL 2 COMPLETE ✔<br>'If you continue like this maybe today you can love me one hour more.'<br><br>LEVEL 3:<br>Where was our frist kiss and which day?.";
        } else fail();
    }

    else if(level===3){
        if(input.includes("duna riverside") && input.includes("sunday")){
            level=4;
            terminal.innerHTML="LEVEL 3 COMPLETE ✔<br><br>LEVEL 4:<br>Which food we ate at our frist night? What was the type of our frist escape room?What type of chocholet you gived me at the frist time in taxi?";
        } else fail();
    }

    else if(level===4){
        if(input.includes("spaghetti") && input.includes("egyptian") && input.includes("ferrero")){
            level=5;
            terminal.innerHTML="LEVEL 4 COMPLETE ✔<br><br>LEVEL 5:<br>What was the frist thing on you what i liked from the frist time ?";
        } else fail();
    }

    else if(level===5){
        if(input.includes("face")||input.includes("eyes")){
            level=6;
            terminal.innerHTML="LEVEL 5 COMPLETE ✔<br><br>LEVEL 6:<br>Describe our relationship in 5 words.";
        } else fail();
    }

    else if(level===6){
        if(input.split(" ").length>=5){
            showFinal();
        } else fail();
    }

    document.getElementById("answer").value="";
}

function fail(){
    fails++;
    terminal.innerHTML+="<br><br>ACCESS DENIED ❌";
    if(fails>=3){
        terminal.innerHTML+="<br>SYSTEM WARNING: Emotional firewall triggered.";
    }
}

/* FINAL */

function showFinal(){
    terminal.innerHTML=`
    <h2 class="glitch">SYSTEM SUCCESSFUL</h2>
    <div id="robotArea">
        <div class="robot">🤖</div>
        <div id="hearts"></div>
    </div>
    <h2>
    I love you my Love<br>
    Happy Valentine's Day ❤️
    </h2>
    <h3 id="countdown"></h3>
    `;
    startHeartRain();
    startCountdown();
}

function startHeartRain(){
    const container=document.getElementById("hearts");
    setInterval(()=>{
        const heart=document.createElement("div");
        heart.classList.add("floatingHeart");
        heart.innerText="❤️";
        heart.style.left=Math.random()*100+"%";
        heart.style.bottom="0px";
        container.appendChild(heart);
        setTimeout(()=>heart.remove(),3000);
    },300);
}

function startCountdown(){
    let count=10;
    const el=document.getElementById("countdown");
    const interval=setInterval(()=>{
        el.innerHTML="Love explosion in "+count+"...";
        count--;
        if(count<0){
            clearInterval(interval);
            el.innerHTML="💥 LOVE OVERFLOW DETECTED 💥";
        }
    },1000);
}

</script>
</body>
</html>
