<script>
	let quantity = 1;
	let price = 0;
	let stateCode = 'UT';
	let errors = [];

	const taxRateChart = new Map([
		['UT', 1.0685],
		['NV', 1.08],
		['TX', 1.0625],
		['AL', 1.04],
		['CA', 1.0825]
	]);

	const discounts = [
		{ threshold: 50000, rate: 0.15 },
		{ threshold: 10000, rate: 0.1 },
		{ threshold: 7000, rate: 0.07 },
		{ threshold: 5000, rate: 0.05 },
		{ threshold: 1000, rate: 0.03 }
	];

	const getDiscount = (total) => {
		const discount = discounts.find(({ threshold }) => threshold <= total);
		return discount ? total * discount.rate : 0;
	};

	$: {
		errors = [];
		if (quantity < 1) {
			errors.push('You must order at least one');
		}

		if (price < 0) {
			errors.push('Price must not be negative');
		}

		if (taxRateChart.has(stateCode) === false) {
			errors.push('State must be one of UT, NV, TX, AL, CA');
		}
	}

	$: total = quantity * price * (taxRateChart.get(stateCode) ?? 1);
	$: totalWithDiscount = total - getDiscount(total);
</script>

<h1>Mike's Super-Duper Retail Calculator</h1>

<main>
	<div>Quantity</div>
	<input type="number" bind:value={quantity} />

	<div>Price ($)</div>
	<input type="number" bind:value={price} />

	<div>State</div>
	<input type="text" bind:value={stateCode} />

	{#if errors.length === 0}
		<div class="total-row">
			<div class="total-label">Total</div>
			<div class="total-price">${Number(totalWithDiscount).toFixed(2)}</div>
		</div>
	{:else}
		<div class="error-row">
			<ul>
				{#each errors as error}
					<li>{error}</li>
				{/each}
			</ul>
		</div>
	{/if}
</main>

<style>
	:root {
		font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu,
			Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
		font-size: 11pt;
		color: #333;
	}

	main {
		display: grid;
		grid-template-columns: 5rem 15rem;
		gap: 0.2rem;
	}

	h1 {
		font-size: 1.2rem;
	}

	input[type='number'] {
		text-align: right;
	}

	.total-row {
		display: contents;
		font-size: 1.5rem;
		font-weight: bold;
	}

	.total-price {
		text-align: right;
	}

	.error-row {
		grid-column: 1 / span 2;
		color: #cc0000;
		border: #ff0000 1px solid;
		background: #cc00007f;
		border-radius: 0.5rem;
		margin: 1rem 0;
	}
</style>
