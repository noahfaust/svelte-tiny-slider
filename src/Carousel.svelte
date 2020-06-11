<script>
    import { onMount } from 'svelte'
    import { tns } from '../node_modules/tiny-slider/src/tiny-slider'
    import CarouselItem from './CarouselItem.svelte'

    export let items
    export let itemsPerPage = 3

    let slider
    let currentIndex = 0
    $: hasEnded = (currentIndex + itemsPerPage) >= items.length

    onMount(() => {
        slider = tns({
            container: '.my-slider',
            items: itemsPerPage,
            slideBy: 'page',
            mouseDrag: true,
            swipeAngle: false,
            speed: 400,
            controls: false,
            nav: false,
            loop: false,
        })
    })

    const prev = () => {
        slider.goTo('prev')
        currentIndex = slider.getInfo().index
    }

    const next = () => {
        slider.goTo('next')
        currentIndex = slider.getInfo().index
        console.log('currentIndex + itemsPerPage', currentIndex + itemsPerPage)
        console.log('items.length', items.length)
    }
    
</script>

<section>

    
    <button class='prev {currentIndex + itemsPerPage >= items.length == 0 ? 'hidden' : ''}' on:click={prev}>
        <svg viewBox='0 0 4 8'>
            <path
                d='M 0.08483895,3.6630355 2.6588389,0.33303554 c 0.199,-0.318 0.64,-0.428 0.985,-0.244 0.344,0.185 0.463,0.593 0.263,0.91200006 l -2.318,2.9999999 2.318,2.998 c 0.2,0.321 0.08,0.727 -0.263,0.912 -0.346,0.184 -0.786,0.074 -0.985,-0.245 l -2.57399995,-3.33 c -0.019,-0.03 -0.023,-0.064 -0.036,-0.098 -0.015,-0.036 -0.03,-0.07 -0.039,-0.108 -0.0100000043,-0.043 -0.0100000043,-0.085 -0.0100000043,-0.13 0,-0.045 0,-0.086 0.0100000043,-0.13 0.008,-0.037 0.024,-0.072 0.039,-0.108 0.013,-0.034 0.017,-0.067 0.036,-0.099 z'
                fill='currentColor' />
        </svg>
    </button>

    <div class='my-slider'>

        {#each items as item (item.id)}

            <CarouselItem title={item.title} status={item.status} />

        {/each}

    </div>

    <button class='next {hasEnded ? 'hidden' : ''}' on:click={next}>
        <svg viewBox='0 0 4 8'>
            <path d='M3.919 4.337l-2.574 3.33c-.199.318-.64.428-.985.244-.344-.185-.463-.593-.263-.912l2.318-3L.097 1.001C-.103.68.017.274.36.089c.346-.184.786-.074.985.245l2.574 3.33c.019.03.023.064.036.098.015.036.03.07.039.108.01.043.01.085.01.13s0 .086-.01.13c-.008.037-.024.072-.039.108-.013.034-.017.067-.036.099z' fill='currentColor' fill-rule='evenodd'>
            </path>
        </svg>
    </button>

</section>

<style>

/*button.prev {
    padding-right: 3px;
}
button.next {
    padding-left: 3px;
}*/
section {
    display: flex;
    justify-content: center
}
button {
    margin: 0;
    border: none;
    background: none;
}
.hidden {
    visibility: hidden;
}
svg {
    width: 12px;
    height: 24px;
}

</style>