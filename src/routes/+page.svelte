<script>
    let quantity = 1;
    let price = 0;

    const taxRate = 1.0685

    $: total = Number(quantity * price * taxRate).toFixed(2);
</script>

<div>Quantity: <input type="number" bind:value={quantity}></div>
<div>Price: <input type="number" bind:value={price}></div>

<p>Total: ${total}</p>