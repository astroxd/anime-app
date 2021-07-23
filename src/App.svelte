<script>
	import NavBar from './NavBar.svelte'
	import SearchBar from './SearchBar.svelte'
	import AnimeList from './AnimeList.svelte'

	let animes = [];	



	async function getTopAnimes(){
		animes = [];
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
		console.log('caca');

		animes = [];
		const data = await fetch(`https://api.jikan.moe/v3/search/anime?q=&genre=1,10&order_by=score&sort=desc`)
					.then(res => res.json())
					.then(data => data.results);
				
		animes = data.map(anime => {
			return {
					id: anime.mal_id, 
					title: anime.title, 
					cover: anime.image_url, 
					url:anime.url
					}
				});

	}

	getTopAnimes();


</script>

<NavBar on:getTopAnimes={getTopAnimes} on:getSeasonalAnimes={getSeasonalAnimes}/>
<main>
	<SearchBar/>
	<AnimeList animes={animes}/>
	<!-- {#await getTopAnimes()}
		loading
	{:then data}
		<AnimeList animes={data}/>
	{/await} -->
</main>

<style>
	main{
		margin-left: 8rem;
  		padding: 1rem;
	}

</style>