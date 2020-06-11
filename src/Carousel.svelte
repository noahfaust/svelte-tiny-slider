<script>
    import { onMount } from 'svelte'
    import { tns } from '../node_modules/tiny-slider/src/tiny-slider'
    import CarouselItem from './CarouselItem.svelte'

    export let items

    onMount(() => {
        const slider = tns({
            "container": ".my-slider",
            "items": 3,
            "slideBy": "page",
            "mouseDrag": true,
            "swipeAngle": false,
            "speed": 400
        })
    })
    
</script>

<div class='my-slider'>

    {#each items as item (item.id)}

        <CarouselItem title={item.title} status={item.status} />

    {/each}

</div>

<style>

</style>