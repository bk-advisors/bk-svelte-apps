<script>
    export let xScale;
    export let height;


    // console.log(xScale);
    // console.log(height);  
    
    let xTicks = [0, 25, 50, 75, 100];

    
</script>

<g class="axis-x" transform="translate(0, {height})">
{#each xTicks as tick}
    <g class='tick' transform="translate({xScale(tick)}, 0)">
      <!-- <line /> -->
      <line x1="0" x2="0" y1="0" y2="6" stroke="hsla(212, 10%, 53%, 1)" />
      <text x="0" y="6">{tick}%</text>
    </g>
{/each}
</g>