<script>
    let quantity = 1;
    let price = 0;
    let taxPercent = 0;

    $: taxRate = 1 + (taxPercent / 100);
    $: total = Number(quantity * price * taxRate).toFixed(2);
</script>

<div>Quantity: <input type="number" bind:value={quantity}></div>
<div>Price: <input type="number" bind:value={price}></div>
<div>Tax Rate: <input type="number" bind:value={taxPercent}></div>

<p>Total: ${total}</p>