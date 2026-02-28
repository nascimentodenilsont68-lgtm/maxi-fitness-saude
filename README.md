# maxi-fitness-saude
<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Maxi Fitness & Saúde</title>

<style>
body{
    font-family:'Segoe UI',sans-serif;
    margin:0;
    background:linear-gradient(135deg,#3BA6FF,#6EC6FF);
    display:flex;
    justify-content:center;
}

.app{
    background:#fff;
    width:100%;
    max-width:420px;
    min-height:100vh;
    border-radius:25px;
    box-shadow:0 20px 40px rgba(0,0,0,0.15);
    overflow:hidden;
}

header{
    background:#3BA6FF;
    color:white;
    text-align:center;
    padding:20px;
}

section{
    padding:20px;
}

.card{
    background:#f9fbff;
    padding:18px;
    border-radius:18px;
    box-shadow:0 6px 15px rgba(0,0,0,0.05);
    margin-bottom:20px;
}

h2{
    margin-top:0;
    font-size:18px;
    color:#3BA6FF;
}

input, select{
    width:100%;
    padding:10px;
    border-radius:10px;
    border:1px solid #ddd;
    margin-bottom:12px;
    font-size:14px;
}

button{
    width:100%;
    padding:12px;
    border:none;
    border-radius:12px;
    background:#3BA6FF;
    color:white;
    font-weight:bold;
    cursor:pointer;
    transition:0.3s;
}

button:hover{
    background:#2c8fe0;
}

.result-box{
    background:#e6f3ff;
    padding:12px;
    border-radius:12px;
    margin-top:10px;
    text-align:center;
}

.whatsapp{
    background:#25D366;
}

footer{
    text-align:center;
    font-size:11px;
    padding:15px;
    color:#777;
}
</style>
</head>

<body>

<div class="app">

<header>
<h1>Maxi Fitness & Saúde</h1>
<p>Drogaria Maxi Popular Delivery</p>
</header>

<section>

<!-- IMC -->
<div class="card">
<h2>Calculadora de IMC</h2>

<select id="genero">
<option>Masculino</option>
<option>Feminino</option>
</select>

<input type="number" id="idade" placeholder="Idade">
<input type="number" id="peso" placeholder="Peso (kg)">
<input type="number" step="0.01" id="altura" placeholder="Altura (m)">

<button onclick="calcularIMC()">Calcular IMC</button>

<div class="result-box" id="resultadoIMC"></div>
<div id="recomendacaoIMC"></div>
</div>

<!-- ÁGUA -->
<div class="card">
<h2>Consumo Diário de Água</h2>

<input type="number" id="pesoAgua" placeholder="Peso (kg)">

<select id="atividade">
<option value="0">Sedentário</option>
<option value="300">Atividade Moderada</option>
<option value="500">Atividade Intensa</option>
</select>

<button onclick="calcularAgua()">Calcular Água</button>

<div class="result-box" id="resultadoAgua"></div>
</div>

<!-- GASTO CALÓRICO PREMIUM -->
<div class="card">
<h2>🔥 Gasto Calórico por Exercício</h2>

<select id="generoCal">
<option>Masculino</option>
<option>Feminino</option>
</select>

<input type="number" id="idadeCal" placeholder="Idade">
<input type="number" id="pesoCal" placeholder="Peso (kg)">
<input type="number" id="tempoExercicio" placeholder="Tempo (minutos)">

<select id="tipoExercicio">
<option value="7">🏃 Aula Aeróbica</option>
<option value="9">🏃‍♂️ Corrida</option>
<option value="6">🏋️ Musculação</option>
<option value="8">🏊 Natação</option>
<option value="8.5">🥋 Artes Marciais</option>
<option value="7.5">🤸 Calistenia</option>
</select>

<button onclick="calcularCalorias()">Calcular Gasto</button>

<div class="result-box" id="resultadoCalorias"></div>

<div style="margin-top:15px;">
<div style="background:#eee;border-radius:12px;height:14px;overflow:hidden;">
<div id="barraCalorias" 
style="height:14px;width:0%;background:linear-gradient(90deg,#3BA6FF,#6EC6FF);border-radius:12px;transition:width 0.8s ease;">
</div>
</div>
</div>

<div id="nivelTreino" style="margin-top:10px;font-weight:bold;text-align:center;"></div>

<div id="recomendacaoCalorias"></div>

</div>

<!-- WHATSAPP -->
<div class="card">
<h2>Atendimento Personalizado</h2>
<button class="whatsapp" onclick="window.open('https://wa.me/5591984181227','_blank')">
Falar no WhatsApp
</button>
</div>

</section>

<footer>
Suplementos não substituem alimentação equilibrada e prática de exercícios físicos.
</footer>

</div>

<script>

function calcularIMC(){
let peso=parseFloat(document.getElementById("peso").value);
let altura=parseFloat(document.getElementById("altura").value);
let resultado=document.getElementById("resultadoIMC");

if(!peso||!altura){resultado.innerHTML="Preencha corretamente.";return;}

let imc=(peso/(altura*altura)).toFixed(1);
resultado.innerHTML=`IMC: ${imc}`;
}

function calcularAgua(){
let peso=parseFloat(document.getElementById("pesoAgua").value);
let atividade=parseInt(document.getElementById("atividade").value);
let resultado=document.getElementById("resultadoAgua");

if(!peso){resultado.innerHTML="Preencha o peso.";return;}

let total=((peso*35)+atividade)/1000;
resultado.innerHTML=`Consumo ideal: ${total.toFixed(2)} litros/dia`;
}

function calcularCalorias(){
let peso=parseFloat(document.getElementById("pesoCal").value);
let tempoMin=parseFloat(document.getElementById("tempoExercicio").value);
let met=parseFloat(document.getElementById("tipoExercicio").value);

let resultado=document.getElementById("resultadoCalorias");
let recomendacao=document.getElementById("recomendacaoCalorias");
let barra=document.getElementById("barraCalorias");
let nivel=document.getElementById("nivelTreino");

if(!peso||!tempoMin){resultado.innerHTML="Preencha peso e tempo.";return;}

let calorias=(met*peso*(tempoMin/60)).toFixed(0);
resultado.innerHTML=`🔥 ${calorias} kcal queimadas`;

let porcentagem=Math.min((calorias/1000)*100,100);
barra.style.width=porcentagem+"%";

if(calorias<300){nivel.innerHTML="Treino Leve 💪";}
else if(calorias<=600){nivel.innerHTML="Treino Moderado 🔥";}
else{nivel.innerHTML="Treino Intenso 🚀";}

if(calorias>=400){
recomendacao.innerHTML=`
<div class="result-box">
<strong>Morocorp:</strong> Suplemento com extrato de laranja moro, podendo auxiliar em programas de controle de peso.
</div>
<div class="result-box">
<strong>Slim Muv:</strong> Fórmula para suporte metabólico associado a hábitos saudáveis.
</div>
<div class="result-box">
<strong>Laranja Moro:</strong> Suplemento antioxidante que pode integrar estratégias nutricionais.
</div>
<button class="whatsapp" onclick="window.open('https://wa.me/5591984181227?text=Olá,%20quero%20informações%20sobre%20Morocorp,%20Slim%20Muv%20e%20Laranja%20Moro.','_blank')">
Falar com Atendente
</button>
`;
}else{
recomendacao.innerHTML=`
<button class="whatsapp" onclick="window.open('https://wa.me/5591984181227','_blank')">
Falar com Atendente
</button>
`;
}
}

</script>

</body>
</html>
