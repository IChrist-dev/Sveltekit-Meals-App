<script>
    import Navbar from "$lib/navbar.svelte";
    import Banner from "$lib/banner.svelte";

    let areaUrl = 'www.themealdb.com/api/json/v1/1/filter.php?a=';

    const performSearch = () => {
        console.log('searching...');
    };

</script>

<div class="by-country">
    <h2>Search Meals by Country</h2>

    <input type="text" placeholder="e.g. Canadian" />
    <button on:click={performSearch}>Search</button>
    <p></p>
</div>

<style>
    * {
        margin: 0;
        padding: 0;
    }

    .by-country {
        text-align: center;
        display: block;
        margin: 20px auto;
    }
</style>
