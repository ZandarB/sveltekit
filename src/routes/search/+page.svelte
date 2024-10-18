<script>
let userInput = '';
let operatorData = '';

async function getOperators(name)
{
    const response = await fetch(`https://api.rhodesapi.com/api/operator/${name}/`);
   
    if (response.ok)
    {
        const data = await response.json();
        console.log(data.name);
    }
    else
    {
        console.log("Error Fetching Operators")
    }
}

function search()
{
    if (userInput){
        getOperators(userInput)
    }
    else
    {
        operatorData = 'Please Enter A Valid Name';
    }
}


getOperators();
</script>


<label for="textbox">Search for Operators</label>
<br>
<input
    id="textbox"
    type="text"
    bind:value={userInput}
    placeholder="Enter an Operators Name"
/>
<br>
<button class="search" on:click={search}>Click to Search</button>
<p class ="operators">{operatorData}</p>


<style>

.search{
    margin: 10px;
}

.textbox{
    margin: 10px;
}
</style>