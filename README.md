<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Para Ti</title>

<style>
body{
margin:0;
font-family:"Segoe UI",sans-serif;
background:black;
color:white;
overflow:hidden;
}

/* FONDO */
.fondo{
position:fixed;
width:100%;
height:100%;
background:radial-gradient(circle at center,#2b0030,#000);
z-index:-1;
}

/* PARTICULAS */
.particula{
position:absolute;
color:rgba(255,255,255,0.3);
animation:flotar 8s linear infinite;
pointer-events:none;
}

@keyframes flotar{
0%{top:100%;opacity:0;}
50%{opacity:1;}
100%{top:-10%;opacity:0;}
}

/* INTRO */
#intro{
position:fixed;
width:100%;
height:100%;
display:flex;
flex-direction:column;
justify-content:center;
align-items:center;
cursor:pointer;
}

/* ESCENA */
#escena{
position:fixed;
width:100%;
height:100%;
display:none;
justify-content:center;
align-items:center;
cursor:pointer;
padding:20px;
}

#frase{
font-size:34px;
max-width:800px;
text-align:center;
line-height:1.5;
font-weight:700;
text-shadow:0 0 10px rgba(255,255,255,0.25);
}

/* FINAL */
#final{
display:none;
text-align:center;
padding:40px 20px;
}

#fotofinal{
max-width:320px;
border-radius:20px;
margin-top:20px;
box-shadow:0 0 30px rgba(255,255,255,0.3);
opacity:0;
animation:aparecer 2s forwards;
}

@keyframes aparecer{
from{opacity:0;transform:scale(0.8);}
to{opacity:1;transform:scale(1);}
}

/* BOTONES */
.opciones{
margin-top:20px;
position:relative;
height:120px;
}

.opciones button{
padding:12px 28px;
font-size:18px;
border:none;
border-radius:14px;
cursor:pointer;
background:#ff4da6;
color:white;
transition:0.3s;
position:absolute;
}

#btnSi{left:30%;}
#btnNo{left:55%;}

#respuesta{
margin-top:25px;
font-size:22px;
}
</style>
</head>

<body>

<div class="fondo"></div>

<div id="intro">
<h1>IYARI...</h1>
<p>Toca la pantalla</p>
</div>

<div id="escena">
<div id="frase"></div>
</div>

<div id="final">
<h1>ERES LA UNICA PERSONA QUE DESEO A MI LADO EN MI VIDA</h1>

<p style="max-width:700px;margin:auto;font-size:24px;">
Sentimientos que permanecen cuando te veo y cuando te vas.
Cuando nuestras miradas se encuentran y cuando saben que deben esperar para volver a verse.
</p>

<img id="fotofinal" src="fotofinal.jpg">

<h2>¿Serias mi San Valentin este año y los siguientes?</h2>

<div class="opciones">
<button id="btnSi" onclick="respuestaSi()">Si</button>
<button id="btnNo">No</button>
</div>

<div id="respuesta"></div>
</div>

<audio id="musica" loop>
<source src="Mi Iyari.mp3" type="audio/mpeg">
</audio>

<script>

/* MUSICA */
let musica=document.getElementById("musica");
musica.volume=0.05;

document.addEventListener("click",()=>{
if(musica.volume<0.9){
musica.volume+=0.05;
}
});

/* VIBRAR */
function vibrar(){
if(navigator.vibrate){
navigator.vibrate(40);
}
}

/* PARTICULAS */
setInterval(()=>{
let p=document.createElement("div");
p.className="particula";
let simbolos=["♡","❤","✦","✧"];
p.innerHTML=simbolos[Math.floor(Math.random()*simbolos.length)];
p.style.left=Math.random()*100+"vw";
p.style.fontSize=(10+Math.random()*20)+"px";
document.body.appendChild(p);
setTimeout(()=>p.remove(),8000);
},300);

/* FRASES ORIGINALES */
let frases=[
"Desde que te vi, fue mi mirada la que se clavó en ti.",
"Cuando te despediste, fue tu rostro el que permaneció en mí.",
"Cuando te volví a ver, fue mi corazón el que se encontró alterado.",
"Cuando te fuiste, fue mi cuerpo el que quería volver a sentir el tuyo a mi lado."
];

let actual=0;
let frase=document.getElementById("frase");

let escribiendo=false;
let timer;

/* ESCRITURA CORREGIDA */
function escribirTexto(texto){

clearTimeout(timer);
frase.textContent="";
let i=0;
escribiendo=true;

function escribir(){

if(i<texto.length){
frase.textContent+=texto[i];
i++;
timer=setTimeout(escribir,35);
}else{
escribiendo=false;
}

}

escribir();
}

/* INICIO */
document.getElementById("intro").onclick=function(){
this.style.display="none";
document.getElementById("escena").style.display="flex";
musica.play();
vibrar();
escribirTexto(frases[actual]);
};

/* AVANZAR SOLO SI TERMINO DE ESCRIBIR */
document.getElementById("escena").onclick=function(){

if(escribiendo) return;

vibrar();
actual++;

if(actual<frases.length){
escribirTexto(frases[actual]);
}else{
this.style.display="none";
document.getElementById("final").style.display="block";
}

};

/* BOTON NO ESCAPA */
let btnNo=document.getElementById("btnNo");

btnNo.addEventListener("mouseover",moverNo);
btnNo.addEventListener("touchstart",moverNo);

function moverNo(){
btnNo.style.left=Math.random()*70+"%";
btnNo.style.top=Math.random()*60+"%";
vibrar();
}

/* RESPUESTA SI❤ */
function respuestaSi(){
vibrar();
document.getElementById("respuesta").textContent="Acercate... besame.";
btnNo.style.display="none";
}

</script>

</body>
</html>
