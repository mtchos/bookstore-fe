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
			const response = await axios.get('/api/books');
			books = await response.data;
		} catch (error) {
			console.error(error);
		}
	});
</script>

<h1>Maria Claraaaaaaaaaaa</h1>
<p>Visite <a class="text-blue-600" href="https://www.sephora.com.br/">ESTE SITEZINHO AQUI</a> se quiser</p>

<br />

<div>
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
