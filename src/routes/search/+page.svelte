<script>
import Footer from '$lib/Footer.svelte';
import Header from '$lib/Header.svelte';


let userInput = '';
let operatorData = '';
let operatorClass = [,,,];
let operatorE0Art = '';
let operatorE2Art = '';
let error = '';

async function getOperators(name)
{
    const allOps = await fetch(`https://api.rhodesapi.com/api/operator/`);
    const allOpsData = await allOps.json();
    console.log(allOpsData)

    const response = await fetch(`https://api.rhodesapi.com/api/operator/${name}/`);

   
    if (response.ok)
    {
        const data = await response.json();
        operatorClass = data.class;
        operatorData = data;
        operatorE0Art = data.art[0].link; 
        if (data.art[2] && data.art[2].link) {
            operatorE2Art = data.art[2].link; 
        } else {
            operatorE2Art = ''; // Clear E2 art if it doesn't exist
        }
        error = '';
        console.log("Successful fetch")
    }
    else
    {
        console.log("Error fetching operators. Invalid name entered.")
        error = 'There was an Error, Please enter a valid Name.';
    }
}

function search()
{
    operatorE0Art = '';
    operatorE2Art = '';
    operatorData = '';
    operatorClass = '';

    if (userInput){
        getOperators(userInput)
        
    }
    else
    {
    }
}
</script>


<div class="content">
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
        <button class="searchbutton" on:click={search}>Click to fetch data (If available)</button>
        {#if operatorData}
            <div class="operatorSpecifics">
                <p>
                    Name: {operatorData.name}<br>
                    Rarity: {operatorData.rarity}* <br>
                    Class: {operatorClass.join(', ')} <br>
                    
                    {#if operatorE0Art[0]} 
                        E0 Art: 
                        <br>
                        <img src={operatorE0Art} alt={operatorData.name + " E0 IMG"} width="500" height="500px"/> 
                    {/if} 

                    <br>

                    {#if operatorE2Art[2]} 
                        E2 Art:                    
                        <br>
                        <img src={operatorE2Art} alt={operatorData.name + " E2 IMG"} width="500px" height="500px"/>                     
                    {/if}
                </p>            
            </div>
        {:else if error}
            <div class="operatorSpecifics">
                <p class="error">{error}</p>
            </div>
        {/if}
    </div>
</div>


<style>

div > p{

    font-family: 'Noto Sans', sans-serif;
    font-weight: bold;
    src: url(https://fonts.gstatic.com/s/notosans/v36/o-0ZIpQlx3QUlC5A4PNr4C5OaxRsfNNlKbCePevttHOmDyw.woff2) format('woff2');
    unicode-range: U+0460-052F, U+1C80-1C8A, U+20B4, U+2DE0-2DFF, U+A640-A69F, U+FE2E-FE2F;    
    color: rgb(75,75,75);

}

.searchbar{
    margin: 10px;
    text-align: center;
    padding: 10px;
}
    
.searchbutton{
    width: 250px;
    height: 40px;
    margin:10px;
    outline: black solid 1px;
}


input{
    width:500px;
    height: 40px; 
    outline: black solid 1px;
}


.content {
    position: relative;
    z-index: 1;
    background-color: lightgray; 
    width: 750px;
    padding: 20px; 
    margin: 20px auto 0;    
    display: flex;
    flex-direction: column;
    align-items: center; 
    border: black solid 2px;
    border-radius: 7px;

}

h2{
    font-family: 'Noto Sans', sans-serif;
    font-weight: bold;
    src: url(https://fonts.gstatic.com/s/notosans/v36/o-0ZIpQlx3QUlC5A4PNr4C5OaxRsfNNlKbCePevttHOmDyw.woff2) format('woff2');
    unicode-range: U+0460-052F, U+1C80-1C8A, U+20B4, U+2DE0-2DFF, U+A640-A69F, U+FE2E-FE2F;    
    color: rgb(75,75,75);
    ;
}

.error{
    color: red;
}
</style>