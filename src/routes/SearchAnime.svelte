<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  import AnimeList from "./AnimeList.svelte";
  export let tagMaps;
  export let searchedAnimes;

  function getTopAnimes() {
    dispatch("getTopAnimes");
  }

  let keys = [...tagMaps.keys()];
  //   console.log(tagMaps);
</script>

<div class="search-tag">
  {#each keys as key}
    <a
      href="#"
      on:click={() => {
        tagMaps = new Map().set(key, tagMaps.get(key));
        keys = [key];
        dispatch("searchByTag", {
          query: "",
          tag: [key],
          nameTag: [tagMaps.get(key)],
        });
      }}
      >{tagMaps.get(key)}
    </a>
    {#if keys.lastIndexOf(key) !== tagMaps.size - 1}
      <span>></span>
    {/if}
  {/each}
</div>

<AnimeList animes={searchedAnimes} on:getTopAnimes={getTopAnimes} />

<style>
  .search-tag {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
  }
  a {
    padding: 0 5px;
  }
</style>
