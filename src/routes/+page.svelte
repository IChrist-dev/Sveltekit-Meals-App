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
    <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Quidem amet, dolorem iusto iure accusantium quo numquam laboriosam ea illo perspiciatis laudantium culpa molestiae laborum labore a repudiandae, qui eaque harum.</p>

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
