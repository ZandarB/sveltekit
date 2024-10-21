<script>
import Footer from '$lib/Footer.svelte';
import Header from '$lib/Header.svelte';
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

<div class="background"></div>

<div class="content">
    <Header headingTitle = "Search AK Operators"/>
    <div class = "search">
        <h2 for="textbox">Search for Operators</h2>
        <br>
        <input
            id="textbox"
            type="text"
            bind:value={userInput}
            placeholder="Enter an Operator's Name"
        />
        <br>
        <button class="search" on:click={search}>Click to Search</button>
        <p class="operators">{operatorData}</p>
    </div>
    <Footer/>
</div>


<style>

.search{
    margin: px;
}
.background {
    background-image: url('/bg.png');
        background-size: cover;
        background-position: center;
        height: 100vh;
        width: 100vw; 
        position: absolute; 
        top: 0;
        left: 0;
        z-index: -1;
    }

.content {
    position: relative;
    z-index: 1;
    color: white;
}

.search {
    margin: 10px;
    text-align: center;
}
</style>