<template>
    <div>

    </div>
</template>

<script>
    export default {
        name: 'PhotosContainer',
        data() {
            return {
                photos: [],
                error: ''
            }
        },
        methods: {
            fetchData: async function() {
                try {
                    const res = await fetch('')

                } catch (error) {
                    this.error = error
                }
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>