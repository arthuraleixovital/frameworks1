<script>
    let usuarios = $state([]);
    
    async function buscusers() {
        let resposta3 = await fetch(`https://jsonplaceholder.typicode.com/users`);
        usuarios = await resposta3.json();
    }
</script>
<button onclick={buscusers}>Buscar usuários</button>

{#if usuarios.length > 0}
    <h2>Usuários</h2>
    {#each usuarios as usuario}
        <ul>
            <li>
                <p>{usuario.name}</p>
            </li>
        </ul>
    {/each}
{/if}