<template>
    <div>

    </div>
</template>

<script>
    import { apiKey } from '../../utils/apiKey.js';
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
                    const url = `https://api.unsplash.com/photos/?client_id=`
                    const response = await fetch(url)
                    const photos = await response.json()

                    this.photos = photos;

                } catch ({ message }) {
                    this.error = message
                }
            }
        }
    }
</script>

<style scoped>

</style>