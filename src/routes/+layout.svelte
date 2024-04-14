<script>
    import Navbar from '$lib/navbar.svelte';
    import Banner from '$lib/banner.svelte';
</script>

<header>
    <Navbar />
    <Banner />
</header>

<main>
    <slot></slot>
    <p>This line of text is defined in the top-level layout file. All pages will see this.</p>
</main>

<footer>
    <p>Data provided by <a href="https://www.themealdb.com/">www.themealdb.com</a></p>
</footer>

<style>
    * {
        font-family: Arial, Helvetica, sans-serif;
    }

    header {
        display: flex;
        flex-direction: column;
        justify-content: center;
    }

    main {
        max-width: 1000px;
        margin: 20px auto;
    }

    p {
        text-align: center;
    }

    footer {
        text-align: center;
    }
</style>