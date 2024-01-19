<script>
	import NavBar from '$lib/components/navbar.svelte';
	import '../app.pcss';
	import '@carbon/charts-svelte/styles.min.css'
	import { fade } from 'svelte/transition'
</script>

<div class="flex min-h-screen flex-col">
	<NavBar />
		<slot />
</div>

<style lang='postcss'>
	:global(.cds--cc--title p.title) {
		@apply text-lg
	}
</style>