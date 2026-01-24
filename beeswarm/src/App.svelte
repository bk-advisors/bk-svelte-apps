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
  const simulation = forceSimulation(data)
    .force("x" , forceX().x(d => d.happiness).strength(0.8)) // Apply a force along the X axis based on happiness
    .force("y" , forceY().y(d => d.continent).strength(0.2)) // Apply a force along the Y axis based on continent
    .force("collide" , forceCollide().radius(RADIUS)); // Apply a collision force


  console.log( simulation.nodes() );

  // Step 3 - Setup infrastructure for a basic chart 


</script>

<main>

</main>

<style>

</style>
