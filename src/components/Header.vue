<template>
    <header>
        <img src='../assets/4acfd3f8-2346-4b9e-950a-f36b137d2cc0_200x200.png'/>
    </header>
</template>

<script>
    import { apiKey } from '../../utils/apiKey';
    export default {
        name: 'Header',
        data() {
            return {
                search: ''
            }
        },
        methods: {
            searchPhotos: async function() {
                try {
                    const url = `https://api.unsplash.com/photos?page=1&per_page=24&query=${this.search}&client_id=${apiKey}`
                    const response = await fetch(url)
                    const queriedPhotos = await response.json();
                    this.photos = queriedPhotos
                    console.log(queriedPhotos)
                } catch ({ message }) {
                    this.error = message
                }
            }
        }
    }
</script>

<style scoped>
    h1 {
        /* position: fixed; */
        font-size: 36px;
        /* color: #fff; */
        margin: 0;
    }
    header {
        background-color: #FAF0E6;
        padding: 20px;
        color: #3d0000;
        /* margin-top: 0; */
        /* text-align: left; */
    }
</style>