<script>
    export let mealName = '';
    export let imgSource = '';

    const showDetails = () => {

    };

</script>

<div class="meal-card">
    <h2>{mealName}</h2>
    <div class="img-container">
        <img src={imgSource} alt={mealName}>
    </div>
    <button on:click={showDetails}>Details</button>
</div>

<style>
    .meal-card {
        display: flex;
        flex-direction: column;
        align-items: center;
        overflow: hidden;
        background-color: lightskyblue;
        width: 300px;
        height: 400px;
        border-radius: 20px;
        margin: 10px;
    }

    h2 {
        text-align: center;
        max-height: 20px;
        padding: 0 10px;
    }

    .img-container {
        display: flex;
        flex-grow: 1;
        justify-content: center;
        align-items: center;
        width: 250px;;
    }

    img {
        max-width: 100%;
        max-height: 100%;
        border-radius: 20px;
        object-fit: cover;
    }

    button {
        position: relative;
        background-color: whitesmoke;
        border: none;
        border-radius: 10px;
        padding: 10px 50px;
        margin-bottom: 10px;
    }

    button:active {
        background-color: lightgray;
    }
</style>