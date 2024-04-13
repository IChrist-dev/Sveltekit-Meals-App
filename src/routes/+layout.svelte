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
</main>

<style>
    header {
        display: flex;
        flex-direction: column;
        justify-content: center;
    }

    main {
        max-width: 1000px;
        margin: 20px auto;
    }
</style>