<script>
    export let mealId = "";
    export let mealName = "";
    export let imgSource = "";

    const uniqueOverlayId = crypto.randomUUID();

    let detailName = "";
    let detailImgSource = "";
    let detailInstructions = "";
    let detailYoutubeLink = "";

    const hideDetails = () => {
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
                detailYoutubeLink = featureMeal.strYoutube;
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
            <iframe title="Youtube Instructional Video" width="630" height="354" src={detailYoutubeLink} frameborder="0"></iframe>
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

    .detail-text {
        max-width: 30vw;
    }

    .detail-text p {
        text-align: left;
        padding: 20px;
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
</style>
