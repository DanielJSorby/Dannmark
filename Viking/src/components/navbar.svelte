<script>
    import { onMount } from 'svelte';
    import { writable } from 'svelte/store';

    let solidNav = writable(false);

    onMount(() => {
        const handleScroll = () => {
            const scrollTop = window.pageYOffset || document.documentElement.scrollTop;

            if (scrollTop >= 1) {
                solidNav.set(true);
                // @ts-ignore
                document.getElementById('logo').style.backgroundImage = "url('./Bilder/Oslo_Kommune_Logo_Transparent.png')";
                console.log("solid-nav");
            } else {
                solidNav.set(false);
                // @ts-ignore
                document.getElementById('logo').style.backgroundImage = "url('./Bilder/Oslo_Kommune_Logo_Transparent_Hvit.png')";
                console.log("no-solid-nav");
            }
        };

        window.addEventListener('scroll', handleScroll);

        return () => {
            window.removeEventListener('scroll', handleScroll);
        };
    });
</script>

<div class="navbar" class:solid-nav={$solidNav}>
    <a href="./">
        <div id="logo" class="logo navbar-logo"></div>
    </a>
    <ul class="navbar_lenker">
        <li><a href="./Hva-kan-du-gjore/" id="navbar-siste-nyheter">Hva kan du gjøre?</a></li>
        <li><a href="./Hva-gjor-oslo/" id="navbar-om-oss">Hva gjør Oslo?</a></li>
        <li><a href="./Kildesortering/" id="navbar-events">Kildesortering</a></li>
    </ul>
</div>
<label id="hamburger">
    <input type="checkbox">
    <span class="menu"> <span class="hamburger"></span> </span>
    <ul class="navbar_lenker">
        <li><a href="./" style="color: #2B2854; text-decoration: underline; text-decoration-thickness: .3rem; text-underline-offset: .45rem;">Hjem</a></li>
        <li><a href="./Hva-kan-du-gjore/" id="navbar-siste-nyheter">Hva kan du gjøre?</a></li>
        <li><a href="./Hva-gjor-oslo/" id="navbar-om-oss">Hva gjør Oslo?</a></li>
        <li><a href="./Kildesortering/" id="navbar-events">Kildesortering</a></li>
    </ul>
</label>

<style>
    /* navbar CSS*/
    .navbar {
        font-family: 'OsloSans', sans-serif;
        font-weight: 500;
        height: 5rem;
        width: 100%;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
        font-size: 1.6rem;
        position: fixed;
        transition: background-color 0.2s linear;
        -webkit-text-stroke: 0.01875rem black;
        z-index: 10000;
        margin: 0;
    }

    .solid-nav {
        background-color: #D9CFC0;
        transition: background-color 0.2s linear;
        -webkit-text-stroke: 0rem black;
        box-shadow: 0px 10px 12px 0px rgba(0,0,0,0.55);
    }

    .logo {
        color: #8A3036;
        display: flex;
        height: 4rem;
        margin-left: 1.5rem;
        width: 12rem;
        background-image: url('./Bilder/Oslo_Kommune_Logo_Transparent_Hvit.png');
        background-size: contain;
        background-repeat: no-repeat;
    }

    .navbar ul li {
        list-style-type: none;
        display: inline-block;
        padding: 0.625rem 1.25rem;
    }

    .navbar ul li a {
        color: #8A3036;
        text-decoration: none;
        display: inline-block;
        position: relative;
    }

    .solid-nav ul li a {
        color: #2B2854;
        transition: .3s;
    }

    .navbar ul li a::after {
        content: '';
        position: absolute;
        width: 100%;
        transform: scaleX(0);
        height: 0.3rem;
        bottom: 0;
        left: 0;
        background-color: #8A3036;
        transform-origin: bottom right;
        transition: transform 0.25s ease-out;
    }

    .navbar ul li a:hover::after {
        transform: scaleX(1);
        transform-origin: bottom left;
    }

    .navbar ul li a:hover {
        color: #8A3036;
        transition: .3s;
    }

    /* Hamburgernavbar CSS */
    *, *:before, *:after { 
        box-sizing: border-box; 
    }

    label .menu {
        position: fixed;
        right: -100px;
        top: -100px;
        z-index: 100;
        width: 200px;
        height: 200px;
        background: #D9CFC0;
        border-radius: 50% 50% 50% 50%;
        -webkit-transition: .5s ease-in-out;
        transition: .5s ease-in-out;
        box-shadow: 0 0 0 0 #D9CFC0, 0 0 0 0 #D9CFC0;
        cursor: pointer;
        box-shadow: 0px 10px 15px rgba(0, 0, 0, 0.1);
    }

    label .hamburger {
        position: absolute;
        top: 135px;
        left: 50px;
        width: 30px;
        height: 2px;
        background: #2B2854;
        display: block;
        -webkit-transform-origin: center;
        transform-origin: center;
        -webkit-transition: .5s ease-in-out;
        transition: .5s ease-in-out;
    }

    label .hamburger:after, label .hamburger:before {
        -webkit-transition: .5s ease-in-out;
        transition: .5s ease-in-out;
        content: "";
        position: absolute;
        display: block;
        width: 100%;
        height: 100%;
        background: #8A3036;
    }

    label .hamburger:before { top: -10px; }

    label .hamburger:after { bottom: -10px; }

    label input { display: none; }

    label input:checked + .menu {
        box-shadow: 0 0 0 100vw #D9CFC0, 0 0 0 100vh #D9CFC0;
        border-radius: 0;
    }

    label input:checked + .menu .hamburger {
        -webkit-transform: rotate(45deg);
        transform: rotate(45deg);
    }

    label input:checked + .menu .hamburger:after {
        -webkit-transform: rotate(90deg);
        transform: rotate(90deg);
        bottom: 0;
    }

    label input:checked + .menu .hamburger:before {
        -webkit-transform: rotate(90deg);
        transform: rotate(90deg);
        top: 0;
    }

    label input:checked + .menu + ul { opacity: 1; }

    label ul {
        z-index: 200;
        position: fixed;
        top: 50%;
        left: 50%;
        -webkit-transform: translate(-50%, -50%);
        transform: translate(-50%, -50%);
        opacity: 0;
        -webkit-transition: .25s 0s ease-in-out;
        transition: .25s 0s ease-in-out;
    }

    label a {
        margin-bottom: 1em;
        display: block;
        text-decoration: none;
        font-size: 1.875rem;
        font-weight: 300;
        color: #8A3036
    }

    .hamburger {
        display: none;
    }
    label .menu {
        display: none;
    }
    label {
        display: none;
    }

    @media screen and (max-width: 1000px) {
        .navbar {
            display: none;
        }

        .hamburger {
            display: block;
        }
        label .menu {
            display: block;
        }
        label {
            display: block;
        }
    }
</style>