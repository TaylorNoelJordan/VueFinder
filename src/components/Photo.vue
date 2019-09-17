<template>
  <img :src='photoPath' :alt='photo.alt_description'/>
</template>

<script>
    export default {
        props: ['photo'],
        computed: {
            photoPath: function() {
                return this.photo.urls.small
            }
        }
    }
</script>

<style scoped>
    img {
        box-shadow: 0 0 35px black;
        margin: 0 8px 8px 0;
    }
</style>