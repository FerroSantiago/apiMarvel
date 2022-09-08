<script>
    let value = ' '
    
    const handleInput = (event) => 
    value = event.target.value
    
    fetch('https://gateway.marvel.com:443/v1/public/characters?name=hulk&ts=1&apikey=8479630058c2db43f533ff3d17fb5646&hash=a8500480dfb36b9dda96150c305af8d9')
        .then(res => res.json())
        .then(json => {
            console.log(json, 'RES.JSON')
        })
</script>

<button on:dblclick={handleInput}>
    Search
</button>