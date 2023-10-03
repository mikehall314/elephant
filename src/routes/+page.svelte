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
	}

	$: total = quantity * price * (taxRateChart.get(stateCode) ?? 1);
	$: totalWithDiscount = total - getDiscount(total);
</script>

<div>Quantity: <input type="number" bind:value={quantity} /></div>
<div>Price: <input type="number" bind:value={price} /></div>
<div>State: <input type="text" bind:value={stateCode} /></div>

{#if errors.length === 0}
	<p>Total: ${Number(totalWithDiscount).toFixed(2)}</p>
{:else}
	<p>THERE ARE ERRORS:</p>
	<ul>
		{#each errors as error}
			<li>{error}</li>
		{/each}
	</ul>
{/if}
