<script>
    import Footer from '$lib/Footer.svelte';
    import Header from '$lib/Header.svelte';

    let operators = []; 
    let selectedOperator = null;
    let operatorE0Art = '';
    let feedback = '';
    let isLoading = true;
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

    async function fetchOperators() {
        isLoading = true;
        const response = await fetch(`https://api.rhodesapi.com/api/operator/`);
        if (response.ok) {
            operators = await response.json();
            selectRandomOperator();
        } else {
            feedback = 'There was an error fetching operators.';
        }
        isLoading = false;
    }
    
    function selectRandomOperator() {
        if (operators.length > 0) {
            const randomIndex = Math.floor(Math.random() * operators.length);
            selectedOperator = operators[randomIndex];
            operatorE0Art = selectedOperator.art[0].link; 
            feedback = ''; 
            selectedClass = '';
        } else {
            feedback = 'No operators available.';
        }
    }
    
    function checkAnswer(className) {
        const correctClass = selectedOperator.class[0];
        if (className === correctClass) {
            correctAnswers++;
            feedback = 'Correct! Total Correct Answers: ' + correctAnswers;
            setTimeout(selectRandomOperator, 2000);
        } else {
            feedback = 'Incorrect. The correct class is: ' + correctClass + '. The game has been reset.';
            correctAnswers = 0;
            selectedOperator = null;
            operatorE0Art = '';
            selectedClass = '';
            setTimeout(selectRandomOperator, 2000);
        }
    }

    fetchOperators();
</script>

<div class="content">
    <div class="searchbar">
        <h2>Operator Quiz</h2>
        <br>
        
        {#if isLoading}
            <p>Loading...</p>
        {:else}
            <div class="operatorSpecifics">
                {#if selectedOperator}
                    <p>
                        Name: {selectedOperator.name}<br>
                        Rarity: {selectedOperator.rarity}* <br>
                        E0 Art: 
                        <br>
                        <img src={operatorE0Art} alt={selectedOperator.name + " E0 IMG"} width="500" height="500"/> 
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
             {#if feedback.startsWith('Correct')}
                    <p class="success">{feedback}</p>
                {:else}
                <p class="error">{feedback}</p>
                {/if}            
            {/if}
        {/if}
        <h3>Welcome to my game of knowledge and memory!. </h3>
        <p>This quiz will test you on your knowledge of AK operators and their class, if you get the answer correct, Great! your score will add up infinitely. Get one wrong and you will be reset back to 0! Good luck!</p>
        <p>Please be aware that a select few operators do not have a full HD transparent art, and as such may look a bit skewed. Also when a new question is loading please allow a few seconds to answer, as the image may be loading.</p>
    </div>
</div>

<style>
div > p, h3 {
    font-family: 'Noto Sans', sans-serif;
    font-weight: bold;
    color: rgb(75, 75, 75);
}

.searchbar {
    margin: 10px;
    text-align: center;
    padding: 10px;
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

h2 {
    font-family: 'Noto Sans', sans-serif;
    font-weight: bold;
    color: rgb(75, 75, 75);
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
    margin: 5px 0; 
    cursor: pointer; 
    font-family: 'Noto Sans', sans-serif; 
    font-size: 16px; 
    color: rgb(75, 75, 75); 
    max-width: 200px; /* Set a maximum width for the label */
}

input[type="radio"] {
    margin-right: 10px; 
    accent-color: #007bff; 
}

</style>
