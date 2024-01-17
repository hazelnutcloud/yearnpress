<script lang="ts">
	import ChartCard from '$lib/components/chart-card.svelte';
	import StatsCard from '$lib/components/stats-card.svelte';
	import * as Card from '$lib/components/ui/card';
	import RecentTxsTable from "$lib/components/recent-txs-table/table.svelte"
	import { Vault, TrendingUp, DollarSign } from 'lucide-svelte';
	import { AreaChart, ChartTheme, ScaleTypes } from '@carbon/charts-svelte';
	import { mode } from "mode-watcher"

	const now = Date.now();
	const data = Array.from({ length: 12 }).map((_, i) => {
		return {
			date: new Date(now - 1000 * 60 * 60 * 24 * 30 * (12 - i)),
			value: Math.random() * 1000,
			group: 'Revenue'
		};
	});
</script>

<h2 class="scroll-m-20 text-2xl font-bold">Overview</h2>

<div class="flex flex-wrap items-center justify-center gap-4">
	<StatsCard title="Total Value Locked" stat="$42,690" description="+20% from yesterday"
		><Vault /></StatsCard
	>
	<StatsCard title="24h Revenue" stat="$5,432" description="+5% from yesterday"
		><DollarSign /></StatsCard
	>
	<StatsCard title="3d APY" stat="42%" description="+2% from yesterday"><TrendingUp /></StatsCard>
</div>

<ChartCard>
	<AreaChart
		{data}
		options={{
			axes: {
				bottom: { mapsTo: 'date', scaleType: ScaleTypes.TIME },
				left: { mapsTo: 'value', scaleType: ScaleTypes.LINEAR }
			},
			height: '300px',
			theme: $mode === 'dark' ? ChartTheme.G90 : ChartTheme.G10,
			title: 'Monthly Revenue'
		}}
	/>
</ChartCard>

<Card.Root>
	<Card.Header>
		<Card.Title>
			Recent Transactions
		</Card.Title>
	</Card.Header>
	<Card.Content>
		<RecentTxsTable />
	</Card.Content>
</Card.Root>
