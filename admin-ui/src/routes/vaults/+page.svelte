<script>
	import VaultsTable from '$lib/components/vaults-table';
	import PageContainer from '$lib/components/page-container.svelte';
</script>

<PageContainer>
	<h2 class="scroll-m-20 text-2xl font-bold">Vaults</h2>

	<div class="rounded-lg border bg-card text-card-foreground shadow-sm">
		<VaultsTable />
	</div>
</PageContainer>
