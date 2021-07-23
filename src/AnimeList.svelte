<script>
    import AnimeCard from './AnimeCard.svelte'
    export let animes;

</script>

<main>    
    {#each animes as anime}
        <AnimeCard {...anime}/>
    {/each}
</main>

<style>
    main{
        display: flex;
        flex-wrap: wrap;
    }

    /*TODO Check anime card style  */

    /* Small Screen */
    @media only screen and (max-width: 600px){
        main{
            justify-content: center;
        }
    }

    /* Large Screen */
    @media only screen and (min-width: 600px){
        main{
            justify-content: start;
        }
    }


</style>