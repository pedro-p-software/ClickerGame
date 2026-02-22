<script>
    /** @type {import('./$types').PageProps} */
    let { data } = $props();

    let clicked = $state(false);
    let clicks = $state(0);

    let shopOpened = $state(false);

    let TenthTimeClicking = $derived(clicks>=10);
    let hundredthTimeClicking = $derived(clicks>=100);


    let btnFace = $derived(clicked ? ":3" : ":I");

    function pressed() {
        clicked = true;
        clicks++;

    }

</script>

<div class="justify-center items-center h-screen flex">
    <div
        class=" flex absolute left-5 top-5 bg-emerald-700 border-2 border-black z-2 w-65 h-20 {clicks >= 10 ? 'visible' : 'invisible'}"
        class:explode={TenthTimeClicking}
    >
        <div
            class=" text-3xl ComicNeue left-3 top-2"
        >
            CLIQUES: {clicks}
        </div>
    </div>

    <button
        id="SHOP"
        onclick={(shopOpened = !shopOpened)}
        class:explode = {hundredthTimeClicking}
        class=" {clicks >= 100
            ? 'visible'
            : 'invisible'} flex items-center justify-center text-center absolute right-10 top-10 bg-emerald-700 border-4 border-black z-2 w-80 h-30"
    >
        <label class="ComicNeue text-5xl font-sans z-1" for="SHOP">
            SHOP
        </label>
    </button>

    <div class="bg-gray-600 w-75 h-75 rounded-full mt-7 absolute"></div>
    <div class="bg-red-800 w-60 h-60 rounded-full mt-7 absolute"></div>

    <button
        class="bitcount-grid-double-texto-botao absolute mb-5 font-sans self-center text-6xl flex rounded-full bg-red-600 w-60 h-60 justify-center items-center text-center"
        class:clicked
        onmousedown={pressed}
        onmouseup={(clicked = false)}
        onmouseleave={(clicked = false)}
    >
        CLIQUE {btnFace}
    </button>

    <div
        class="h-screen w-72 ease duration-300 justify-end bg-emerald-900 right-0 fixed 
        {shopOpened
            ? 'translate-x-0'
            : 'translate-x-full'}"
    ></div>
</div>
