
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
        <strong>{hoveredData.name}</strong><br />
        Hours Studied: {hoveredData.hours}<br />
        Final Grade: {hoveredData.grade}%
    </div>
{/if}

<style>
    .tooltip {
    position: absolute;
    transition: top 0.1s ease, left 0.1s ease;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.15);
    border-radius: 4px; 

    }
  
</style>