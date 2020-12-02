<script>
    import { onMount } from 'svelte';
    import CryptoCard from './CryptoCard.svelte';

    let cryptoPrices;

    onMount(async () => {
      const returnValue = await fetch(`https://api.coingecko.com/api/v3/simple/price?ids=chainlink%2Clitecoin%2Cbitcoin%2Cethereum&vs_currencies=usd`);
      await returnValue.json().then(data => {
          let cryptoPricesKey = Object.keys(data);
          cryptoPrices = [];
          cryptoPricesKey.forEach(key => {
            cryptoPrices.push({name: key, currentPrice: data[key].usd});
          });
        });
    });
</script>

<style>
    .cards {
        display: grid;
        /* grid-template-columns: 1fr 1fr;
	grid-template-rows: auto auto; */
    grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  grid-gap: 10px;
    }
</style>

{#if cryptoPrices}
<div class="cards">
    {#each cryptoPrices as crypto, i}
        <CryptoCard {crypto} {i} />
	{/each}
</div>
{:else}
	<p class="loading">Loading...</p>
{/if}




<!-- <p>
    Bitcoin Price: ${chainlinkData?.bitcoin?.usd}
</p>
<p>
    Ethereum Price: ${chainlinkData?.ethereum?.usd}
</p>
<p>
    Litecoin Price: ${chainlinkData?.litecoin?.usd}
</p>
<p>
    Chainlink Price: ${chainlinkData?.chainlink?.usd} 
</p> -->
