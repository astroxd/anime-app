<script>
    import { createEventDispatcher} from 'svelte';

    const dispatch = createEventDispatcher();

    function getSeasonalAnimes(){
        dispatch('getSeasonalAnimes');
    }
    function getTopAnimes(){
        dispatch('getTopAnimes');
    }
</script>

<nav class="navbar">
    <ul class="navbar-nav">
        <li class="logo">
            <a href="#" class="nav-link">
                <span class="link-text">Anime</span>
            </a>
        </li>
        <li class="nav-item">
            <a href="#" class="nav-link" on:click={getTopAnimes}>
                <span class="link-text">Top Anime</span>
            </a>
        </li>
        <li class="nav-item">
            <a href="#" class="nav-link" on:click={getSeasonalAnimes}>
                <span class="link-text">Seasonal</span>
            </a>
        </li>
        <!-- <li class="nav-item">
            <a href="#" class="nav-link">
                <span class="link-text">Item</span>
            </a>
        </li> -->
    </ul>
</nav>

<style>

    .navbar {
        position: fixed;
        background-color: var(--bg-primary);
        transition: width 600ms ease;
        /* media Query */
        width: 8rem;
        height: 100vh;
    }

    .navbar:hover{
        width: 16rem;
    }


    .navbar-nav {
        list-style: none;
        padding: 0;
        margin: 0;
        display: flex;
        flex-direction: column;
        align-items: center;
        height: 100%;
    }

    .nav-item {
        width: 100%;
        text-align: center;
    }

    .logo {
        font-weight: bold;
        text-transform: uppercase;
        margin-bottom: 1rem;
        text-align: center;
        font-size: 1.5rem;
        letter-spacing: 0.3ch;
        width: 100%;
    }



    .nav-link {
        display: flex;
        align-items: center;
        justify-content: center;
        height: 5rem;
        color: var(--primary);
        text-decoration: none;
        /* filter: grayscale(100%) opacity(0.7); */
        transition: var(--transition-speed);
    }

    .nav-link:hover {
        /* filter: grayscale(0%) opacity(1); */
        background: var(--bg-secondary);
        /* color: var(--text-secondary); */
    }


    /* for icons */
    /* .link-text {
        display: none;
        margin-left: 1rem;
    } */
</style>