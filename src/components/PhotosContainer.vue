<template>
    <main>
        <div class='search-form'>
            <input type='text' v-model="search" placeholder="search images" autocomplete="off" id='search-input'/>
            <button class='search-button' v-on:click='searchPhotos'>Search</button>
        </div>
        <div v-if="currentSearch">
            <p class='current-search'>Displaying images related to {{ currentSearch }}</p>
        </div>
        <div v-else-if='error'>
            <p>{{ error }}</p>
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
    import Photo from './Photo.vue';
    export default {
        name: 'PhotosContainer',
        data() {
            return {
                photos: [],
                error: '',
                search: '',
                currentSearch: ''
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
                    const url = `https://api.unsplash.com/search/photos?page=1&per_page=24&query=${this.search}&client_id=${apiKey}`
                    const response = await fetch(url)
                    const queriedPhotos = await response.json();
                    
                    if(queriedPhotos == undefined) {
                        this.currentSearch = ''
                        this.error = 'No photos match your search'
                    } else {
                        this.currentSearch = this.search
                        this.search = ''
                        this.photos = queriedPhotos.results;
                    }


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
        flex-flow: row wrap;
        align-items: space-evenly;
        list-style: none;
        width: 100%;
    }

    #search-input {
        border-radius: 15px;
        font-size: 1.2em;
        height: 30px;
        letter-spacing: 1px;
        margin: 5px;
        padding: 5px;
        width: 200px;
    }

    .search-button {
        height: 30px;
        border-radius: 15px;
        padding: 5px;
        font-size: 1em;
        font-weight: 200;
        letter-spacing: 1px;
        width: 80px;
    }

    .search-button:hover {
        background-color: #3d0000;
        color: #FAF0E6;
    }
    .search-form {
        display: flex;
        justify-content: center;
        align-items: center;
    }
</style>