<script lang="ts">
	import axios from 'axios';
	import { onMount } from 'svelte';

	type Book = {
		id: string;
		isbn: string;
		name: string;
		author: string;
		year: string;
		publisher: string;
	}

	let books = $state([] as Book[]);

	onMount(async () => {
		try {
			const response = await axios.get("http://localhost:8080/books")
			books = await response.data;
		} catch (error) {
			console.error(error);
		}
	})

	let name = 'SvelteKit';
	let badabing = $state(0);
</script>

<h1>Welcome to {name}</h1>
<p>Visit <a href="https://svelte.dev/docs/kit">svelte.dev/docs/kit</a> to read the documentation</p>

<div>
	<div>
		{badabing}
	</div>
	{#each books as book, index}
		<div>
			<span>#{index}</span>
			<br />
			<span>Título: {book.name}</span>
			<br />
			<span>Autor: {book.author}</span>
			<br />
			<span>Ano: {book.year}</span>
			<br />
			<span>ISBN: {book.isbn}</span>
			<br />
			<span>Editora: {book.publisher}</span>
			<br />
			<br />
		</div>
	{/each}
</div>
