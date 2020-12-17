<script>
	import Nested from "./Nested.svelte";

	let name = "Svelte!";

	let count = 0;
	$: doubled = count * 2;

	function handleClick() {
		count += 1;
	}

	// reactivity is only triggered by assignements, so .push doesn't cause an update
	$: if (count>=0) { 
		console.log("the count is high af");
	}
</script>

<style>

	main {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
	h1 {
		text-align: center;
		font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
		font-size: 2em;
	}
</style>

<main>
	<h1>Hello {name.toUpperCase()}</h1>
	<Nested />

	<button on:click={handleClick}>
		Clicked {count} {count === 1 ? 'time' : 'times'}
	</button>

	<p>and doubled is {doubled}</p>
</main>