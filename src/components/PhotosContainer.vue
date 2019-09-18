<template>
    <main>
        <!-- <SearchForm :search='this.search'/> -->
        <div class='search-form'>
            <input type='text' v-model="search" placeholder="search images" autocomplete="off" id='search-input'/>
            <button v-on:click='searchPhotos()'>Search</button>
        </div>
        <ul>
            <li :key='photo.id' v-for='photo in photos'>
                <Photo :photo='photo' :key='photo.id'/>
            </li>
        </ul>  
    </main>
</template>

<script>
    import { apiKey } from '../../utils/apiKey.js';
    // import SearchForm from './SearchForm.vue';
    import Photo from './Photo.vue';
    export default {
        name: 'PhotosContainer',
        data() {
            return {
                photos: [],
                error: ''
            }
        },
        created() {
            this.fetchPhotos()
        },
        methods: {
            fetchPhotos: async function() {
                try {
                    const url = `https://api.unsplash.com/photos/?page=1&per_page=24&client_id=${apiKey}`
                    const response = await fetch(url)
                    const photos = await response.json()

                    this.photos = photos;

                } catch ({ message }) {
                    this.error = message
                }
            },
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
        },
        components: {
            Photo,
            // SearchForm
        }
    }
</script>

<style scoped>
    ul {
        display: flex;
        flex-flow: row wrap;
        /* flex-wrap: wrap; */
        align-items: space-evenly;
        list-style: none;
        /* height: 800px; */
        /* margin-left: -8px;  */
        width: 100%;


        /* margin: 0;
        padding: 1rem;  */
        /* grid-row-gap: 1rem; */
        /* grid-template-columns: repeat(6, 1fr) */
    }
</style>