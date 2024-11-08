<script>
    import Footer from '$lib/Footer.svelte';
    import Header from '$lib/Header.svelte';
</script>

<Header headingTitle = "About"/>
<p>This website is more or less an attempt at utlising an Arknights API (Linked Below). This inlcudes some basic usability and reactivity, and is mostly just a testing ground for implimenting new features. This may be updated as progress with my skills in web development,</p>
<h2>Current Update</h2>
<p>As of writing this, the latest Event the API is up to date with is the "Path of Life" Event (June 5, 2024 in the CN server.) </p>

<h2>Key Features</h2>
<ul>
    <li><strong>Interactive Tools:</strong> Utilize an API (linked below) to search through a database of operators and display basic details, such as rarity and class.</li>
</ul>

<h2>About the Creator</h2>
<p>Hi, I'm Zandar! I'm a web developer with a newfound love for web development (and for Arknights). This site is part of my journey to learn more about web development while also giving back to the community. I'm always looking to improve and add new features, so if you have any feedback or suggestions, feel free to reach out!</p>

<h2>What’s Coming Next?</h2>
<p>Here’s some (possibly) upcoming features:</p>
<ul>
    <li>More In Depth Operator Overview: Display Skills, Stats and build Costs.</li>
</ul>


<h2>Data Used</h2>
<p>https://api.rhodesapi.com/api/operator</p>


<h2><strong>Website Update Log:</strong></h2>
<p><strong>V 0.1</strong> <br> Implimented Update Log</p>
<br>
<style>
    *{
    font-family: 'Butler', serif;
    color: rgb(75, 75, 75);
    font-weight: bold;
    }

</style>
