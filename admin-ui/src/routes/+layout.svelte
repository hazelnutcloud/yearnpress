<script>
	import NavBar from '$lib/components/navbar.svelte';
	import '../app.pcss';
	import '@carbon/charts-svelte/styles.min.css'
</script>

<div class="flex min-h-screen flex-col">
	<NavBar />
	<div class="flex w-full max-w-screen-lg flex-1 flex-col gap-4 self-center p-8 pt-6">
		<slot />
	</div>
</div>
