<script lang="ts">
	import { createTable, Render, Subscribe } from 'svelte-headless-table';
	import { readable } from 'svelte/store';
	import * as Table from '$lib/components/ui/table';

	type Vault = {
		tvl: number;
		apr: number;
		chain: string;
		tokenAddress: string;
		tokenName: string;
		vaultAddress: string;
		vaultName: string;
	};

	const vaults: Vault[] = [
		{
			apr: 20,
			chain: 'polygon',
			tokenAddress: '0x1234',
			tokenName: 'USDC',
			tvl: 100,
			vaultAddress: '0x1234',
			vaultName: 'USDC Vault'
		},
		{
			apr: 20,
			chain: 'polygon',
			tokenAddress: '0x1234',
			tokenName: 'USDC',
			tvl: 100,
			vaultAddress: '0x1234',
			vaultName: 'USDC Vault'
		}
	];

	const table = createTable(readable(vaults));

	const columns = table.createColumns([
		table.column({
			accessor: 'vaultName',
			header: 'Vault'
		}),
		table.column({
			accessor: 'chain',
			header: 'Chain'
		}),
		table.column({
			accessor: 'apr',
			header: 'APR'
		}),
		table.column({
			accessor: 'tvl',
			header: 'TVL'
		})
	]);

	const { headerRows, pageRows, tableAttrs, tableBodyAttrs } = table.createViewModel(columns);
</script>

<Table.Root {...$tableAttrs}>
	<Table.Header>
		{#each $headerRows as headerRow}
			<Subscribe rowAttrs={headerRow.attrs()}>
				<Table.Row>
					{#each headerRow.cells as cell (cell.id)}
						<Subscribe attrs={cell.attrs()} let:attrs props={cell.props()}>
							<Table.Head {...attrs}>
								{#if cell.id === 'apr' || cell.id === 'tvl'}
									<div class="text-right">
										<Render of={cell.render()} />
									</div>
								{:else}
									<Render of={cell.render()} />
								{/if}
							</Table.Head>
						</Subscribe>
					{/each}
				</Table.Row>
			</Subscribe>
		{/each}
	</Table.Header>
	<Table.Body {...$tableBodyAttrs}>
		{#each $pageRows as row (row.id)}
			<Subscribe rowAttrs={row.attrs()} let:rowAttrs>
				<Table.Row {...rowAttrs}>
					{#each row.cells as cell (cell.id)}
						<Subscribe attrs={cell.attrs()} let:attrs>
							<Table.Cell {...attrs}>
								{#if cell.id === 'apr' || cell.id === 'tvl'}
									<div class="text-right">
										<Render of={cell.render()} />
									</div>
								{:else}
									<Render of={cell.render()} />
								{/if}
							</Table.Cell>
						</Subscribe>
					{/each}
				</Table.Row>
			</Subscribe>
		{/each}
	</Table.Body>
</Table.Root>
