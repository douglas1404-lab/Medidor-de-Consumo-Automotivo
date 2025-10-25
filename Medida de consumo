<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Cálculo de Rendimento do Automóvel</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background: #f3f4f6;
    margin: 0;
    padding: 20px;
    display: flex;
    justify-content: center;
  }
  .container {
    background: #fff;
    width: 100%;
    max-width: 420px;
    border-radius: 15px;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
    padding: 20px;
  }
  h2 {
    text-align: center;
    color: #333;
  }
  label {
    display: block;
    margin-top: 15px;
    color: #333;
    font-weight: bold;
  }
  input {
    width: 100%;
    padding: 10px;
    margin-top: 5px;
    border-radius: 8px;
    border: 1px solid #ccc;
    font-size: 1em;
  }
  button {
    margin-top: 20px;
    width: 100%;
    background-color: #2563eb;
    color: white;
    padding: 12px;
    border: none;
    border-radius: 10px;
    font-size: 1em;
    cursor: pointer;
  }
  button:hover {
    background-color: #1d4ed8;
  }
  .resultado {
    margin-top: 25px;
    background: #e5e7eb;
    padding: 15px;
    border-radius: 10px;
    font-size: 1.1em;
  }
  .historico {
    margin-top: 25px;
  }
  .item-historico {
    background: #f9fafb;
    border: 1px solid #d1d5db;
    border-radius: 10px;
    padding: 10px;
    margin-bottom: 10px;
    font-size: 0.95em;
  }
  .limpar-btn {
    background-color: #dc2626;
    margin-top: 10px;
  }
  .limpar-btn:hover {
    background-color: #b91c1c;
  }
</style>
</head>
<body>
<div class="container">
  <h2>Rendimento do Automóvel</h2>

  <label for="kmInicio">Km ao abastecer:</label>
  <input type="number" id="kmInicio" placeholder="Ex: 25320.5" step="0.1">

  <label for="kmFinal">Km após rodar:</label>
  <input type="number" id="kmFinal" placeholder="Ex: 25580.7" step="0.1">

  <label for="litros">Litros abastecidos:</label>
  <input type="number" id="litros" placeholder="Ex: 25" step="0.01">

  <label for="valorCombustivel">Valor do combustível (R$/L):</label>
  <input type="number" id="valorCombustivel" placeholder="Ex: 5.89" step="0.01">

  <button onclick="calcular()">Calcular</button>

  <div class="resultado" id="resultado"></div>

  <div class="historico" id="historico">
    <h3>📜 Histórico de Abastecimentos</h3>
    <div id="listaHistorico"></div>
    <button class="limpar-btn" onclick="limparHistorico()">🗑️ Limpar Histórico</button>
  </div>
</div>

<script>
function calcular() {
  const kmInicio = parseFloat(document.getElementById("kmInicio").value);
  const kmFinal = parseFloat(document.getElementById("kmFinal").value);
  const litros = parseFloat(document.getElementById("litros").value);
  const valorCombustivel = parseFloat(document.getElementById("valorCombustivel").value);

  if (isNaN(kmInicio) || isNaN(kmFinal) || isNaN(litros) || isNaN(valorCombustivel) || kmFinal <= kmInicio || litros <= 0) {
    document.getElementById("resultado").innerHTML = "⚠️ Por favor, insira valores válidos.";
    return;
  }

  const kmRodado = kmFinal - kmInicio;
  const rendimento = kmRodado / litros;
  const custoPorKm = (litros * valorCombustivel) / kmRodado;

  const data = new Date().toLocaleDateString('pt-BR');
  const resultado = {
    data,
    kmInicio,
    kmFinal,
    kmRodado,
    litros,
    valorCombustivel,
    rendimento: rendimento.toFixed(2),
    custoPorKm: custoPorKm.toFixed(2)
  };

  salvarNoHistorico(resultado);

  document.getElementById("resultado").innerHTML = `
    🚗 <b>Rendimento:</b> ${rendimento.toFixed(2)} km/L<br>
    💰 <b>Custo por km rodado:</b> R$ ${custoPorKm.toFixed(2)}
  `;
}

function salvarNoHistorico(dados) {
  let historico = JSON.parse(localStorage.getItem("historicoAbastecimento")) || [];
  historico.unshift(dados); // adiciona no início
  localStorage.setItem("historicoAbastecimento", JSON.stringify(historico));
  exibirHistorico();
}

function exibirHistorico() {
  const lista = document.getElementById("listaHistorico");
  const historico = JSON.parse(localStorage.getItem("historicoAbastecimento")) || [];

  if (historico.length === 0) {
    lista.innerHTML = "<p>Nenhum registro salvo.</p>";
    return;
  }

  lista.innerHTML = historico.map(item => `
    <div class="item-historico">
      📅 <b>${item.data}</b><br>
      Km inicial: ${item.kmInicio} | Km final: ${item.kmFinal}<br>
      Rodou: ${item.kmRodado.toFixed(1)} km<br>
      Combustível: ${item.litros} L @ R$${item.valorCombustivel}/L<br>
      🚗 ${item.rendimento} km/L — 💰 R$ ${item.custoPorKm}/km
    </div>
  `).join("");
}

function limparHistorico() {
  if (confirm("Tem certeza que deseja apagar todo o histórico?")) {
    localStorage.removeItem("historicoAbastecimento");
    exibirHistorico();
  }
}

window.onload = exibirHistorico;
</script>
</body>
</html>
