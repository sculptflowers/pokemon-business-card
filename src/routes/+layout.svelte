<script lang="ts">
	import favicon from '$lib/assets/favicon.svg';
	import "../App.css";
	import bg from '$lib/assets/background@4x.png';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	<title> Pokémon Business Card Generator </title>
</svelte:head>
<div class="min-h-screen flex flex-col bg-[#e5f1ec]" style:background-image="url({bg})">
	<main>
		{@render children()}
	</main>
</div>
