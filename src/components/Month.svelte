<script>
	import Episode from "./Episode.svelte";
	import Event from "./Event.svelte";
	import IS from "./IS.svelte";

	export let date, eventDivs, episodeDivs, isDivs;

	const [y, m] = date;
	const days = new Date(y, m + 1, 0).getDate();

	date = new Date(...date);
	const monthName = date.toLocaleString("en", { month: "long" });
	const firstDay = date.getDay();
	const sundayStart = firstDay === 0;

	const events = eventDivs?.[y]?.[m];
	const episodes = episodeDivs?.[y]?.[m];
	const is = isDivs?.[y]?.[m];
	const today = new Date();
</script>

<section class:no-margin={sundayStart}>
	<h1>{monthName} <span>{y}</span></h1>
	<div class="calendar">
		{#each Array(days) as _, index}
			{				
				@const is_today = (
					today.getDate() === index+1 &&
					today.getMonth() === date.getMonth() &&
					today.getFullYear() === date.getFullYear()
				)
			}
			{#if (index === 0 && !sundayStart)}
				{#if is_today}	
					<div style="--grid-start:{firstDay + 1}" data-today={is_today}></div>
				{:else}
					<div style="--grid-start:{firstDay + 1}"></div>
				{/if}
			{:else}
				{#if is_today}	
					<div data-today={is_today}></div>
				{:else}
					<div></div>
				{/if}
			{/if}
		{/each}
	</div>
	{#if events || episodes || is}
		<div class="overlay">
			{#if events}
				{#each events as event}
					<Event div={event}/>
				{/each}
			{/if}
			{#if episodes}
				{#each episodes as episode}
					<Episode div={episode}/>
				{/each}
			{/if}
			{#if is}
				{#each is as isDiv}
					<IS div={isDiv}/>
				{/each}
			{/if}
		</div>
	{/if}
</section>
