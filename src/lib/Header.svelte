<script>
	import { onMount } from "svelte";

	let isDarkMode = false;
    let currentTheme = "";

    $: isDarkMode = currentTheme === "dark";

	function setTheme(theme) {
        localStorage.setItem("user-theme", theme);
        currentTheme = theme;
        document.documentElement.className = theme;
    }

    function getMediaPreference() {
        const hasDarkPreference = window.matchMedia("(prefers-color-scheme: dark)").matches;

        if (hasDarkPreference) {
            return "dark";
        } else {
            return "light";
        }
    }

    function toggleColorScheme() {
        const currentTheme = localStorage.getItem("user-theme");

        if (currentTheme === "dark") {
            setTheme("light");
        } else {
            setTheme("dark");
        }
    }

    onMount(() => {
        setTheme(getMediaPreference());
    });
</script>

<header>
	<!-- <img class="logo" src={dictionaryLogo} alt="Logo" /> -->
	<div class="logo">
		<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 64 64" id="book"><path d="M54,2H14A5.006,5.006,0,0,0,9,7V57a5.006,5.006,0,0,0,5,5H54a1,1,0,0,0,1-1V3A1,1,0,0,0,54,2ZM14,4H53V50H14a4.948,4.948,0,0,0-3,1.026V7A3,3,0,0,1,14,4Zm0,56a3,3,0,0,1-3-3V55a3,3,0,0,1,3-3H53v3H15v2H53v3Z" /><path d="M18,22H48a1,1,0,0,0,1-1V9a1,1,0,0,0-1-1H18a1,1,0,0,0-1,1V21A1,1,0,0,0,18,22Zm1-12H47V20H19Z" /></svg>
	</div>

	<div class="header-ctas">
		<select name="font" id="font">
			<option value="serif">Serif</option>
			<option value="sans serif">Sans Serif</option>
			<option value="monospace">Monospace</option>
		</select>
		<span>|</span>

		<div class="toggle">
			<input type="checkbox" name="color-scheme" id="color-scheme" bind:checked={isDarkMode} on:change={toggleColorScheme} />
			<label for="color-scheme" />
		</div>

		<div class="mode">
			<svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" id="moon"><path d="M343.1 315c-1.8.1-3.5.1-5.3.1-29.1 0-56.5-11.3-77.1-31.9-20.6-20.6-31.9-48-31.9-77.1 0-16.6 3.7-32.6 10.6-47.1 3.1-6.4 6.8-12.5 11.1-18.2-7.6.8-14.9 2.4-22 4.6-46.8 14.8-80.7 58.5-80.7 110.2 0 63.8 51.7 115.5 115.5 115.5 35.3 0 66.8-15.8 88-40.7 4.8-5.7 9.2-11.9 12.8-18.5-6.8 1.7-13.8 2.8-21 3.1zm-79.8 40.1c-54.9 0-99.5-44.6-99.5-99.5 0-39.1 22.6-72.9 55.4-89.2-4.2 12.5-6.4 25.8-6.4 39.7 0 65.9 51 119.9 115.6 124.7-17.4 15.2-40.2 24.3-65.1 24.3z" fill="white" /></svg>
		</div>
	</div>
</header>

<style>
	header {
		display: flex;
		align-items: center;
		justify-content: space-between;
	}

	.logo {
		width: 30px;
		height: 30px;
	}

	.logo svg path {
		fill: var(--black);
	}

	.header-ctas {
		display: flex;
		align-items: center;
		gap: 20px;
	}

	select {
		padding: 0 10px 0 10px;
		border: 0;
		outline: none;
        background: var(--white);
        color: var(--black);
	}

	input[type="checkbox"] {
		display: none;
	}

	input[type="checkbox"]:checked + label {
		background-color: var(--black);
	}

	input[type="checkbox"]:checked + label:before {
		transform: translateX(13px);
		background-color: var(--white);
	}

	label {
		display: flex;
		width: 35px;
		height: 20px;
		border: 1px solid var(--black);
		border-radius: 99em;
		position: relative;
		transition: transform 0.7s ease-in-out;
		transform-origin: 50% 50%;
		cursor: pointer;
	}

	label::before {
		transition: transform 0.7s ease;
		content: "";
		display: block;
		position: absolute;
		width: 14px;
		height: 14px;
		background-color: var(--black);
		border-radius: 50%;
		top: 2px;
		left: 3px;
	}

    .mode svg path {
        fill: var(--black);
    }
</style>
