<script>
    import { each } from "svelte/internal";
    import Carga from "./Carga.svelte";

    let value = "";
    let response = undefined;
    let loading = false;

    const handleInput = (event) => (value = event.target.value);

    $: if (loading == true) {
        fetch(
            `https://gateway.marvel.com:443/v1/public/characters?ts=1&name=${value.trim()}&apikey=8479630058c2db43f533ff3d17fb5646&hash=a8500480dfb36b9dda96150c305af8d9`
        )
            .then((res) => res.json())
            .then((json) => {
                response = json.data.results || [];
                loading = false;
                console.log(response);
            });
        
    }
    function buscar() {
        loading = true;
    }
</script>

<input placeholder="Elige el héroe..." {value} on:input={handleInput} />

<button on:click={buscar}> Buscar </button>

{#if loading}
    <Carga></Carga>
{:else }
    {#if response && response.length > 0}
        {#each response as personaje}
            <div>
                <br><strong class="titulos">{personaje.name}</strong>
            </div>
            <div>
                {personaje.description}
            </div>
            <article>
                <img
                    alt={personaje.description}
                    src="{personaje.thumbnail.path}.{personaje.thumbnail.extension}"
                />
            </article>
        {/each}
    {/if}
    {#if response && response.length == 0}
        <strong>Sin resultados...</strong>
    {/if}
{/if}
