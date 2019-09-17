<template>
    <main>
        <SearchForm :search='this.search'/>
        <!-- <input type='text' v-model="search" placeholder="search images"/> -->
        <ul>
            <li :key='photo.id' v-for='photo in photos'>
                <Photo :photo='photo' />
            </li>
        </ul>  
    </main>
</template>

<script>
    import { apiKey } from '../../utils/apiKey.js';
    import SearchForm from './SearchForm.vue';
    import Photo from './Photo.vue';
    export default {
        name: 'PhotosContainer',
        data() {
            return {
                photos: [],
                error: '',
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
            Photo,
            SearchForm
        }
    }
</script>

<style scoped>
    ul {
        display: flex;
        flex-flow: column wrap;
        /* flex-wrap: wrap; */
        list-style: none;
        max-height: 800px;
        margin-left: -8px; 
        /* overflow: hidden; */
        max-width: 90%;


        margin: 0;
        padding: 1rem; 
        /* grid-row-gap: 1rem; */
        /* grid-template-columns: repeat(6, 1fr) */
    }
</style>