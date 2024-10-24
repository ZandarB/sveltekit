<script>
    import Footer from '$lib/Footer.svelte';
    import Header from '$lib/Header.svelte';
</script>

<Header headingTitle = "Contact us"/>

<p>We can be found at:</p>
<p>www.XYZ.com</p>
<p>0800 001 001</p>
<br>
<p>Name</p>
<input
    id="name"
    type="text"
    placeholder="Please enter your full name"
/>
<p>Email</p>
<input
    id="email"
    type="text"
    placeholder="Please enter your Email"
/>

<Footer year={1987}/>

<style>

    p{
        font-family: 'Noto Sans', sans-serif;
        font-weight: bold;
        src: url(https://fonts.gstatic.com/s/notosans/v36/o-0ZIpQlx3QUlC5A4PNr4C5OaxRsfNNlKbCePevttHOmDyw.woff2) format('woff2');  
        unicode-range: U+0460-052F, U+1C80-1C8A, U+20B4, U+2DE0-2DFF, U+A640-A69F, U+FE2E-FE2F;   
        color:lightgray;
    }

#email{
    width: 300px;
    height: 25px;
}

#name{
    width:200px;
    height: 25px;
}
</style>
