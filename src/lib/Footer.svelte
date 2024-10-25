<script>


let currentTime = new Date();
let currentYear = new Date().getFullYear();

</script>

<p>&copy; My Shitshow: {currentYear} {currentTime}</p>

<style>
    body {
        display: flex;
        flex-direction: column;
        min-height: 100vh; /* Ensure the body takes at least the full height of the viewport */
        margin: 0; /* Remove default body margin */
    }

    .footer {
        margin-top: auto; /* Push footer to the bottom */
    }

    p { 
        padding: 5px;
        font-size: 20px;
        color: rgb(75, 75, 75);
        background-color: lightgray;
        width: 100%; 
        z-index: 1000;
        border: 2px solid black;
        border-radius: 7px;
        text-align: center; /* Center the text */
    }
</style>