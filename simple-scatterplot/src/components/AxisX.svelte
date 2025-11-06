<script>
    export let xScale;
    export let height;


    // console.log(xScale);
     console.log(height);  
    
    let xTicks = [0, 25, 50, 75, 100];

    
</script>

<g class="axis-x" transform="translate(0, {height})">
{#each xTicks as tick}
          
    <text x="{xScale(tick)}" y={0}>
        {tick}
    </text>
{/each}
</g>