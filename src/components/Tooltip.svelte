<script>
    export let event;
    export let items;
</script>

<div class={`event_${event}-tooltip event_${event} tooltip`}>
    {#each Object.entries(items) as [stage, item]}
        <div class="tooltip-item">
            <img class="tooltip-item-icon" src={`images/items/${item}.png`} alt={item} />
            <span class="tooltip-item-stage">{stage}</span>
        </div>
    {/each}
</div>
