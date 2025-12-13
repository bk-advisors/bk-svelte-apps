<script>
    export let yScale;
    export let width;

    let yTicks = yScale.ticks(4);

    console.log(yScale);
    console.log(width);
    
</script>

<g class="axis-y">
{#each yTicks as tick, index}
    <g class='tick' transform="translate(0, {yScale(tick)})">
      <line x1="0" x2={width} y1="0" y2="0" stroke={index === 0? '#8f8f8f' : '#e5e7eb'} />
      <text x="0" y="-5">
        {index === yTicks.length - 1 ? `${tick} hours studied` : tick}
      </text>
    </g>
{/each}
</g>