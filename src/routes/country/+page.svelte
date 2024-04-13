<script>
    import Mealresult from "$lib/mealresult.svelte";

    let areaUrl = "https://www.themealdb.com/api/json/v1/1/filter.php?a=";
    let country = "";

    let responseReport = "";
    let searchResults = [];

    const performSearch = () => {
        // Update url endpoint with query value
        areaUrl = areaUrl.concat(country);

        fetch(areaUrl)
            .then((response) => response.json())
            .then((data) => {
                // Provide feedback for bad searches
                if (data["meals"] === null) {
                    responseReport =
                        "Uh oh! Looks like we couldn't find anything for that search." +
                        "<br><br>Please make sure you're using the derived adjective of the country." +
                        "<br>For example, to search for food from Canada, type 'Canadian'";
                } else {
                    responseReport = "";

                    searchResults = data['meals'];
                }
            })
            .catch(() => {
                alert(
                    "Oops! Looks like there was a problem performing the search. Please try again in a million years.",
                );
            });
    };
</script>

<div class="by-country">
    <h2>Search Meals by Country</h2>
    <br/>
    <input bind:value={country} placeholder="e.g. Canadian" />
    <button on:click={performSearch}>Search</button>
    <p>{@html responseReport}</p>
    <ul class="meals-list">
        {#each searchResults as meal}
        <li>
            <Mealresult
            key={meal.idMeal}
            mealName={meal.strMeal}
            imgSource={meal.strMealThumb}
        />
        </li>
    {/each}
    </ul>
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

    .meals-list {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: space-evenly;
        list-style-type: none;
    }
</style>
