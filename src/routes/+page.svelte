<script>
    let ingredientList = [];

    const addIngredient = () => {
        const inputElement = document.querySelector('input[type="text"]');
        const ingredient = inputElement.value;
        if (ingredient.trim() !== "") {
            ingredientList = [...ingredientList, ingredient];
            inputElement.value = "";
        }
    }
</script>

<div class="index">
    <p>Here is the homepage for this Svelte app. These two lines of text are defined in a component file at the top of the routing directory.</p>
    <p>When going to another route, Svelte swaps this top-level component out for whatever component file is found in the targeted route sub-folder.</p>

</div>

<style>
    * {
    margin: 0;
    padding: 0;
    }

    .index {
        text-align: center;
        display: block;
        margin: 20px auto;
    }

</style>
