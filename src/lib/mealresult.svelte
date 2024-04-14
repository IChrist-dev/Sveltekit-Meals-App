<script>
    export let mealId = "";
    export let mealName = "";
    export let imgSource = "";

    const uniqueOverlayId = crypto.randomUUID();

    let detailName = "";
    let detailImgSource = "";
    let detailInstructions = "";
    let detailYoutubeLink = "";
    let detailIngredientsList = [];

    const hideDetails = () => {
        detailYoutubeLink = "";
        document.getElementById(uniqueOverlayId).style.display = "none";
    };

    const showDetails = () => {
        document.getElementById(uniqueOverlayId).style.display = "block";

        // Retrieve extra info from different endpoint
        let detailsUrl =
            "https://www.themealdb.com/api/json/v1/1/lookup.php?i=";
        detailsUrl = detailsUrl.concat(mealId);

        fetch(detailsUrl)
            .then((response) => response.json())
            .then((data) => {
                const featureMeal = data["meals"][0];
                detailName = featureMeal.strMeal;
                detailImgSource = featureMeal.strMealThumb;
                detailInstructions = featureMeal.strInstructions;
                // Correct modify youtube url to be embed friendly
                detailYoutubeLink = featureMeal.strYoutube.replace(
                    "watch?v=",
                    "embed/",
                );

                // Extract all ingredients from JSON. 1 - 20 are standard for all meal queries
                const tempIngredientsList = [];
                for (let i = 1; i <= 20; i++) {
                    const ingredient = featureMeal[`strIngredient${i}`];
                    if (ingredient) {
                        tempIngredientsList.push(ingredient);
                    } else {
                        // Reached end of ingredients fields
                        break;
                    }
                }

                detailIngredientsList = tempIngredientsList;
            })
            .catch(() => {
                alert(
                    "Oops! Looks like there was a problem getting details on this meal. That's a bummer.",
                );
            });
    };
</script>

<div class="detail-overlay" id={uniqueOverlayId}>
    <button class="overlay-exit" on:click={hideDetails}>X</button>
    <div class="detail-card">
        <img src={detailImgSource} alt={detailName} />
        <div class="detail-text">
            <h1>{detailName}</h1>
            <p>{detailInstructions}</p>
            <div class="lower-detail-box">
                <div class="ingredients-box">
                    <h2>Ingredients</h2>
                    <ul class="ingredients-list">
                        {#each detailIngredientsList as ingredient}
                            <li>
                                <p>{ingredient}</p>
                            </li>
                        {/each}
                    </ul>
                </div>
                <iframe
                    title="Youtube Instructional Video"
                    src={detailYoutubeLink}
                    width="300"
                    height="240"
                    frameborder="0"
                    allow="enctrypted-media *"
                    referrerpolicy="strict-origin-when-cross-origin"
                    allowfullscreen
                ></iframe>
            </div>
        </div>
    </div>
</div>

<div class="meal-card">
    <h2>{mealName}</h2>
    <div class="img-container">
        <img src={imgSource} alt={mealName} />
    </div>
    <button id="show-details-btn" on:click={showDetails}>Details</button>
</div>

<style>
    .overlay-exit {
        float: right;
        padding: 10px;
        margin: 20px;
    }

    .overlay-exit:hover {
        cursor: pointer;
    }

    .detail-overlay {
        position: fixed;
        display: none;
        width: 100%;
        height: 100%;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        background-color: rgba(0, 0, 0, 0.5);
        z-index: 2;
    }

    .detail-card {
        display: flex;
        flex-direction: row;
        width: fit-content;
        margin: auto;
        margin-top: 50px;
        padding: 20px;
        border-radius: 30px;
        background-color: white;
    }

    .detail-card img {
        max-width: 30vw;
        max-height: 30vw;
    }

    .detail-text {
        max-width: 30vw;
    }

    .detail-text p {
        text-align: left;
        padding: 20px;
        margin: 5px;
    }

    .lower-detail-box {
        display: flex;
        justify-content: space-between;
    }

    .ingredients-list {
        list-style-type: circle;
    }

    .ingredients-list li p {
        padding: 0;
    }

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
        width: 250px;
    }

    img {
        max-width: 100%;
        max-height: 100%;
        border-radius: 20px;
        object-fit: cover;
    }

    #show-details-btn {
        position: relative;
        background-color: whitesmoke;
        border: none;
        border-radius: 10px;
        padding: 10px 50px;
        margin-bottom: 10px;
    }

    #show-details-btn:active {
        background-color: lightgray;
    }

    @media (max-width: 1700px) {
        .detail-card {
            width: 80%;
        }

        .detail-card img {
            width: 100%;
        }

        .detail-text {
            max-width: 60%;
        }
    }
</style>
