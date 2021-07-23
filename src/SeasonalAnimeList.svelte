<script>
    import AnimeCard from './AnimeCard.svelte'
import AnimeList from './AnimeList.svelte';
import App from './App.svelte';
    export let AllSeasons;
    let seasons = AllSeasons.slice(0,5);


    async function getSeasonalAnimes(season_year, season_name){
        const data = await fetch(`https://api.jikan.moe/v3/season/${season_year}/${season_name.toLowerCase()}`)
					.then(res => {
						return res.json()})
					.then(data => data.anime);
        
        return data.map(anime => {
			return {
					id: anime.mal_id, 
					title: anime.title, 
					cover: anime.image_url, 
					url:anime.url
					}
				});
    }


</script>

<main>
    {#each seasons as season}
        <h1>{season.year}</h1>
        {#each season.seasons as season_name}
            <h3>{season_name}</h3>
            {#await getSeasonalAnimes(season.year, season_name)}
                loading
            {:then animes}
            <div class="season">
                {#each animes as anime}
                    <AnimeCard {...anime}/>
                {/each}
            </div> 
            {/await}
        {/each}
    {/each}
    <!-- <div class="season">
        {#each animes as anime}
            <AnimeCard {...anime}/>
        {/each}
    </div>     -->
</main>

<style>
    .season{
        display: flex;
        overflow: auto;
    }
</style>