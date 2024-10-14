<script>
    export let headingTitle;

</script>

<header>
    <h1>{headingTitle}</h1>
    <nav>
        <ul>
            <li><a href="/home">Home</a></li> 
            <li><a href="/about">About</a></li>
            <li><a href="/contact_us">Contact</a></li>
        </ul>
    </nav>
</header>

<style>

 {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    list-style: none;
    font-weight: bolder;
    font-size: 25px;
    font-family:'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
    background-color: black;
    padding: 2px;
    border: 20px solid blue; 
}
</style>