<script lang="ts">
	import { createTable, Render, Subscribe } from 'svelte-headless-table';
	import { readable } from 'svelte/store';
	import * as Table from '$lib/components/ui/table';

	type Transaction =
		| {
				hash: string;
				from: string;
				to: string;
				function: 'deposit' | 'withdraw';
				amount: number;
		  }
		| {
				hash: string;
				from: string;
				to: string;
				function: 'rebalance';
				amount?: never;
		  };

	const transactions: Transaction[] = [
		{
			function: 'deposit',
			amount: 100,
			from: '0x1234',
			to: '0x5678',
			hash: '0x1234'
		},
		{
			function: 'rebalance',
			from: '0x1234',
			hash: '0x1234',
			to: '0x5678'
		}
	];

	const table = createTable(readable(transactions));

	const columns = table.createColumns([
		table.column({
			accessor: 'hash',
			header: 'Tx Hash'
		}),
		table.column({
			accessor: 'from',
			header: 'From'
		}),
		table.column({
			accessor: 'to',
			header: 'To'
		}),
		table.column({
			accessor: 'function',
			header: 'Function',
			cell: ({ value }) => value.charAt(0).toUpperCase() + value.slice(1)
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
								<Render of={cell.render()} />
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
								<Render of={cell.render()} />
							</Table.Cell>
						</Subscribe>
					{/each}
				</Table.Row>
			</Subscribe>
		{/each}
	</Table.Body>
</Table.Root>
