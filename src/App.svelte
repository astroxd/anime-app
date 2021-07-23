<script>
	import NavBar from './NavBar.svelte'
	import SearchBar from './SearchBar.svelte'
	import AnimeList from './AnimeList.svelte'
	import SeasonalAnimeList from './SeasonalAnimeList.svelte'

	let animes = [];
	let seasons = [];	
	let page = 'topAnimes';


	async function getTopAnimes(){
		animes = [];
		page = 'topAnimes';	
		const data = await fetch(`https://api.jikan.moe/v3/top/anime/1/bypopularity`)
					.then(res => res.json())
					.then(data => {return data.top});
				
		animes = data.map(anime => {
			return {
					id: anime.mal_id, 
					title: anime.title, 
					cover: anime.image_url, 
					url:anime.url
					}
				});
		
			
		return animes;
	}

	async function getSeasonalAnimes(){
		seasons = [];
		const data = await fetch(`https://api.jikan.moe/v3/season/archive`)
					.then(res => {
						
						return res.json()})
					.then(data => data.archive);
				
		seasons = data.map(season => {
			return {
					year: season.year,
					seasons: season.seasons,
					}
				});
		page = 'seasonalAnimes';

	}

	getTopAnimes();


</script>

<NavBar on:getTopAnimes={getTopAnimes} 
		on:getSeasonalAnimes={getSeasonalAnimes}
	/>
<main>
	<SearchBar/>
	{#if page === 'topAnimes'}
		<AnimeList animes={animes}/>
	{:else if page === 'seasonalAnimes'}
		<SeasonalAnimeList AllSeasons={seasons}/>
	{/if}
</main>

<style>
	main{
		margin-left: 8rem;
  		padding: 1rem;
	}

</style>