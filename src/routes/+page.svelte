<script>
    let quantity = 1;
    let price = 0;
</script>

<div>Quantity: <input type="number" bind:value={quantity}></div>
<div>Price: <input type="number" bind:value={price}></div>

<p>Total: ${quantity * price}</p>