
<script>
    // Removed deep import into d3 internals. Use public APIs or built-in Math if needed.

    export let hoveredData = null;
    export let xScale;
    export let yScale;

    // compute safe positions (guard when hoveredData is null)
    $: xPos = hoveredData ? xScale(hoveredData.grade) : 0;
    $: yPos = hoveredData ? yScale(hoveredData.hours) : 0;
</script>

{#if hoveredData}
    <div class="tooltip" style="left: {xPos + 50}px; top: {yPos + 20}px; background: white; padding: 8px 6px; pointer-events: none;">
        <h1>{hoveredData.name} <span>{hoveredData.grade}%</span></h1>
        <h2>{hoveredData.hours} hours studied</h2>
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