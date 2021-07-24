<script>
  import AnimeCard from "../components/AnimeCard.svelte";

  async function getSeasons() {
    let AllSeasons;
    const data = await fetch(`https://api.jikan.moe/v3/season/archive`)
      .then((res) => {
        return res.json();
      })
      .then((data) => data.archive);

    AllSeasons = data.map((season) => {
      return {
        year: season.year,
        seasons: season.seasons,
      };
    });

    return AllSeasons.slice(0, 3);
  }

  async function getSeasonalAnimes(season_year, season_name) {
    // console.log(
    //   `https://api.jikan.moe/v3/season/${season_year}/${season_name.toLowerCase()}`
    // );
    const data = await fetch(
      `https://api.jikan.moe/v3/season/${season_year}/${season_name.toLowerCase()}`
    )
      .then((res) => {
        return res.json();
      })
      .then((data) => data.anime);

    return data.map((anime) => {
      return {
        id: anime.mal_id,
        title: anime.title,
        cover: anime.image_url,
        url: anime.url,
      };
    });
  }
</script>

<main>
  {#await getSeasons()}
    loading
  {:then seasons}
    {#each seasons as season}
      <h1>{season.year}</h1>
      {#each season.seasons as season_name}
        <h3>{season_name}</h3>
        {#await getSeasonalAnimes(season.year, season_name)}
          loading
        {:then animes}
          <div class="season">
            {#each animes as anime}
              <AnimeCard {...anime} />
            {/each}
          </div>
        {/await}
      {/each}
    {/each}
  {/await}
</main>

<style>
  .season {
    display: flex;
    overflow: auto;
  }

  .season::-webkit-scrollbar {
    height: 0.25rem;
  }

  .season::-webkit-scrollbar-track {
    background: #1e1e24;
  }

  .season::-webkit-scrollbar-thumb {
    background: #6649b8;
  }
</style>
