<script>
  // Step 1 - Import data and necessary functions from d3-force
  import data from "$data/data.js";
  import { 
    forceSimulation, // This function creates a new force simulation
    forceY, // This function applies a force along the Y axis
    forceX, // This function applies a force along the X axis
    forceCollide // This function applies a collision force
   } from "d3-force";

  console.log(data);

  // Step 2 - Setup a force simulation
  const RADIUS = 5;
  $: simulation = forceSimulation(data)
    .force("x" , forceX().x(d => xScale(d.happiness)).strength(0.8)) // Apply a force along the X axis based on happiness
    .force("y" , forceY().y(d => yScale(d.continent)).strength(0.2)) // Apply a force along the Y axis based on continent
    .force("collide" , forceCollide().radius(RADIUS)); // Apply a collision force

  $: nodes = simulation.nodes(); // Get the nodes from the simulation

  $: console.log( nodes );

  // Step 3 - Setup infrastructure for a basic chart 

  let width = 400, height = 400;

  let margin = { top: 0, right: 0, bottom: 20, left: 0 };
  $: innerWidth = width - margin.left - margin.right;
  let innerHeight = height - margin.top - margin.bottom;

  // Step 4 - Create scales for positioning
  
  import { scaleLinear, scaleBand } from "d3-scale";
  $: xScale = scaleLinear()
    .domain([1, 9]) // Input domain for happiness scores
    .range([0, innerWidth]); // Output range for the chart width
  
  // Step 5 - Sort continents by average happiness
  // Generate the average for each continent, so that we can sort according to that
  const continents = rollups(
      data,
      v => mean(v, d => d.happiness),
      d => d.continent
    ) // Group data by continent and return the group-wide mean
    .sort((a, b) => a[1] - b[1]) // Sort according to value
    .map(d => d[0]); // Grab the continent name

  let yScale = scaleBand()
    .domain(continents) // Input domain for continents
    .range([0, innerHeight]) // Output range for the chart height
    .paddingOuter(0.5);  

    console.log(yScale.domain());

    import { mean, rollups } from "d3-array";



</script>

<main>
  <div class='chart-container' bind:clientWidth={width}> <!-- Step 3.1 - Create a container for the chart -->
    <svg {width} {height}>
      <g class="inner-chart" transform="translate({margin.left}, {margin.top})">
        {#each nodes as node} <!-- Step 5.1 - Render circles for each data point -->
        <circle 
        cx={node.x} 
        cy={node.y} 
        r={RADIUS} 
        fill="steelblue" />
        {/each}
      </g>
    </svg>
  </div>

</main>

<style>

</style>
