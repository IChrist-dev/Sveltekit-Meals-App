<script>
    import Mealresult from "$lib/mealresult.svelte";

    let mealUrl = "https://www.themealdb.com/api/json/v1/1/search.php?s=";
    let mealSearch = "";

    let responseReport = "";
    let searchResults = [];

    const performSearch = () => {
        // Update url endpoint with query value
        mealUrl = mealUrl.concat(mealSearch);
        mealUrl = mealUrl.replace(" ", "_");
        searchResults = [];

        console.log(mealUrl)
        fetch(mealUrl)
            .then((response) => response.json())
            .then((data) => {
                // Provide feedback for bad searches
                if (data["meals"] === null) {
                    responseReport =
                        "<br>Uh oh! Looks like we couldn't find anything for that search." +
                        "<br><br>Please make sure you're using the derived adjective of the country." +
                        "<br>For example, to search for food from Canada, type 'Canadian'";
                    searchResults = [];
                } else {
                    responseReport = "";
                    searchResults = data["meals"];
                }

                // Cleanup variables for next search
                mealUrl = mealUrl.replace(mealSearch, "");
                mealSearch = "";
            })
            .catch(() => {
                alert(
                    "Oops! Looks like there was a problem performing the search. Please try again in a million years.",
                );
            });
    };
</script>

<div class="by-meal">
    <h2>Searh by Meal Name</h2>
    <br />
    <input bind:value={mealSearch} placeholder="e.g. Canadian" />
    <button on:click={performSearch}>Search</button>
    <p>{@html responseReport}</p>
    <ul class="meals-list">
        {#each searchResults as meal}
            <li>
                <Mealresult
                    mealId={meal.idMeal}
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

    .by-meal {
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
