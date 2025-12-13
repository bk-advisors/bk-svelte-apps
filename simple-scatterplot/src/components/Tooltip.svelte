
<script>
        // Tooltip dimensions
        let tooltipWidth;

        // Removed deep import into d3 internals. Use public APIs or built-in Math if needed.

        export let xScale;
        export let yScale;
        export let width;
        export let data;

        $: console.log(tooltipWidth + xPos > width, 'Tooltip width check');

        // compute safe positions (guard when hoveredData is null)
        $: xPos = data ? xScale(data.grade) : 0;
        $: yPos = data ? yScale(data.hours) : 0;

        $: isFallingOffChart = (xPos + tooltipWidth > width);

        // Nudges to position tooltip away from point
        const xNudge = 15;
        const yNudge = 30;

        // Adjust xPosition to prevent overflow
        $: xPosition = isFallingOffChart ? (xPos - tooltipWidth - xNudge ) : xPos + xNudge;
        $: yPosition = yPos + yNudge;

        import {fly} from 'svelte/transition';

</script>

{#if data}
    <div transition:fly={{y:-20}}  bind:clientWidth={tooltipWidth} class="tooltip" style="left: {xPosition}px; top: {yPosition}px; background: white; padding: 8px 6px; pointer-events: none;">
        <h1>{data.name} <span>{data.grade}%</span></h1>
        <h2>{data.hours} hours studied</h2>
    </div>
{/if}

<style>
    .tooltip {
    position: absolute;
    transition: top 0.1s ease, left 0.1s ease;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.15);
    border-radius: 4px; 

    }

    h1 {
    font-size: 1rem;
    font-weight: 500;
    margin-bottom: 6px;
    width: 100%;
}

    h2 {
    font-size: 0.8rem;
    font-weight: 300;
    text-transform: uppercase;
}

    span {
    background: #dda0dd50;
    font-size: 80%;
    margin-left: 2px;
    padding: 2px 4px;
    display: inline-block;
    vertical-align: bottom;
    border-radius: 3px;
    color: rgba(0, 0, 0, 0.7);
}
  
</style>