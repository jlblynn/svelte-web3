<script>
	import Test from './components/Test.svelte';
	import { onMount } from 'svelte';

	export let name;	

	onMount(() => {
		checkMetaMask();
	});

	function checkMetaMask() {
		const { ethereum } = window;
		return Boolean(ethereum && ethereum.isMetaMask);
	}

	function connectMetaMask() {
		ethereum.request({ method: 'eth_requestAccounts' });
	}

	let account;

	async function getAccount() {
		const accounts = await ethereum.request({ method: 'eth_requestAccounts' });
		account = accounts[0];
		console.log(account)
	}

	let etherBalance;

	async function getEtherBalance() {
		const balance = await ethereum.request({
			method: 'eth_getBalance',
			params: [
				account,
				"latest"
			],
			id: 1
		})
		etherBalance = balance;
		console.log(balance)
	}
	
</script>

<main>
	<h1>Hello {name}!</h1>
	
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>

	{#if checkMetaMask}
		<button on:click={connectMetaMask} class="enableEthereumButton">Connect</button>
		<button on:click={getAccount}>Get Account</button>
		<p>Account: {account}</p>
		<button on:click={getEtherBalance}>{etherBalance}</button>
	{/if}
	{#if account}
		<Test />
	{/if}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>