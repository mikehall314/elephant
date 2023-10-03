<script>
    let quantity = 1;
    let price = 0;
    let stateCode = "UT";
    let discountPercent = 0;

    const taxRateChart = new Map([
        ["UT", 1.0685],
        ["NV", 1.08],
        ["TX", 1.0625],
        ["AL", 1.04],
        ["CA", 1.0825]
    ]);

    $: total = quantity * price * (taxRateChart.get(stateCode) ?? 1);
    $: totalWithDiscount = total - ((discountPercent / 100) * total);
</script>

<div>Quantity: <input type="number" bind:value={quantity}></div>
<div>Price: <input type="number" bind:value={price}></div>
<div>State: <input type="text" bind:value={stateCode}></div>

<div>Discount: <input type="number" bind:value={discountPercent}> %</div>

<p>Total: ${Number(totalWithDiscount).toFixed(2)}</p>

