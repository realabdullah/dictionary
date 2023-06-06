<script>
import Header from "./lib/Header.svelte";
import Result from "./lib/Result.svelte";

let result = {};
let keyword = '';

async function getWord() {
	console.log("keyword", keyword);
    const url = `https://api.dictionaryapi.dev/api/v2/entries/en/${keyword}`;
    const response = await fetch(url);
    const data = await response.json();

	result = data[0];
}
</script>

<main>
	<Header />

	<form on:submit|preventDefault={getWord}>
		<input class="search" type="search" name="keyword" id="keyword" placeholder="Search..." bind:value={keyword}>
	</form>

	{#if Object.keys(result).length > 0}
		<Result result={result} />
	{/if}
</main>

<style>
main {
	width: 100%;
	max-width: 700px;
	margin: 60px auto;
}

.search {
	width: 100%;
	padding: 15px;
	border-radius: 10px;
	border: 0;
	outline: 0;
	background: var(--fadedWhite);
	margin-top: 40px;
	color: #000;
	font-size: 16px;
}
</style>
