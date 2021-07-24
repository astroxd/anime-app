<script>

    import { createEventDispatcher} from 'svelte';
    const dispatch = createEventDispatcher();

    let query;

    function searchAnime(){
        dispatch('searchAnime',{query:query});
    }

    let showMenu;


</script>

<div>
    <div class="dropdown">
        <button on:click="{() => showMenu = !showMenu}">Tag</button>
        <div class="dropdown-content" class:show="{showMenu === true}" id="dropdownID">
            <li class="dropdown-item selected" on:click="{(event)=> console.log(event.target.innerText)}">Hentai</li>
            <li class="dropdown-item">Ecchi</li>
            <li class="dropdown-item">Shounen</li> 
        </div>
    </div>
    <form class="search-box" on:submit={searchAnime}>
        <input     
            bind:value={query}
            type="search" 
            placeholder="Search for anime...">
    </form>
</div>

<style>
    div{
        display: flex;
        justify-content: end;
    }

    button{
        margin: auto 1rem;
        background-color: #04AA6D;
        color: white;
        padding: 16px;
        font-size: 16px;
        border: none;
    }
    .dropdown {
        position: relative;
        display: inline-block;
    }

    .dropdown-content {
        display: none;
        position: absolute;
        background-color: #f1f1f1;
        min-width: 160px;
        box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
        z-index: 1;
    }

    .dropdown-content li {
        color: black;
        padding: 12px 16px;
        text-decoration: none;
        display: block;
    }

    .dropdown-content li:hover {
        background-color: #ddd;
    }

    .selected{
        background-color: red;
    }

    .show {display: block;}

    input{
        appearance: none;
        background: none;
        outline: none;
        border: none;
        
        display: block;
        width: 100%;
        max-width: 400px;
        padding: 16px;
        border-radius: 999px;
        background-color: #EEE;

        transition: var(--transition-speed);
    }



    input:focus{
        background-color: #313131;
        color: #FFF;
    }
    /* Small Screen */
    @media only screen and (max-width: 600px){
        /* input{
            margin:auto;
        } */
        /* div{
            justify-content: center;
        } */
    }

    /* Large Screen */
    @media only screen and (min-width: 600px){
        /* input{
            margin-left:auto;
        } */

        /* div{
            justify-content: end;
        } */
    }


</style>

<!-- <script>
    let languages = ['sk','cz','en','at']
    let activeLang = 'en'
</script>

<ul>
    {#each languages as language }
    <li on:click={() => activeLang = language} >{language}</li>
    {/each}
</ul> -->