<script>
    let iduser = $state("");
    let user = $state(null);
    let titpostuser = $state(null);
    
    async function buscuserid() {
        if (!iduser) return;
        let resposta4 = await fetch(`https://jsonplaceholder.typicode.com/users/${iduser}`);
        user = await resposta4.json();

        let resposta5 = await fetch(`https://jsonplaceholder.typicode.com/posts/${iduser}`);
        titpostuser = await resposta5.json();
    }
</script>

<input type="number" placeholder="Buscar usuário por ID" bind:value={iduser} />
<button onclick={buscuserid}>Buscar usuário</button>
<br />

{#if user}
    <h2>Usuário</h2>
    <p>{user.name}</p>
{/if}

{#if titpostuser}
    <h2>Título da Postagem</h2>
    <p>{titpostuser.title}</p>
{/if}
