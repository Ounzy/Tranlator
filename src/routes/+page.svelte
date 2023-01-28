<h1>Welcome to EASY TRANSLATE</h1>
<div class="div1">
    <select name="languages" class="lang" bind:value={inputLang}>
        <option value="en">English</option>
        <option value="es">Spanish</option>
        <option value="de">German</option>
        <option value="it">Italian</option>
        <option value="el">Greek</option>
        <option value="fr">French</option>
    </select>

    <select name="languages" class="lang" bind:value={outputLang}>
        <option value="en">English</option>
        <option value="es">Spanish</option>
        <option value="de">German</option>
        <option value="it">Italian</option>
        <option value="el">Greek</option>
        <option value="fr">French</option>
    </select>
</div>

<div class="div">
    <input bind:value={input} on:keypress={handleKeypress} class="inputfield" id="valuefield" placeholder="Print your text here" type="text">
    <input bind:value={output} on:keypress={handleKeypress}  class="inputfield" placeholder="Translation" type="text">
</div>

<script type="module">
    import { onMount } from 'svelte';

    let url = "https://libretranslate.de/translate";
    let input;
    let output;
    let inputLang;
    let outputLang;
    

    async function getData() {
        const res = await fetch(url, {
            method: "POST",
            body: JSON.stringify({
                q: input,
                source: inputLang,
                target: outputLang,
                format: "text"
                }),
            headers: { "Content-Type": "application/json" }
        });	
        let response = await res.json();
        console.log(response);
        output = response.translatedText;
        console.log(inputLang);
    }

    function handleKeypress(event) {
        if (event.key === "Enter") {
            getData();
        }
    }
</script>


<style>
    .inputfield {
        width: 25rem;
        height: 15rem;
        border-radius: 1rem;
        margin-left: 5rem;
        margin-right: 5rem;
        background-color: rgb(29, 28, 28);
        color: aliceblue;
        border-color: white;
    }

    div {
        display: flex;
        width: 100%;
        justify-content: center;
    }

    .lang {
        display: flex;
        width: 5rem;
        margin-right: 25rem;
        margin-left: 5.6rem;
    }
</style>