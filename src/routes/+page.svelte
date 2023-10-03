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

<table>
    <tr>
        <th>State</th>
        <th>Rate</th>
    </tr>
    <tr>
        <td>UT</td>
        <td>6.85%</td>
    </tr>
    <tr>
        <td>NV</td>
        <td>8.00%</td>
    </tr>
    <tr>
        <td>TX</td>
        <td>6.25%</td>
    </tr>
    <tr>
        <td>AL</td>
        <td>4.00%</td>
    </tr>
    <tr>
        <td>CA</td>
        <td>8.25%</td>
    </tr>
</table>