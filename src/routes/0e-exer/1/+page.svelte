<script>
    let seg = 10;
    let tempo = 0;
    let bloqueado = false;
    let contador = 0;

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
        bloqueado = false;
    }
</script>

<p>{`Tempo restante: ${contador}s`}</p>
{#if (bloqueado == false)}
<input type="number" min="1" placeholder="segundos" bind:value={seg} disabled={bloqueado} />
<button onclick={transformar} disabled={bloqueado}>Iniciar Contagem</button>
{/if}