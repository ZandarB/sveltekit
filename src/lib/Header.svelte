<script>
    export let headingTitle;
</script>

<header>
    <h1>{headingTitle}</h1>
    <nav>
        <div class="links">
            <a href="/">Home</a>
            <a href="/about">About</a>
            <a href="/contact_us">Contact</a>
            <a href="/search">Search</a>
        </div>
    </nav>
</header>

<style>
    .links {
        display: flex;
        padding: 0;
        margin: 0; 
    }

    .links a {
        margin-right: 20px; 
        text-decoration: none;
        color: inherit; 
    }

    .links a:hover {
        text-decoration: underline; 
    }

    header > h1{
    font-family: 'Noto Sans', sans-serif;
    font-weight: bold;
    src: url(https://fonts.gstatic.com/s/notosans/v36/o-0ZIpQlx3QUlC5A4PNr4C5OaxRsfNNlKbCePevttHOmDyw.woff2) format('woff2');
    unicode-range: U+0460-052F, U+1C80-1C8A, U+20B4, U+2DE0-2DFF, U+A640-A69F, U+FE2E-FE2F;    
    }
</style>