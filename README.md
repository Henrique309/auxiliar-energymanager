# auxiliar-energymanager
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Auxiliar EnergyManager</title>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: Arial, sans-serif;
}

body {
  background: #0b1220;
  color: #fff;
  min-height: 100vh;
}

header {
  background: linear-gradient(135deg, #0f766e, #16a34a);
  padding: 22px 18px;
  text-align: center;
  border-radius: 0 0 22px 22px;
}

header h1 {
  font-size: 24px;
}

header p {
  margin-top: 6px;
  opacity: .9;
  font-size: 13px;
}

.container {
  padding: 15px;
  max-width: 700px;
  margin: auto;
}

.card {
  background: #151f31;
  border: 1px solid #26334a;
  border-radius: 16px;
  padding: 16px;
  margin-bottom: 14px;
  box-shadow: 0 5px 20px rgba(0,0,0,.18);
}

.card h2 {
  font-size: 17px;
  margin-bottom: 13px;
}

.stats {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 10px;
}

.stat {
  background: #0f172a;
  border-radius: 13px;
  padding: 13px;
}

.stat span {
  display: block;
  color: #94a3b8;
  font-size: 12px;
  margin-bottom: 5px;
}

.stat strong {
  font-size: 18px;
}

input, select {
  width: 100%;
  padding: 12px;
  margin: 6px 0 10px;
  border-radius: 10px;
  border: 1px solid #334155;
  background: #0f172a;
  color: white;
  outline: none;
}

button {
  width: 100%;
  padding: 13px;
  border: none;
  border-radius: 11px;
  background: #16a34a;
  color: white;
  font-weight: bold;
  cursor: pointer;
  margin-top: 5px;
}

button:active {
  transform: scale(.98);
}

.btn-secondary {
  background: #334155;
}

.btn-danger {
  background: #dc2626;
}

.recommendation {
  border-left: 4px solid #22c55e;
  background: #0f172a;
  padding: 13px;
  border-radius: 10px;
  line-height: 1.5;
}

.good {
  color: #4ade80;
}

.warning {
  color: #facc15;
}

.bad {
  color: #f87171;
}

.plant {
  background: #0f172a;
  padding: 13px;
  border-radius: 12px;
  margin-bottom: 9px;
  border: 1px solid #273449;
}

.plant-title {
  display: flex;
  justify-content: space-between;
  margin-bottom: 7px;
}

.progress {
  height: 8px;
  background: #273449;
  border-radius: 10px;
  overflow: hidden;
  margin-top: 8px;
}

.progress div {
  height: 100%;
  background: #22c55e;
}

.small {
  color: #94a3b8;
  font-size: 12px;
}

.hidden {
  display: none;
}

footer {
  text-align: center;
  padding: 20px;
  color: #64748b;
  font-size: 12px;
}

nav {
  position: sticky;
  bottom: 0;
  background: #111827;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  padding: 7px;
  border-top: 1px solid #26334a;
}

nav button {
  background: transparent;
  margin: 0;
  font-size: 11px;
  padding: 9px 3px;
}

nav button.active {
  background: #16a34a;
  border-radius: 9px;
}

.section {
  display: none;
}

.section.active {
  display: block;
}
</style>
</head>

<body>

<header>
  <h1>⚡ Auxiliar EnergyManager</h1>
  <p>Seu assistente para administrar sua companhia de energia</p>
</header>

<div class="container">

<!-- DASHBOARD -->
<section id="dashboard" class="section active">

  <div class="card">
    <h2>📊 Visão geral</h2>

    <div class="stats">

      <div class="stat">
        <span>💰 Dinheiro</span>
        <strong id="saldo">R$ 0</strong>
      </div>

      <div class="stat">
        <span>⚡ Produção</span>
        <strong id="producao">0 MW</strong>
      </div>

      <div class="stat">
        <span>📈 Receita/h</span>
        <strong id="receita">R$ 0</strong>
      </div>

      <div class="stat">
        <span>🏭 Usinas</span>
        <strong id="quantidadeUsinas">0</strong>
      </div>

    </div>
  </div>

  <div class="card">
    <h2>🤖 Recomendação do auxiliar</h2>

    <div class="recommendation" id="recomendacao">
      Preencha os dados da sua companhia para receber uma recomendação.
    </div>
  </div>

  <div class="card">
    <h2>🎯 Próximo objetivo</h2>

    <div id="objetivo">
      Cadastre sua primeira usina.
    </div>
  </div>

</section>


<!-- COMPANHIA -->
<section id="companhia" class="section">

  <div class="card">
    <h2>🏢 Minha companhia</h2>

    <label>Nome da companhia</label>
    <input id="nomeEmpresa" placeholder="Ex.: Voltix Energia">

    <label>Saldo atual</label>
    <input id="saldoInput" type="number" placeholder="Ex.: 100000">

    <label>Demanda/mercado atual (MW)</label>
    <input id="demandaInput" type="number" placeholder="Ex.: 500">

    <button onclick="salvarCompanhia()">
      💾 Salvar dados
    </button>
  </div>

</section>


<!-- USINAS -->
<section id="usinas" class="section">

  <div class="card">

    <h2>🏭 Adicionar usina</h2>

    <label>Nome</label>
    <input id="nomeUsina" placeholder="Ex.: Usina Solar 1">

    <label>Tipo</label>

    <select id="tipoUsina">
      <option value="Solar">☀️ Solar</option>
      <option value="Eolica">🌬️ Eólica</option>
      <option value="Hidreletrica">💧 Hidrelétrica</option>
      <option value="Termica">🔥 Térmica</option>
      <option value="Nuclear">☢️ Nuclear</option>
    </select>

    <label>Produção (MW)</label>
    <input id="mwUsina" type="number">

    <label>Receita por hora (R$)</label>
    <input id="receitaUsina" type="number">

    <button onclick="adicionarUsina()">
      ➕ Adicionar usina
    </button>

  </div>

  <div class="card">
    <h2>📋 Minhas usinas</h2>
    <div id="listaUsinas"></div>
  </div>

</section>


<!-- INVESTIMENTOS -->
<section id="investimentos" class="section">

  <div class="card">

    <h2>💰 Simulador de investimento</h2>

    <label>Valor do investimento</label>
    <input id="investimento" type="number">

    <label>Produção adicional (MW)</label>
    <input id="investimentoMW" type="number">

    <label>Receita adicional por hora</label>
    <input id="investimentoReceita" type="number">

    <button onclick="analisarInvestimento()">
      🔎 Analisar investimento
    </button>

  </div>

  <div class="card">
    <h2>🤖 Análise</h2>

    <div class="recommendation" id="analiseInvestimento">
      Informe os valores acima.
    </div>
  </div>

</section>


<!-- ALIANÇAS -->
<section id="aliancas" class="section">

  <div class="card">

    <h2>🤝 Alianças</h2>

    <label>Nome da aliança</label>
    <input id="nomeAlianca" placeholder="Ex.: Grandes Energias">

    <label>Nível/força da aliança</label>
    <input id="forcaAlianca" type="number">

    <button onclick="adicionarAlianca()">
      🤝 Adicionar aliança
    </button>

  </div>

  <div class="card">

    <h2>📋 Minhas alianças</h2>

    <div id="listaAliancas"></div>

  </div>

</section>

</div>


<nav>

  <button class="active" onclick="mostrar('dashboard', this)">
    🏠<br>Início
  </button>

  <button onclick="mostrar('companhia', this)">
    🏢<br>Companhia
  </button>

  <button onclick="mostrar('usinas', this)">
    🏭<br>Usinas
  </button>

  <button onclick="mostrar('investimentos', this)">
    💰<br>Investir
  </
