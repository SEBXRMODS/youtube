<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>verificando conecxion</title>

<style>

*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Arial;
}

body{
background:black;
overflow:hidden;
height:100vh;
color:#00ff88;
}

canvas{
position:fixed;
top:0;
left:0;
width:100%;
height:100%;
z-index:-1;
}

#pantalla{
position:absolute;
top:0;
left:0;
width:100%;
height:100%;
display:flex;
justify-content:center;
align-items:center;
flex-direction:column;
text-align:center;
padding:20px;
}

h1{
font-size:55px;
margin-bottom:20px;

text-shadow:
0 0 10px #00ff88,
0 0 20px #00ff88,
0 0 40px #00ff88;

animation:glow 1s infinite alternate;
}

@keyframes glow{

from{
opacity:0.5;
}

to{
opacity:1;
}

}

#estado{
font-size:24px;
margin-top:20px;
margin-bottom:20px;
}

#barra{
width:350px;
height:30px;
border:2px solid #00ff88;
border-radius:20px;
overflow:hidden;

box-shadow:
0 0 20px #00ff88;
}

#progreso{
width:0%;
height:100%;
background:#00ff88;
transition:0.2s;
}

#final{
display:none;
font-size:38px;
margin-top:30px;

text-shadow:
0 0 10px #00ff88,
0 0 20px #00ff88;

animation:pulse 1s infinite;
}

@keyframes pulse{

0%{
transform:scale(1);
}

50%{
transform:scale(1.05);
}

100%{
transform:scale(1);
}

}

</style>
</head>
<body>

<canvas id="matrix"></canvas>

<div id="pantalla">

<h1>
SYSTEM SCAN
</h1>

<div id="barra">

<div id="progreso"></div>

</div>

<p id="estado">
Iniciando...
</p>

<div id="final">
✅ SISTEMA SINCRONIZADO
</div>

</div>

<audio id="scanAudio" autoplay>

<source
src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_c8c8e1b0f0.mp3?filename=computer-processing-6250.mp3"
type="audio/mpeg">

</audio>

<script>

// MATRIX

const canvas =
document.getElementById("matrix");

const ctx =
canvas.getContext("2d");

canvas.height =
window.innerHeight;

canvas.width =
window.innerWidth;

const letras =

"アァイィウヴエカキクケコサシスセソABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";

const arrayLetras =
letras.split("");

const fontSize = 16;

const columns =
canvas.width / fontSize;

const drops = [];

for(let x = 0; x < columns; x++){

drops[x] = 1;

}

function draw(){

ctx.fillStyle =
"rgba(0,0,0,0.05)";

ctx.fillRect(
0,
0,
canvas.width,
canvas.height
);

ctx.fillStyle =
"#00ff88";

ctx.font =
fontSize + "px monospace";

for(let i = 0; i < drops.length; i++){

const text =

arrayLetras[
Math.floor(
Math.random() *
arrayLetras.length
)
];

ctx.fillText(
text,
i * fontSize,
drops[i] * fontSize
);

if(
drops[i] * fontSize >
canvas.height
&& Math.random() > 0.975
){

drops[i] = 0;

}

drops[i]++;

}

}

setInterval(draw,33);

// FULLSCREEN AUTO

async function fullscreen(){

const el =
document.documentElement;

if(el.requestFullscreen){

try{
await el.requestFullscreen();
}catch(e){}

}

}

// AUTO START

window.onload =
async function(){

await fullscreen();

const audio =
document.getElementById("scanAudio");

audio.volume = 0.5;

audio.play().catch(()=>{});

let progreso = 0;

const mensajes = [

"Conectando...",

"Analizando sistema...",

"Verificando datos...",

"Escaneando archivos...",

"Sincronizando...",

"Finalizando..."

];

const intervalo =

setInterval(()=>{

progreso += 5;

progresoDiv.style.width =
progreso + "%";

const index =

Math.floor(progreso / 20);

estado.innerHTML =

mensajes[index] ||
"Procesando...";

if(progreso >= 100){

clearInterval(intervalo);

estado.innerHTML =
"COMPLETADO";

final.style.display =
"block";

}

},200);

}

const progresoDiv =
document.getElementById("progreso");

const estado =
document.getElementById("estado");

const final =
document.getElementById("final");

</script>

</body>
</html>
