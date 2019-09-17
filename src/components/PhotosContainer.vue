<template>
    <div>

    </div>
</template>

<script>
    import { apiKey } from '../utils/apiKey.js'
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
                    const res = await fetch(`https://api.unsplash.com/photos/?client_id=${apiKey}`)
                    const photos = res.json();
                    this.photos = photos;
                } catch (error) {
                    this.error = error
                }
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>