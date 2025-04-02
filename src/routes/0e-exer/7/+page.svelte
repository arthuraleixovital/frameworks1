<script>
    let emailuser = $state("");
    let emailsfiltrados = $state("");
    let titpostemailfiltrados = $state(null);
    let cidadeuser = $state("");
    let usercity = $state({name:""});

    async function buscuseremail() {
        let resposta6 = await fetch(`https://jsonplaceholder.typicode.com/users`);
        let allUsers = await resposta6.json();

        emailsfiltrados = allUsers.filter(emailsfiltrados => emailsfiltrados.email === emailuser);
        let idusere = emailsfiltrados[0].id;

        let resposta7 = await fetch(`https://jsonplaceholder.typicode.com/posts/${idusere}`)
        titpostemailfiltrados = await resposta7.json();
    }

    async function buscarcidade() {
        let resposta8 = await fetch(`https://jsonplaceholder.typicode.com/users`);
        let allUsers = await resposta8.json();

        let cidadefiltrada = allUsers.filter(cidadefiltrada => cidadefiltrada.address.city === cidadeuser);
        usercity = cidadefiltrada[0];
        console.log(usercity);
        //não está funcionando
    }
</script>

<input type="text" placeholder="Buscar usuarios por cidade" bind:value={cidadeuser} />
<button onclick={buscarcidade}>Buscar usuarios por cidade</button>
<br />

{usercity.name}