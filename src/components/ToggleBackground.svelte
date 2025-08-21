<script>
function toggle() {
	window.document.body.classList.toggle("light-mode");
}
</script>
<button on:click={toggle}>
	<slot/>
</button>
<style>
	button {
        
        background-color: #0084f6;
		color: black;
		
		border: none;
		border-radius: 4px;
		padding: 0.5rem;
		text-transform: uppercase;
        z-index: 99;
		
	}
	:global(body.light-mode) button {
		background-color: #f76027;
		color: white;
	}
</style>