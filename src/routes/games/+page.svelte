<script>
    import Footer from '$lib/Footer.svelte';
    import Header from '$lib/Header.svelte';
    
    let operators = []; // To store all operators
    let selectedOperator = null;
    let operatorE0Art = '';
    let operatorE2Art = '';
    let feedback = '';
    let classes = [
        "Class A",
        "Class B",
        "Class C",
        "Class D",
        "Class E",
        "Class F",
        "Class G",
        "Class H"
    ]; // Placeholder classes
    
    // Function to fetch all operators
    async function fetchOperators() {
        try {
            const response = await fetch(`https://api.rhodesapi.com/api/operator/`);
            if (response.ok) {
                operators = await response.json();
                console.log("Successfully fetched all operators");
            } else {
                console.log("Error fetching operators");
                feedback = 'There was an error fetching operators.';
            }
        } catch (err) {
            console.error(err);
            feedback = 'There was an error fetching operators.';
        }
    }
    
    // Function to select a random operator
    function selectRandomOperator() {
        if (operators.length > 0) {
            const randomIndex = Math.floor(Math.random() * operators.length);
            selectedOperator = operators[randomIndex];
            operatorE0Art = selectedOperator.art[0].link; 
            operatorE2Art = selectedOperator.art[2]?.link || ''; // Optional chaining for E2 art
            feedback = ''; // Clear any previous feedback
        } else {
            feedback = 'No operators available to select.';
        }
    }
    
    // Function to check the answer
    function checkAnswer(selectedClass) {
        const correctClass = selectedOperator.class.join(', '); // Assuming class is an array
        if (selectedClass === correctClass) {
            feedback = 'Correct!';
        } else {
            feedback = 'Incorrect. The correct class is: ' + correctClass;
        }
    }
    
    // Call fetchOperators when the component mounts
    fetchOperators();
    </script>
    
    <div class="content">
        <div class="searchbar">
            <h2>Operator Quiz</h2>
            <br>
            <button class="searchbutton" on:click={selectRandomOperator}>Get Random Operator</button>
            
            {#if selectedOperator}
                <div class="operatorSpecifics">
                    <p>
                        Name: {selectedOperator.name}<br>
                        Rarity: {selectedOperator.rarity}* <br>
                        
                        {#if operatorE0Art} 
                            E0 Art: 
                            <br>
                            <img src={operatorE0Art} alt={selectedOperator.name + " E0 IMG"} width="500" height="500"/> 
                        {/if} 
    
                        <br>
    
                        {#if operatorE2Art} 
                            E2 Art:                    
                            <br>
                            <img src={operatorE2Art} alt={selectedOperator.name + " E2 IMG"} width="500" height="500"/>                     
                        {/if}
                    </p>
                </div>
    
                <h3>What is the class of this operator?</h3>
                {#each classes as className}
                    <label>
                        <input type="radio"
                            name="operatorClass"
                            value={className}
                            on:change={() => checkAnswer(className)} />
                        {className}
                    </label>
                {/each}
                <p>{feedback}</p>
            {:else if feedback}
                <div class="operatorSpecifics">
                    <p class="error">{feedback}</p>
                </div>
            {/if}
        </div>
    </div>
    
    <style>
    /* Your existing CSS styles remain unchanged */
    </style>
    