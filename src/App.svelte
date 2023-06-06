<script>
import Header from "./lib/Header.svelte";
import Result from "./lib/Result.svelte";

let loading = false;
let isError = false;
let errorMessage = 'Something went wrong. Please try again later.';
let result = {};
let keyword = '';

async function getWord() {
	try {
		isError = false;
		loading = true;
		const url = `https://api.dictionaryapi.dev/api/v2/entries/en/${keyword}`;
		const response = await fetch(url);
		const data = await response.json();

		result = data[0];
		if (!result) {
			isError = true;
			errorMessage = data.message;
		}
		loading = false;
	} catch (error) {
		loading = false;
		isError = true;
	}
}
</script>

<main>
	<Header />

	<form on:submit|preventDefault={getWord}>
		<input class="search" type="search" name="keyword" id="keyword" placeholder="Search..." bind:value={keyword}>
	</form>

	{#if loading}
		<p class="loading">Loading...</p>
	{/if}

	{#if !isError && !loading && Object.keys(result).length > 0}
		<Result result={result} />
	{/if}

	{#if isError}
		<p class="error">{errorMessage}</p>
	{/if}
</main>

<style>
main {
	width: 100%;
	max-width: 700px;
	min-height: 100vh;
	margin: 60px auto;
	position: relative;
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

.error,
.loading {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	color: var(--black);
}
</style>
