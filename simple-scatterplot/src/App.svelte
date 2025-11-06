<script>
  // This is where the logic lives
  import data from '$data/data.js';

  import { scaleLinear } from 'd3-scale';

// Dimensions
  let width = 400;
  let height = 400;

// Scales
 let xScale = scaleLinear()
   .domain([0, 100])  // input
   .range([0, width]);  // output

  let yScale = scaleLinear()
    .domain([0, 60])  // input
    .range([height, 0]);  // output

  // Import Axis components

  import AxisX from '$components/AxisX.svelte';
  import AxisY from '$components/AxisY.svelte';

</script>

<!-- Svelte each block to display data (must be in component markup, not inside <script>) -->

<svg width="{width}" height="{height}" style="border:1px solid black;">
<AxisX xScale = {xScale} height={height} />
  {#each data as d}
    <circle 
    cx="{xScale(d.grade)}" 
    cy="{yScale(d.hours)}" 
    r="5" 
    fill="blue"
    stroke="black"
    stoke-width="1" />
  {/each}
</svg>

{#each data as d}
  <p>{d.name} studied for {d.hours} hours and scored {d.grade}</p>
{/each}