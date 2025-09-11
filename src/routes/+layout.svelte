<script>
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<nav>
	<a href="/">Calender</a>
	<a href="/list">List</a>
</nav>

{@render children?.()}

<style>
	nav{
		background-color: grey;
		font-size: 32px;
		display: flex;
		justify-content: space-around;
		position: relative;
		top: 0px;
		right: 0px;
		left: 0px;
		height: 55px;
		align-items: center;
	}
	a{
		text-decoration: none;
		color: black;
	}
	:global(body) {
		margin: 0px; 
		padding: 0px;
	}
	@import url('https://fonts.googleapis.com/css2?family=Space+Mono&display=swap');
	*{font-family: "Space Mono", monospace;
  	font-weight: 400;
  	font-style: normal;
	}
</style>