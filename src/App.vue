<template>
    <the-header title="RememberMe"></the-header>
    <stored-resources :resources="storeResources"></stored-resources>
</template>

<script>
import TheHeader from "./components/layouts/TheHeader.vue";
import StoredResources from "./components/learning-resources/StoredResources.vue"

export default {
    components: {
        StoredResources,
        TheHeader
    },

    data() {
        return {
            storeResources: [
                {
                    id: 'official-giude',
                    tittle: 'Oficial Guide',
                    description: 'The official Vue JS Documentation',
                    link: 'https://vuejs.org'
                },
                {
                    id: 'google',
                    tittle: 'Google',
                    description: 'The official Internet search site',
                    link: 'https://www.google.com'
                },
            ]
        }
    }
}
</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

    * {
    box-sizing: border-box;
    }

    html {
    font-family: 'Roboto', sans-serif;
    }

    body {
    margin: 0;
    }
</style>