<script context="module">
	export async function load({ fetch, url, params }) {
		const res = await fetch('https://yts.mx/api/v2/list_movies.json');
		const movies = await res.json().then((result) => result.data.movies); //API 다 받아오면 result.data.movies
		const qs = url.searchParams;

		if (res.ok) {
			return {
				props: {
					movies
				}
			};
			return {
				status: res.status,
				error: new Error('xxxxxxxxxxxxxxxxxxxxx')
			};
		}
	}
</script>

<script>
	import Title from '$lib/title.svelte';
	export let movies;
</script>

<Title />
<h1>movies</h1>
<nav>
	<ul>
		<li><a href="/movies/movie1">page1</a></li>
		<li><a href="/movies/movie2">page2</a></li>
	</ul>
</nav>

<ul>
	{#each movies as page}
		<li><a href={`/movies/${page.id}`}><img src={page.medium_cover_image} alt="list_img" /></a></li>
		<li><a href={`/movies/${page.id}`}>{page.title}</a></li>
	{/each}
</ul>

<style>
	ul {
		list-style: none;
	}
</style>
