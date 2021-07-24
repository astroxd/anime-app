<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  import AnimeCard from "../components/AnimeCard.svelte";
  export let animes;
</script>

<main>
  {#if animes.length === 0}
    <button on:click={() => dispatch("getTopAnimes")}
      >Go back to Top Anime</button
    >
    <div class="no-data">no data</div>
  {:else}
    {#each animes as anime}
      <AnimeCard {...anime} />
    {/each}
  {/if}
</main>

<style>
  main {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }

  /* Small Screen */
  /* @media only screen and (max-width: 600px){
        main{
            justify-content: center;
        }
    } */

  /* Large Screen */
  /* @media only screen and (min-width: 600px){
        main{
            justify-content: start;
        }
    } */
</style>
