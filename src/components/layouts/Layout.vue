<script setup>

</script>

<template>
    <header>
        <h1 class="text-gradient">App Header</h1>
    </header>
    <main>
        <slot />
    </main>
    <footer>
        <small>Created by</small>
        <a href="https://github.com/YuriiShcherba">
            <img src="https://avatars.githubusercontent.com/u/146816809?s=400&u=d72016333205f3962c8cfd519d62192789d41673&v=4" alt="pfp"/>
            Yuriy Scherba <i class="fa-brands fa-github"></i>
        </a>
        <p>Thanks to jamezmca for course meterials</p>
    </footer>
</template>

<style scoped>
    header, footer, main {
        padding: 1rem;
        max-width: 700px;
        margin: 0 auto;
    }
    main {
        flex: 1;
    }

    footer {
        display: flex;
        flex-direction: column;
        gap: 0.5rem;
        align-items: center;
        padding: 2rem 0 0.5rem;
    }

    footer a {
        display: flex;
        align-items: center;
        gap: 0.5rem;
        padding: 0.3rem;
        padding-right: 0.5rem;
        background: var(--background-muted);
        border-radius: 4rem;
        border: 1px solid transparent;
        transition-duration: 200ms;
        text-decoration: none;
    }

    footer a:hover {
        border-color: var(--color-link)
    }

    footer a img {
        max-width: 30px;
        aspect-ratio: 1 / 1;
        border-radius: 100%;
    }
</style>
