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

	let book = $state({
		isbn: "1234567890123",
		name: "",
		author: "",
		year: "2000",
		publisher: "Exemplo Editora",
	})

	onMount(async () => {
		try {
			const response = await axios.get(`${import.meta.env.VITE_API_URL}/books`);
			books = await response.data;
		} catch (error) {
			window.alert("erro ao buscar livros :(");
			console.error(error);
		}
	});

	async function createBook() {
		try {
			const response = await axios.post(`${import.meta.env.VITE_API_URL}/books`, book)
			const created = response.data as Book;
			books.push(created)
			window.alert("livro criado :)");
		} catch(error) {
			window.alert("erro ao criar livro :(");
			console.error(error);
		}
	}

	async function deleteBook(id: string) {
		try {
			await axios.delete(`${import.meta.env.VITE_API_URL}/books/${id}`);
			books = books.filter((book) => book.id !== id);
			window.alert("livro apagado com sucesso!")
		} catch (error) {
			window.alert("erro ao apagar livro :(");
			console.error(error);
		}
	}
</script>

<h1>Maria Claraaaaaaaaaaa</h1>
<h3>♥♥♥♥♥♥♥♥♥ LINDA GOSTOSA TE AMO DEMAIS ♥♥♥♥♥♥♥♥♥♥</h3>
<img src="https://c.tenor.com/bZFUIkvAaAQAAAAC/tenor.gif" alt="olhos coração">

<br />

<p>Visite <a class="text-blue-600" href="https://www.sephora.com.br/">ESTE SITEZINHO AQUI (se-fô-rah)</a> se quiser</p>

<br />

<div>
	<form onsubmit={createBook} class="flex flex-col gap-y-2 max-w-xs">
		<label class="border p-2 rounded-md">
			ISBN:&nbsp;
			<input bind:value={book.isbn} type="text">
		</label>

		<label class="border p-2 rounded-md">
			Título:&nbsp;
			<input bind:value={book.name} type="text" placeholder="digite o título">
		</label>

		<label class="border p-2 rounded-md">
			Autor:&nbsp;
			<input bind:value={book.author} type="text" placeholder="digite o autor">
		</label>

		<label class="border p-2 rounded-md">
			Ano:&nbsp;
			<input bind:value={book.year} type="text">
		</label>

		<label class="border p-2 rounded-md">
			Editora:&nbsp;
			<input bind:value={book.publisher} type="text">
		</label>

		<button type="submit">Adicionar</button>
	</form>
</div>

<br>

<div>
	{#each books as book, index}
		<div>
			<span>#{index + 1}</span>
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
			<button onclick={() => deleteBook(book.id)}>🗑</button>
			<br />
			<br />
		</div>
	{/each}
</div>
