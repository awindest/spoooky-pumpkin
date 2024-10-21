<div class="scene">
	<slot />
</div>

<svelte:head>
	<title>Spoooky Pumpkin</title>
</svelte:head>

<style>
	.scene {
		position: absolute;
		inset: 0;
		background: radial-gradient(hsl(220 14% 20%), hsl(220 20% 10%));
	}
</style>
