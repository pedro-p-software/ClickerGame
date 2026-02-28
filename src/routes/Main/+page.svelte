<script>
    /** @type {import('./$types').PageProps} */
    let { data } = $props();

    let clicked = $state(false);
    let clicks = $state(0);

    let shopOpened = $state(false);

    let clicksPerClick = $state(1);

    let showCantBuy = $state(false);

    let btnFace = $derived(clicked ? ":3" : ":I");

    function pressed() {
        clicked = true;
        clicks += clicksPerClick;
    }

    let timesBoughtCI = $state(1);
    let clickImprovementprice = $derived((5 * timesBoughtCI) ** 2);

    function clickImprovementBought() {
        if (clickImprovementprice > clicks) {
            showCantBuy = true;
            setTimeout(() => (showCantBuy = false), 1000);
        } else {
            clicksPerClick += 3;
            clicks -= clickImprovementprice;
            timesBoughtCI++;
        }
    }

    let timesBoughtAC = $state(0);
    let autoClickerPrice = $derived((10 * timesBoughtAC) ** 2 + 500);
    let autoClickerPower = $state(0);
    let autoClickerOn = $derived(timesBoughtAC > 0);

    function autoClickerBought() {
        if (autoClickerPrice > clicks) {
            showCantBuy = true;
            setTimeout(() => (showCantBuy = false), 1000);
        } else {
            autoClickerPower++;
            timesBoughtAC++;
            clicks -= autoClickerPrice;
        }
    }

    let intervalId = $state(null);

    $effect(() => {
        if (autoClickerOn) {
            intervalId = setInterval(() => {
                clicks += autoClickerPower;
            }, 1000);
        } return () => {
            if ((intervalId)) {
                clearInterval(intervalId);
            }
        };
    });
</script>

<div class="justify-center items-center h-screen flex">
    <div
        class=" flex absolute left-5 top-5 bg-emerald-700 border-2 border-black z-2 w-65 h-20 {clicks >=
            10 || timesBoughtCI > 1
            ? 'visible, explode'
            : 'invisible'}"
    >
        <div class=" text-3xl ComicNeue left-3 top-2">
            CLIQUES: {clicks}
        </div>
    </div>

    <button
        id="SHOP"
        onclick={(shopOpened = !shopOpened)}
        class=" {clicks >= 50 || timesBoughtCI > 1
            ? 'visible, explode'
            : 'invisible'} 
            flex items-center justify-center text-center absolute right-10 top-10 bg-emerald-700 border-4 border-black z-2 w-80 h-30"
    >
        <label class="ComicNeue text-5xl font-sans z-1" for="SHOP">
            SHOP
        </label>
    </button>

    <div
        id="buyWarning"
        class:miniexplode={showCantBuy}
        class="{showCantBuy
            ? 'visible'
            : 'invisible'} w-90 h-40 text-center top-10 self-center items-center justify-center flex absolute bg-amber-400"
    >
        <label class="text-2xl ComicNeue font-sans" for="buyWarning"
            >Not enough clicks buddy.</label
        >
    </div>

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
        {shopOpened ? 'translate-x-0' : 'translate-x-full'}"
    >
        <div class="mt-40 bg-amber-400 h-full list-none gap-10">
            <ul>
                <li id="ClickImprovement">
                    <button
                        class="w-full mt-5 border-4 border-black"
                        onclick={clickImprovementBought}
                        id="clickImprovement {clicks < clickImprovementprice
                            ? 'disabled'
                            : 'enabled'}"
                    >
                        CLICK POWER: {clickImprovementprice} bucks</button
                    >
                </li>

                <li>
                    <button onclick={autoClickerBought}>
                        +1 AUTO CLICKER: {autoClickerPrice}
                    </button>
                </li>
            </ul>
        </div>
    </div>
</div>
<button onclick={(clicks += 1000)}> HACK </button>
