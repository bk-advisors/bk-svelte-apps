<script>
  // This is where the logic lives
  import data from '$data/data.js';

 // console.log(data);
</script>

<!-- Svelte each block to display data (must be in component markup, not inside <script>) -->
{#each data as d}
  <p>{d.name}</p>
{/each}