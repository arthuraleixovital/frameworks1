<script>
    import Select from 'svelte-select';

    let moedas = [
        { nome: 'Dólar americano', código: 'USD'},
        { nome: 'Real brasileiro', código: 'BRL'},
        { nome: 'Euro', código: 'EUR'},
        { nome: 'Libra esterlina', código: 'GBP'},
        { nome: 'Iene japonês', código: 'JPY'},
        { nome: 'Peso argentino', código: 'ARS'}
    ];

    let código1 = $state(moedas[0].código);
    let código2 = $state(moedas[1].código);
    let valor1 = $state(0);
    let valor2 = $state(0);
    let moedaPadrao = $state();

    async function mudarMoeda() {
        const resposta = await fetch(`https://open.er-api.com/v6/latest/${código1}`);
        moedaPadrao = await resposta.json();
        converterDe();
    }

    function converterDe() {
        valor2 = (valor1 * moedaPadrao.rates[código2]).toFixed(2);
    }

    function converterPara() {
        valor1 = (valor2 / moedaPadrao.rates[código2]).toFixed(2);
    }

    function swap() {
        [código1, código2] = [código2, código1];
        [valor1, valor2] = [valor2, valor1];
        mudarMoeda();
    }
    mudarMoeda();
    function converterParaHorarioLocal(dataUTC) {
        if (!dataUTC) return "Data inválida";
        let data = new Date(dataUTC + " UTC");
        return data.toLocaleString();
    }
</script>

<div class="container">
    <h1 class="text-center">Cotação de moedas</h1>
    <div class="input-group">
        <select class="form-select" bind:value={código1} onchange={mudarMoeda} style="background-image:url({moedas})">
            {#each moedas as moeda}
                <option value={moeda.código} title={moeda.nome}>{moeda.código}</option>
            {/each}
        </select>
        <input placeholder="0,00" type="number" class="form-control w-25" oninput={converterDe} bind:value={valor1} />
        <button class="btn btn-outline-secondary" type="button" onclick={swap}>⇄</button>
        <input placeholder="0,00" type="number" class="form-control w-25" oninput={converterPara} bind:value={valor2} />
        <select class="form-select" bind:value={código2} onchange={converterPara}>
            {#each moedas as moeda}
                <option value={moeda.código} title={moeda.nome}>{moeda.código}</option>
            {/each}
        </select>
    </div>
    <br />
    <div style="text-align: center;">
        Cotação atual: 1 USD = <span style="color: green;">
            {moedaPadrao && moedaPadrao.rates[código2].toFixed(2)}
        </span>
        {código2}
        <br />
        <p>Última atualização: {moedaPadrao ? converterParaHorarioLocal(moedaPadrao.time_last_update_utc) : "Carregando..."}</p>
    </div>
    <div class="position-fixed bottom-0 end-0 m-3">
        <a href="https://www.exchangerate-api.com">Rates By Exchange Rate API</a>
    </div>
</div>

<style>
    .container {
        background-color: #f8f9fa;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        width: 100vh;
        height: 30vh;
        border-radius: 15px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        position: absolute;
        top: 30%;
        left: 25%;
    }
</style>
