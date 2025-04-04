<script>

    let seg = $state(10);
    let tempo = 0;
    let bloqueado = $state(false);
    let contador = $state();

    function transformar() {
        tempo = seg;
        contador = seg;
        bloquear();
    }

    async function bloquear() {
        bloqueado = true;
        while (contador > 0) {
            await new Promise(resolve => setTimeout(resolve, 1000));
            contador--;
        }
        soltarconfete();
        bloqueado = false;
    }

    function soltarconfete(){
        confetti({
            particleCount: 200, // Quantidade de partículas
            spread: 70, // Abertura do confete
            origin: { y: 0.6 } // Origem do confete (altura relativa)
        });
    }
</script>

<svelte:head>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
</svelte:head>

<div class="container">
    <div class="card">
        <h4>Tempo restante: {contador}s</h4>
        <div class="input-group">
            <input type="number" min="1" placeholder="Segundos" bind:value={seg} disabled={bloqueado} class="form-control" />
        </div>
        <button class="btn btn-primary" onclick={transformar} disabled={bloqueado}>Iniciar Contagem</button>
        <br>
        {#if contador <= 0}
        <h1><b>Parábens</b></h1>
        {/if}
    </div>
</div>

<style>
    .container {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 100vh;
        background-color: #ffffff;
    }
    .card {
        padding: 20px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        border-radius: 8px;
        background: white;
        text-align: center;
    }
    .input-group {
        margin: 10px 0;
    }
    button {
        width: 100%;
    }
</style>