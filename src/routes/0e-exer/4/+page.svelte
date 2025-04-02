<script>
    let idPostagem = $state("");
    let postagem = $state(null);
    let comentarios = $state([]);

    async function buscarPostagem() {
        if (!idPostagem) return;
        let resposta = await fetch(`https://jsonplaceholder.typicode.com/posts/${idPostagem}`);
        postagem = await resposta.json();

        let resposta2 = await fetch(`https://jsonplaceholder.typicode.com/posts/${idPostagem}/comments`);
        comentarios = await resposta2.json();
    }
</script>

<input type="number" placeholder="ID da postagem" bind:value={idPostagem} />
<button onclick={buscarPostagem}>Buscar postagem</button>
<br />

{#if postagem}
    <h2>{postagem.title}</h2>
{/if}