<script>
  import NavBar from "./components/NavBar.svelte";
  import SearchBar from "./components/SearchBar.svelte";

  import AnimeList from "./routes/AnimeList.svelte";
  import SeasonalAnimeList from "./routes/SeasonalAnimeList.svelte";
  import SearchAnime from "./routes/SearchAnime.svelte";
  import AnimeCard from "./components/AnimeCard.svelte";
  let animes = [];
  let page = "topAnimes";

  async function getTopAnimes() {
    animes = [];
    page = "topAnimes";
    const data = await fetch(
      `https://api.jikan.moe/v3/top/anime/1/bypopularity`
    )
      .then((res) => res.json())
      .then((data) => {
        return data.top;
      });

    animes = data.map((anime) => {
      return {
        id: anime.mal_id,
        title: anime.title,
        cover: anime.image_url,
        url: anime.url,
      };
    });

    return animes;
  }

  async function getSeasonalAnimes() {
    page = "seasonalAnimes";
  }

  let searchedAnimes = [];
  let nameTags = [];
  let tags = [];
  async function searchAnime(event) {
    console.log(event.detail);
    searchedAnimes = [];
    page = "searchAnimes";
    let query = event.detail.query;
    tags = event.detail.tag;
    nameTags = event.detail.nameTagList;

    let queryString = "";
    let tagsString = "";
    let sort = "";
    let order_by = "";

    if (tags.length === 0) {
      if (query.length < 3) {
        page = "topAnimes";
        getTopAnimes();
      } else {
        queryString = query;
        sort = "&sort=desc";
        order_by = "&order_by=title";
      }
    } else {
      tagsString = `&genre=${tags.join(",")}`;
      if (query.length >= 3) {
        queryString = query;
      }
      sort = "&sort=desc";
      order_by = "&order_by=members";
    }

    let finalQuery = `https://api.jikan.moe/v3/search/anime?q=${queryString}${tagsString}${order_by}${sort}&page=1`;
    console.log(finalQuery);
    const data = await fetch(finalQuery)
      .then((res) => res.json())
      .then((data) => data.results)
      .catch((error) => []);

    searchedAnimes = data.map((anime) => {
      return {
        id: anime.mal_id,
        title: anime.title,
        cover: anime.image_url,
        url: anime.url,
      };
    });
  }

  function getTags() {
    let map = new Map();
    for (let i = 0; i < tags.length; i++) {
      map.set(tags[i], nameTags[i]);
    }
    console.log(map);
    return map;
  }

  getTopAnimes();
</script>

<NavBar
  on:getTopAnimes={getTopAnimes}
  on:getSeasonalAnimes={getSeasonalAnimes}
/>
<main>
  <SearchBar on:searchAnime={searchAnime} />
  {#if page === "topAnimes"}
    <AnimeList {animes} />
  {:else if page === "seasonalAnimes"}
    <SeasonalAnimeList />
  {:else if page === "searchAnimes"}
    <SearchAnime
      tagMaps={getTags()}
      {searchedAnimes}
      on:getTopAnimes={getTopAnimes}
      on:searchByTag={searchAnime}
    />
  {/if}
</main>

<style>
  main {
    margin-left: 8rem;
    padding: 1rem;
  }
</style>
