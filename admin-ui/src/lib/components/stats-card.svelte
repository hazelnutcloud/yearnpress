<script lang="ts">
	import * as Card from '$lib/components/ui/card';

	export let title: string;
	export let stat: string;
	export let description: string;
</script>

<Card.Root class="flex-1 min-w-max">
	<Card.Header class="flex flex-row items-center justify-between space-y-0 pb-2 gap-2">
		<Card.Title>{title}</Card.Title>
		<slot />
	</Card.Header>
	<Card.Content>
		<div class="text-3xl font-bold">{stat}</div>
		<p class="text-xs text-muted-foreground">{description}</p>
	</Card.Content>
</Card.Root>
