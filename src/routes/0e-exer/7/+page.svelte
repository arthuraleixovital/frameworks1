<script>
    let city = $state();
    let users = $state();

    async function buscarcidademetodo2() {
        let res = await fetch(`https://jsonplaceholder.typicode.com/users?address.city=${city}`);
        users = await res.json();
    }
</script>

<input type="text" placeholder="Buscar usuarios por cidade" bind:value={city} />
<button onclick={buscarcidademetodo2}>Buscar usuarios por cidade</button>
<br />

{#each users as user}
   <p>{user.name}</p>
{/each}