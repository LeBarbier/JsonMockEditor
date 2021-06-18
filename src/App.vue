<template>
    <div id="app">
        <Home />
    </div>
</template>

<script>
    import Home from './components/Home.vue';

    export default {
        name: 'app',
        components: {
            Home
        }
    };
</script>

<style>
    body {
        max-width: 1024px;
        max-height: 768px;
        margin: 0 auto;
    }
</style>