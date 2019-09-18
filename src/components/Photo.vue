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
        box-shadow: 0 0 15px #3D0000;
        flex: auto;
        height: 250px;
        min-width: 150px;
        margin: 0 8px 8px 0; 
    }

    img:hover {
        transform: scale(1.04);
        transition: all ease-in-out .3s;
    }
</style>