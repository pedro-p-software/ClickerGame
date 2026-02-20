<script>
    /** @type {import('./$types').PageProps} */
    let { data } = $props();

    let pressed = $state(false);
    let clicks = $state(0);

    function press(){
        pressed = true;
        clicks++;
         setTimeout(()=> pressed = false, 150
        );
    }

</script>

<div class="justify-center items-center h-screen flex">
    <div class="absolute self-center justify-center right-99/100 bottom-95/100">{clicks}</div>

    <div class="bg-gray-600 w-75 h-75 rounded-full mt-7"></div>
    <div class="bg-red-800 w-60 h-60 rounded-full mt-7 absolute"></div>
    <button
        class="bitcount-grid-double-texto-botao absolute mb-5 font-sans self-center text-6xl flex rounded-full bg-red-600 w-60 h-60 justify-center items-center text-center"
        class:pressed={pressed}
        onclick={press}
    >
        CLICK
</button>
</div>
