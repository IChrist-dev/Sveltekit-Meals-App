<script>
    import { onMount } from 'svelte';
    import Mealresult from "$lib/mealresult.svelte";

    let ingredientsUrl = "https://www.themealdb.com/api/json/v1/1/list.php?i=list";

    let responseReport = "";
    let searchResults = [];

    const performSearch = () => {
        searchResults = [];

        fetch(ingredientsUrl)
            .then((response) => response.json())
            .then((data) => {
                if (data && data.meals && data.meals.length > 0) {
                    responseReport = "";
                    searchResults = data.meals;
                } else {
                    responseReport =
                        "<br>Uh oh! Looks like we couldn't find anything for that search." +
                        "<br><br>Please make sure you're using the derived adjective of the country." +
                        "<br>For example, to search for food from Canada, type 'Canadian'";
                }
            })
            .catch(() => {
                alert(
                    "Oops! Looks like there was a problem performing the search. Please try again in a million years.",
                );
            });
    };

    let mealsUrl = "https://www.themealdb.com/api/json/v1/1/filter.php?i=";
    let ingredient = "";

    let searchResponse = [];

    const formatIngredient = (input) => {
        return input.toLowerCase().replace(/\s+/g, '_');
    };

    const searchMeals = () => {
        mealsUrl = "https://www.themealdb.com/api/json/v1/1/filter.php?i=" + formatIngredient(ingredient);
        searchResponse = [];

        fetch(mealsUrl)
            .then((response) => response.json())
            .then((data) => {
                // Provide feedback for bad searches
                if (data["meals"] === null) {
                    responseReport =
                        "<br>Uh oh! Looks like we couldn't find anything for that search." +
                        "<br><br>Please make sure you're selecting one ingredient on the list.";
                    searchResponse = [];
                } else {
                    responseReport = "";
                    searchResponse = data["meals"];
                }
                ingredient = "";
            })
            .catch(() => {
                alert(
                    "Oops! Looks like there was a problem performing the search. Please try again in a million years.",
                );
            });
    };

    onMount(performSearch);
</script>

<div class="ingredient">
    <h2>Search Meals by Ingredient</h2>
    <br />
    <input bind:value={ingredient} placeholder="e.g. Chicken" list="ingredientsList" />
    <datalist id="ingredientsList">
        {#each searchResults as ingredient}
            <option value={ingredient.strIngredient} />
        {/each}
    </datalist>
    <button on:click={searchMeals}>Search</button>
    <p>{@html responseReport}</p>
    <ul class="meals-list">
        {#each searchResponse as meal}
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

    .ingredient {
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
