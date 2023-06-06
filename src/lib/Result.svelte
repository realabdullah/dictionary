<script>
	import playIcon from "../assets/play.svg";
	import pauseIcon from "../assets/pause.svg";

	export let result = {};

	let isPlaying = false;
	let audioFile = result?.phonetics[1]?.audio ?? "";

	function playAudio() {
		const audio = new Audio(audioFile);

		audio.addEventListener("ended", () => {
			isPlaying = false;
		});

		isPlaying = !isPlaying;
		isPlaying ? audio.play() : audio.pause();
	}
</script>

<div class="result">
	<div class="result-word">
		<div class="result-word__detail">
			<h2>{result.word}</h2>
			<span>{result?.phonetics[1]?.text ?? ""}</span>
		</div>

		{#if audioFile}
			<div class="result-word__audio">
				<button on:click={playAudio}>
					{#if isPlaying}
						<img src={pauseIcon} alt="Pause" />
					{:else}
						<img src={playIcon} alt="Play" />
					{/if}
				</button>
			</div>
		{/if}
	</div>

	{#each result.meanings as word}
		<div class="part-speech">
			<div class="part-speech__header">
				<span>{word.partOfSpeech}</span>
				<hr />
			</div>

			<div class="part-speech__body">
				<h5>Meaning</h5>

				<ul>
					{#each word.definitions as definition}
						<li>{definition.definition}</li>
					{/each}
				</ul>
			</div>

			{#if word.synonyms.length > 0}
				<div class="synonyms">
					<span>Synonyms</span>
					{#each word.synonyms as synonym}
						<span>{synonym}</span>
					{/each}
				</div>
			{/if}
		</div>
	{/each}
</div>

<style>
	.result {
		margin-top: 40px;
	}

	.result-word {
		display: flex;
		align-items: center;
		justify-content: space-between;
	}

	.result-word__detail {
		display: flex;
		flex-direction: column;
		gap: 10px;
	}

	.result-word__detail h2 {
		font-size: 45px;
		font-weight: 700;
		color: var(--black);
	}

	.result-word__detail span {
		font-size: 20px;
		color: var(--black);
	}

	.result-word__audio button {
		background: transparent;
		border: 0;
		outline: 0;
		cursor: pointer;
	}

	.result-word__audio button img {
		width: 50px;
		height: 50px;
	}

	.part-speech {
		margin-top: 40px;
	}

	.part-speech__header {
		display: flex;
		align-items: center;
		gap: 10px;
	}

	.part-speech__header span {
		font-size: 20px;
		font-weight: 700;
		color: var(--black);
	}

	.part-speech__header hr {
		flex: 1;
		border: 0;
		border-top: 1px solid var(--black);
	}

	.part-speech__body {
		margin-top: 40px;
	}

	.part-speech__body h5 {
		font-size: 20px;
		color: var(--fadedWhite);
	}

	.part-speech__body ul {
		margin-top: 20px;
		margin-left: 40px;
	}

	.part-speech__body ul li {
		margin-top: 10px;
		font-size: 20px;
		color: var(--black);
	}

	.synonyms {
		margin-top: 40px;
	}

	.synonyms span {
		margin-left: 10px;
		font-size: 20px;
		font-weight: 700;
		color: var(--black);
	}

	.synonyms span:first-child {
		font-weight: 400;
	}
</style>
