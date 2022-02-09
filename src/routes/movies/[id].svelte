<script context="module">
	export async function load({ url, fetch, params }) {
		const id = params.id;

		const qs = url.search; //url.serchparams에서 그냥 search 로 변경됨
		// const param = new URLSearchParams(qs);
		// param.set('name', 'ffffffff');
		// const end = param.toString();
		// console.log(end);

		const res = await fetch(`https://yts.mx/api/v2/list_movies.json/?name=${id}`);
		// `https://jsonplaceholder.typicode.com/posts/${id}`
		const movies = await res.json().then((result) => result.data.movies);
		// const loadmovies = movies.data.movies.map(() => {
		// 	console.log(loadmovies);
		// 	return {
		// 		title: movies.title
		// 	};
		// });

		if (res.ok) {
			return {
				props: {
					movies,
					id
				}
			};
			return {
				status: res.status,
				error: new Error('xxxxxxxxxxxxxxxxxxxxx')
			};
		}
	}
</script>

<script lang="ts">
	export let movies;
	export let id;

	let isLoading = true;
	const thisPage = movies.find((movie) => movie.id === +id); //배열에서 값 찾기 + 타입 지정

	// console.log(movies);
</script>

<h2>{thisPage && thisPage.title}</h2>
<img src={thisPage && thisPage.large_cover_image} alt="detail_img" />
<p>{thisPage && thisPage.summary}</p>
