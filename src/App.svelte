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


	async function searchAnime(event){
		animes = [];
		page = 'topAnimes';	
		let query = event.detail.query;
		if(query.length < 3){
			getTopAnimes();
		}else{

		
		const data = await fetch(`https://api.jikan.moe/v3/search/anime?q=${query}&order_by=title&sort=desc&page=1`)
					.then(res => {return res.json()})
					.then(data => data.results);
		
		animes = data.map(anime =>{
			return {
				id: anime.mal_id, 
				title: anime.title, 
				cover: anime.image_url, 
				url:anime.url
				}
			})
		}

	}


	getTopAnimes();


</script>

<NavBar on:getTopAnimes={getTopAnimes} 
		on:getSeasonalAnimes={getSeasonalAnimes}
	/>
<main>
	<SearchBar on:searchAnime={searchAnime}/>
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