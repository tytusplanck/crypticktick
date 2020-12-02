<script>
export let crypto;
</script>

<style>
    .card {
        border-style: solid;
        border-radius: 5px;
        border-color: black;
        padding: 75px;
    }
</style>

<div class="card">
    <p>
        {crypto.name} Price: ${crypto.currentPrice}
    </p>
</div>
