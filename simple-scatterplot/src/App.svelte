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

  innerWidth = width - margin.left - margin.right;
  innerHeight = height - margin.top - margin.bottom;

// Scales
 let xScale = scaleLinear()
   .domain([0, 100])  // input
   .range([0, innerWidth]);  // output

  let yScale = scaleLinear()
    .domain([0, 60])  // input
    .range([innerHeight, 0]);  // output

  // Import Axis components

  import AxisX from '$components/AxisX.svelte';
  import AxisY from '$components/AxisY.svelte';

</script>

<!-- Svelte each block to display data (must be in component markup, not inside <script>) -->

<svg width="{width}" height="{height}" style="border:1px solid black;">
  <g transform="translate({margin.left}, {margin.top})">  
<AxisX xScale = {xScale} height={innerHeight} />
<AxisY yScale = {yScale} width={innerWidth} />
  {#each data as d}
    <circle 
    cx="{xScale(d.grade)}" 
    cy="{yScale(d.hours)}" 
    r="5" 
    fill="blue"
    stroke="black"
    stoke-width="1" />
  {/each}
  </g>
</svg>

{#each data as d}
  <p>{d.name} studied for {d.hours} hours and scored {d.grade}</p>
{/each}