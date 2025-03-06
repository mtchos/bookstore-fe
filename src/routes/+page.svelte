<script module>
	let books = [
		{
			title: 'Quincas Borba',
			author: 'Machado de Assis'
		},
		{
			title: 'Olhos d\'Água',
			author: 'Conceição Evaristo'
		},
		{
			title: 'Moby-Dick',
			author: 'Herman Melville'
		}
	];

</script>

<script lang="ts">
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
			<span>Author: {book.author}</span>
			<br />
			<span>Title: {book.title}</span>
			<br />
			<br />
		</div>
	{/each}
</div>
