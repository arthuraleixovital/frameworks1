<script>
    let emailuser = $state("");
    let emailsfiltrados = $state("");
    let titpostemailfiltrados = $state("");

    async function buscuseremail() {
        let resposta6 = await fetch(`https://jsonplaceholder.typicode.com/users`);
        let allUsers = await resposta6.json();

        emailsfiltrados = allUsers.filter(emailsfiltrados => emailsfiltrados.email === emailuser);
        let idusere = emailsfiltrados[0].id;

        let resposta7 = await fetch(`https://jsonplaceholder.typicode.com/posts/${idusere}`)
        titpostemailfiltrados = await resposta7.json();
    }
</script>

<input type="text" placeholder="Buscar posts por email" bind:value={emailuser} />
<button onclick={buscuseremail}>Buscar posts por email</button>

<br />

{#if titpostemailfiltrados}
    <h2>Posts do usuário por e-mail</h2>
    {titpostemailfiltrados.title}
{/if}
