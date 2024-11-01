<script>
  import Footer from "../lib/Footer.svelte";
  import Navigation from "../lib/Navigation.svelte";

</script>

<div class="background"></div>
<h1>My Shitshow</h1>
<Navigation/>
<slot/>
<Footer/>
<style>
*{
    font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    color: lightgray;
}

.background {
    background-image: url('/bg.png');
    background-size: cover;
    background-position: center;
    height: 100vh;
    width: 100vw; 
    position: fixed; 
    top: 0;
    left: 0;
    z-index: -1;
}


</style>