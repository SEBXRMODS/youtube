<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>No te metas con Karen</title>

<link
rel="stylesheet"
href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"
/>

<style>

body{
background:black;
color:#00ff88;
font-family:Consolas;
margin:0;
padding:20px;
}

.card{
max-width:700px;
margin:auto;
border:2px solid #00ff88;
padding:25px;
border-radius:15px;
box-shadow:0 0 25px #00ff88;
background:rgba(0,0,0,0.9);
animation:glow 2s infinite alternate;
}

h1{
text-align:center;
font-size:40px;
text-shadow:0 0 20px #00ff88;
margin-bottom:30px;
}

p{
font-size:18px;
margin:12px 0;
word-break:break-word;
}

#map{
height:400px;
margin-top:20px;
border-radius:10px;
overflow:hidden;
border:2px solid #00ff88;
}

@keyframes glow{
from{
box-shadow:0 0 10px #00ff88;
}
to{
box-shadow:0 0 30px #00ff88;
}
}

</style>

</head>
<body>

<div class="card">

<h1>NO TE METAS CON KAREN</h1>

<p id="ip">🌐 Cargando IP...</p>

<p id="pais">🌍 Cargando país...</p>

<p id="ciudad">🏙 Cargando ciudad...</p>

<p id="device">📱 Detectando dispositivo...</p>

<p id="browser">🖥 Detectando navegador...</p>

<p id="hora">🕒 Cargando hora...</p>

<div id="map"></div>

</div>

<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<script>

async function obtenerInfo(){

const res = await fetch("https://ipapi.co/json/");

const data = await res.json();

let dispositivo = "PC";

if(/Android/i.test(navigator.userAgent)){
dispositivo = "Android";
}

if(/iPhone|iPad|iPod/i.test(navigator.userAgent)){
dispositivo = "iPhone";
}

document.getElementById("ip").innerHTML =
"🌐 IP: " + data.ip;

document.getElementById("pais").innerHTML =
"🌍 País: " + data.country_name;

document.getElementById("ciudad").innerHTML =
"🏙 Ciudad: " + data.city;

document.getElementById("device").innerHTML =
"📱 Dispositivo: " + dispositivo;

document.getElementById("browser").innerHTML =
"🖥 Navegador: " + navigator.userAgent;

document.getElementById("hora").innerHTML =
"🕒 Hora: " + new Date().toLocaleString();


// MAPA

const map = L.map('map').setView([
data.latitude,
data.longitude
], 10);

L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
attribution: '&copy; OpenStreetMap'
}).addTo(map);

L.marker([
data.latitude,
data.longitude
]).addTo(map)
.bindPopup("Ubicación detectada")
.openPopup();

}

obtenerInfo();

</script>

</body>
</html>
