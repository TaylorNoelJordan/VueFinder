<template>
    <div>
        <input type="text" v-model="search" placeholder="search images"/>
    </div>
</template>

<script>
    export default {
        name: 'SearchForm',
        props: {
            query: String
        }
    }
</script>

<style scoped>

</style>