<div class="max-w-md mx-auto flex p-12 bg-gray-100 mt-12 rounded-lg shadow-xl">
	<div class="mx-6 pt-1">
		<img class="object-scale-down h-48 w-full mb-12" src="/logo.png"/>
		<h1 class="text-2xl text-blue-700 leading-tight text-center">
			Rastreamento Correios
		</h1>
		{#if mode === 'track'}
			<form class="w-full max-w-sm pt-4" on:submit|preventDefault={track}>
				<div class="flex items-center border-b border-blue-700 py-2">
					<input class="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none" type="text" placeholder="Código de rastreamento" id="code" required/>
					<button class="flex-shrink-0 bg-blue-700 hover:bg-blue-700 border-blue-700 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded" type="submit">
						Rastrear
					</button>
				</div>
			</form>
			<button class="object-scale-down w-full mt-6 bg-blue-700 hover:bg-blue-300 text-white font-semibold py-2 px-4 border border-gray-400 rounded shadow uppercase" on:click={see}>
				Meus Pedidos
			</button>
		{:else if mode === 'details'}
			<div>
				<div className="flex flex-wrap flex-col md:flex-row py-2">
					<Details code="{order}"/>
				</div>
				<button class="object-scale-down w-full bg-blue-700 hover:bg-blue-300 text-white font-semibold py-2 px-4 border border-gray-400 rounded shadow uppercase" on:click={reset}>
					Voltar
				</button>
			</div>
		{:else}
			<div class="flex flex-wrap flex-col md:flex-row py-2">
				{#each orders as ord}
					<Order code={ord} on:removed={remove} on:detailed={details}/>
				{/each}
			</div>
			<button class="object-scale-down w-full bg-blue-700 hover:bg-blue-300 text-white font-semibold py-2 px-4 border border-gray-400 rounded shadow uppercase" on:click={reset}>
				Voltar
			</button>
		{/if}
	</div>
</div>

<script>
  import Order from './Order.svelte'
	import Details from './Details.svelte'

  let orders = []
	let order = null
	let mode = 'track'

  function track(event) {
		orders.push(event.target.code.value)
		mode = 'orders'
  }

  function reset() {
    mode = 'track'
  }

	function see() {
    mode = 'orders'
  }

  function remove(event) {
		orders = orders.filter(function(order) {return order !== event.detail});
		mode = 'track';
  }

	function details(event) {
		order = event.detail;
		mode = 'details';
  }
</script>

<style>

</style>
