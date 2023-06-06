<script>
    import dictionaryLogo from '../assets/book.svg';
    import moon from '../assets/moon.svg';
</script>

<header>
    <img class="logo" src={dictionaryLogo} alt="Logo" />

    <div class="header-ctas">
        <select name="font" id="font">
            <option value="serif">Serif</option>
            <option value="sans serif">Sans Serif</option>
            <option value="monospace">Monospace</option>
        </select>
        <span>|</span>

        <div class="toggle">
            <input type="checkbox" name="color-scheme" id="color-scheme">
            <label for="color-scheme"></label>
        </div>

        <img src={moon} alt="Color Mode" />
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

.header-ctas {
    display: flex;
    align-items: center;
    gap: 20px;
}

select {
    padding: 0 10px 0 10px;
    border: 0;
    outline: none;
}

input[type="checkbox"] {
    display: none;
}

input[type="checkbox"]:checked + label {
    background-color: #000;
}

input[type="checkbox"]:checked + label:before {
    transform: translateX(13px);
    background-color: #fff;
}

label {
	display: flex;
	width: 35px;
	height: 20px;
	border: 1px solid;
	border-radius: 99em;
	position: relative;
	transition: transform .7s ease-in-out;
	transform-origin: 50% 50%;
	cursor: pointer;
}

label::before {
    transition: transform .7s ease;
    content: "";
    display: block;
    position: absolute;
    width: 14px;
    height: 14px;
    background-color: #000;
    border-radius: 50%;
    top: 2px;
    left: 3px;
}

.header-ctas img {
    width: 30px;
    height: 30px;
}
</style>