<script>
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<nav>
	<p>Navigation</p>
	<a href="/">Calender</a>
	<a href="/list">List</a>
</nav>

{@render children?.()}
