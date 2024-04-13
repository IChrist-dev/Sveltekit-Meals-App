<script>
    import Navbar from '$lib/navbar.svelte';
    import Banner from '$lib/banner.svelte';

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

<Navbar />
<Banner />

<div class="index">
    <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Quidem amet, dolorem iusto iure accusantium quo numquam laboriosam ea illo perspiciatis laudantium culpa molestiae laborum labore a repudiandae, qui eaque harum.</p>
    <input type="text" placeholder="Enter ingredient" />
    <button on:click={addIngredient}>Add Ingredient</button>
    <ul>
        {#each ingredientList as ingredient}
            <li>{ingredient}</li>
        {/each}
    </ul>
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

    ul {
        list-style-type: none;
        display: flex;
        padding: 0;
    }

    li {
        margin-right: 20px; /* Adjust as needed */
    }

</style>
