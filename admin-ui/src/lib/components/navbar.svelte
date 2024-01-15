<script>
	import Button from "./ui/button/button.svelte";
	import Wallet from "./wallet.svelte";
	import DarkmodeToggle from "./darkmode-toggle.svelte";
</script>

<nav class="flex items-center space-x-2 border-b px-4 h-16">
	<ol class="flex items-center space-x-4">
		<li>
			<Button href="/" variant="ghost">
				<h1 class="scroll-m-20 text-xl font-extrabold tracking-tight bg">YearnPress</h1>
			</Button>
		</li>
		<li>
			<Button variant="ghost" href="/vaults" class="scroll-m-20 text-lg tracking-tight">Vaults</Button>
		</li>
	</ol>
	<div class="flex-1"></div>
	<DarkmodeToggle />
	<Wallet />
</nav>
