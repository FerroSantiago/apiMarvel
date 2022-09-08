<script>
    let value = " "
    let response = []
    let loading = false

    const handleInput = (event) => 
        value = event.target.value

    $: if (value.length > 2){
        loading = true
        fetch(`https://gateway.marvel.com:443/v1/public/characters?name=${value}&ts=1&apikey=8479630058c2db43f533ff3d17fb5646&hash=a8500480dfb36b9dda96150c305af8d9`)
        .then(res => res.json())
        .then(json => {
            response = json.Search || []
            loading = false
        })
    }
</script>

<input
    placeholder="Elige el héroe..."
    value={value} 
    on:input={handleInput} 
/>

{#if loading}
<strong>Cargando...</strong>>
{/if}

{
    response.length > 0
        ? 'Se encontro el heroe'
        : 'No se encontro al heroe'
}