<script lang="ts">
	import Button from '$lib/components/ui/button/button.svelte';
	import { Sun, Moon } from 'lucide-svelte';
	import { toggleMode, userPrefersMode, setMode, mode } from 'mode-watcher';
	import { onMount } from 'svelte';

	onMount(() => {
		if ($userPrefersMode === 'system') {
			setMode('dark');
		}
	});

	// fix for weird bug where color mode doesn't update on some pages
	const toggle = () => {
		toggleMode();
		$mode
	};
</script>

<Button on:click={toggle} variant="ghost" size="icon">
	<Sun
		class="h-[1.2rem] w-[1.2rem] rotate-0 scale-100 transition-all dark:-rotate-90 dark:scale-0"
	/>
	<Moon
		class="absolute h-[1.2rem] w-[1.2rem] rotate-90 scale-0 transition-all dark:rotate-0 dark:scale-100"
	/>
	<span class="sr-only">Toggle theme</span>
</Button>
