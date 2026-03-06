<script lang="ts">
	import favicon from '$lib/assets/favicon.ico';
	import './main.scss';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	<title>Miku Apology Letter Generator</title>
</svelte:head>

{@render children()}
