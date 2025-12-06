<script>
  // This is where the logic lives
  import data from '$data/data.js';

  import { scaleLinear } from 'd3-scale';

// Dimensions
  let width = 400;
  let height = 400;

  const margin = {
    right: 20,
    left: 40,
    top: 20,
    bottom: 25
  }

  $: innerWidth = width - margin.left - margin.right;
  let innerHeight = height - margin.top - margin.bottom;

// Scales
 $: xScale = scaleLinear()
   .domain([0, 100])  // input
   .range([0, innerWidth]);  // output

  let yScale = scaleLinear()
    .domain([0, 60])  // input
    .range([innerHeight, 0]);  // output

  // Import Axis components

  import AxisX from '$components/AxisX.svelte';
  import AxisY from '$components/AxisY.svelte';
  // removed deep import from d3-scale; use Math.log or the public d3 API if needed

  // Tooltip state
  let hoveredData = null;
 // $: console.log('Hovered data:', hoveredData);

  // Import Tooltip component
  import Tooltip from '$components/Tooltip.svelte';

</script>

<!-- Svelte each block to display data (must be in component markup, not inside <script>) -->
<div class="scatterplot-container" bind:clientWidth={width}>
<svg width={width} height={height} style="border:1px solid black;">
  <g transform="translate({margin.left}, {margin.top})">  
<AxisX xScale={xScale} height={innerHeight} width={innerWidth} />
<AxisY yScale={yScale} width={innerWidth} />
  {#each data as d}
    <circle
      cx={xScale(d.grade)}
      cy={yScale(d.hours)}
      r={5}
      fill="purple"
      stroke="black"
      stroke-width="1"
      on:mouseover={() => hoveredData = d}
      on:focus={() => hoveredData = d}
    />
  {/each}
  </g>
</svg>
{#if hoveredData}
<Tooltip data={hoveredData} {xScale} {yScale} width={innerWidth} />
{/if}
</div>

<style>
  /* Component styles go here */

  :global(.tick text, .axis-title) {
    font-weight: 400;
    font-size: 10px;
    fill: #6b7280; /* Tailwind gray-500 */
  }

  .scatterplot-container {
    position: relative;
  }

</style>