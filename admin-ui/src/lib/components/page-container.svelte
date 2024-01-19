<script>
	import { slide } from 'svelte/transition';
</script>

<div class="container flex flex-col gap-4 self-center p-8 pt-6" in:slide out:slide>
	<slot />
</div>
