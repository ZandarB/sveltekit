<script>
    import Footer from '$lib/Footer.svelte';
    import Header from '$lib/Header.svelte';

    let operators = []; 
    let selectedOperator = '';
    let operatorArt = '';
    let result = '';
    let pageLoading = true;
    let correctAnswers = 0;
    let selectedClass = '';
    let classes = [
        "Vanguard",
        "Guard",
        "Defender",
        "Sniper",
        "Caster",
        "Medic",
        "Specialist",
        "Supporter"
    ]; 
    let gamePlaying = false;

    async function fetchOperators() {
        pageLoading = true;
        const response = await fetch(`https://api.rhodesapi.com/api/operator/`);
        if (response.ok) {
            operators = await response.json();
            console.log(operators)
            selectRandomOperator();
        } else {
            result = 'There was an error fetching operators.';
        }
        pageLoading = false;
    }
    
    function selectRandomOperator() {
        if (operators.length > 0) {

            const randomNumber = Math.floor(Math.random() * operators.length);

            if (randomNumber == 252)
            {
                selectRandomOperator();
            }

             {            
                selectedOperator = operators[randomNumber];
                operatorArt = selectedOperator.art[0].link; 
                result = ''; 
                selectedClass = '';
            }
            

        } else {
            result = 'No operators available.';
        }
    }
    
    function checkAnswer(className) {
    const correctClass = selectedOperator.class[0];
    if (className === correctClass) {
        correctAnswers++;
        result = 'Correct! Total Correct Answers: ' + correctAnswers;
        setTimeout(selectRandomOperator, 2000);
    } else {
        result = 'Incorrect. The correct class is: ' + correctClass + '. Your score will now be reset to 0.';
        correctAnswers = 0;
        selectedClass = '';
        setTimeout(selectRandomOperator, 2000);
    }
    }

function startPlaying()
{
    gamePlaying = true;
}

fetchOperators()
</script>

<div class="content">
    <div class="searchbar">
        <h2>Operator Quiz</h2>        
        {#if pageLoading}
            <p>Loading...</p>
        {:else if !gamePlaying}
            <input type="button"
                value="Start Game"
                class="startButton"
                on:click={startPlaying} />        
        {:else}
            <div class="operatorSpecifics">
                {#if selectedOperator}
                    <p>
                        Name: {selectedOperator.name}<br>
                        Rarity: {selectedOperator.rarity}* <br>
                        <img src={operatorArt} alt={selectedOperator.name + " E0 IMG"} width="500" height="500"/> 
                    </p>
                {/if}
            </div>

            {#if selectedOperator}
                <h3>What is the class of this operator?</h3>
                <div class ="radioButtonContainer">
                    {#each classes as className}
                    <label>
                        <input type="radio"
                            name="operatorClass"
                            value={className}
                            bind:group={selectedClass}
                            on:change={() => checkAnswer(className)} />
                        {className}
                    </label>
            {/each}
            </div>
             {#if result.startsWith('Correct')}
                    <p class="success">{result}</p>
                {:else}
                    <p class="error">{result}</p>
                {/if}            
            {/if}
        {/if}
        <h3>Welcome to my game of knowledge and memory!</h3>
        <p>This quiz will test you on your knowledge of AK operators and their class, if you get the answer correct, Great! your score will add up infinitely. Get one wrong and you will be reset back to 0! Good luck!</p>
        <p>Please be aware that a select few operators do not have a full HD transparent art, and as such may look a bit skewed. Also when a new question is loading please allow a few seconds to answer, as the image may be loading.</p>
    </div>
</div>

<style>
div > p, h3 {
    font-family: 'Butler', serif;
    font-weight: bold;
    color: rgb(75, 75, 75);
    font-size: 20px;
}

.searchbar {
    margin: 10px;
    text-align: center;
    padding: 10px;
}

h2 {
    font-family: 'Butler', serif;
    font-weight: bold;
    color: rgb(75, 75, 75);
    font-size: 40px;
}

.error {
    color: red;
}

.success {
    color: green;
}

label {
    display: flex; 
    align-items: center; 
    flex-wrap: wrap; 
    cursor: pointer; 
    font-family: 'Butler', serif;
    font-size: 16px; 
    color: rgb(75, 75, 75); 
    max-width: 200px;
    font-weight: bold;
    margin-left: 5px;
}

input[type="radio"] {
    margin-right: 2px; 
    accent-color: #007bff; 
}

.radioButtonContainer{
    display: flex;
    justify-content: center;
}

.radioButtonContainer :hover {
    color: #1a1a1a; 
    transform: scale(1.1); 
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2); 
    border-radius: 5px;
    transition: color 0.3s, transform 0.3s, box-shadow 0.3s;
}


.startButton {
    max-width: 200px;
    padding: 15px; 
    font-size: 16px; 
    border-radius: 7px;
    border:solid black 2px;
}

</style>
