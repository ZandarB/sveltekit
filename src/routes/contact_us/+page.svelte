<script>
    import Footer from '$lib/Footer.svelte';
    import Header from '$lib/Header.svelte';

    let phone_number = '';
    let email = '';
    let name = '';
    let confirmation = '';

    function  enter()
    {

        if (phone_number == '' || email == '' || name == '')
        {  
            confirmation = "There was an error submitting your data, please make sure all forms are filled in correctly. Thank you :)"
            setTimeout(() => {
            confirmation = ''
            }, 2000);
        }
        if (phone_number != '' && email != '' && name != ''){

            phone_number = '';
            email = '';
            name = '';

            confirmation = 'Success! Your data has been forwarded.'
            setTimeout(() => {
                confirmation = ''
            }, 2000);

        }
    }

    function clear ()
    {

        phone_number = '';
        email = '';
        name = '';

        confirmation = 'Your data has been cleared.'
        setTimeout(() => {
            confirmation = ''
        }, 2000);

    }





</script>
<Header headingTitle = "Contact us"/>

<p>If you have some comments and/or querys, you can find us at:
</p>
<ul>Phone Number: XXX XXX XXXX
<br> Email: XXXXXX@XXX.com
<br> Location: XXXXX Road in XXXXX</ul>

<p>Name</p>
<input
    id="name"
    type="text"
    placeholder="Please enter your full name"
    bind:value={name}
    />
<p>Email</p>
<input
    id="email"
    type="text"
    placeholder="Please enter your Email"
    bind:value={email}
/>
<p>Phone Number</p>
<input
    id="phone_number"
    type="number"
    placeholder="Please enter your Phone Number"
    bind:value={phone_number}
/>


<button class="submit" on:click={enter}>Click here to Submit your Data</button>
<button class="clear" on:click={clear}>Click here to clear your Data.</button>

<p class="confirmation">{confirmation}</p>


<style>
.confirmation{
    color: black;
}

    p{
        font-family: 'Butler', serif;
        font-weight: bold;
        color:rgb(75, 75, 75);
    }

    #email{
        width: 300px;
        height: 25px;
    }

    #name{
        width:200px;
        height: 25px;
    }

    #phone_number{
        width: 250px;
        height:25px

    }

    input[type="number"]::-webkit-inner-spin-button,
    input[type="number"]::-webkit-outer-spin-button 
    {
            -webkit-appearance: none;
            margin: 0;
    }

    .submit{
        padding: 10px;
        margin: 10px;
    }

    ul{
        font-family: 'Butler', serif;
        font-weight: bold;
        color:rgb(75, 75, 75);
    }

</style>
