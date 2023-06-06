<script>
	import Header from "./lib/Header.svelte";
</script>

<main>
	<Header />

	<input class="search" type="search" name="keyword" id="keyword" placeholder="Search...">
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
	background: #e9e4e492;
	margin-top: 40px;
	color: #000;
	font-size: 16px;
}
</style>
