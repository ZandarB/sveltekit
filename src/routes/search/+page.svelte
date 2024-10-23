<script>
import Footer from '$lib/Footer.svelte';
import Header from '$lib/Header.svelte';


let userInput = '';
let operatorData = '';
let operatorClass = [,,,];

async function getOperators(name)
{
    const response = await fetch(`https://api.rhodesapi.com/api/operator/${name}/`);
   
    if (response.ok)
    {
        const data = await response.json();
        console.log(data);
        operatorClass = data.class;
        operatorData = data;
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


<div class="content">
    <Header headingTitle = "Search AK Operators"/>
    <div class = "searchbar">
        <h2 for="textbox">Search for Operators</h2>
        <br>
        <input
            id="textbox"
            type="text"
            bind:value={userInput}
            placeholder="Please enter an Operator's Name"
        />
        <br>
        <button class="searchbutton" on:click={search}>Click to Search</button>
        {#if operatorData  && operatorClass}
            <div class="operatorSpecifics">
                <p>Name: {operatorData.name}<br>Rarity: {operatorData.rarity} <br> Class: {operatorClass.join(', ')}</p>
            </div>
        {/if}
    </div>
</div>


<style>


.searchbar{
    margin: 10px;
    text-align: center;
    padding: 10px;
}
    
.searchbutton{
    width: 250px;
    height: 40px;
    margin:10px;
}


input{
    width:500px;
    height: 40px; 
}


.content {
    position: relative;
    z-index: 1;
    color: lightgray;
}

h2{
    font-family: 'Noto Sans', sans-serif;
    font-weight: bold;
    src: url(https://fonts.gstatic.com/s/notosans/v36/o-0ZIpQlx3QUlC5A4PNr4C5OaxRsfNNlKbCePevttHOmDyw.woff2) format('woff2');
    unicode-range: U+0460-052F, U+1C80-1C8A, U+20B4, U+2DE0-2DFF, U+A640-A69F, U+FE2E-FE2F;    
    color: lightgray;
}

</style>