<template>
    <ul>
        <li :key='photo.id' v-for='photo in photos'>
            <Photo :photo='photo' />
        </li>
    </ul>
</template>

<script>
    import { apiKey } from '../../utils/apiKey.js';
    import Photo from './Photo.vue'
    export default {
        name: 'PhotosContainer',
        data() {
            return {
                photos: [],
                error: ''
            }
        },
        created() {
            this.fetchData()
        },
        methods: {
            fetchData: async function() {
                try {
                    const url = `https://api.unsplash.com/photos/?client_id=${apiKey}`
                    const response = await fetch(url)
                    const photos = await response.json()

                    this.photos = photos;

                } catch ({ message }) {
                    this.error = message
                }
            }
        },
        components: {
            Photo
        }
    }
</script>

<style scoped>
    ul {
        display: flex;
        flex-flow: column wrap;
        flex-wrap: wrap;
        list-style: none;
        max-height: 1000px;
        margin-left: -8px; 
        overflow: hidden;
        width: 100%;
        /* display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
        list-style: none;
        margin: 0;
        padding: 1rem; 
        /* grid-row-gap: 1rem; */
        /* grid-template-columns: repeat(6, 1fr) */
    }
</style>