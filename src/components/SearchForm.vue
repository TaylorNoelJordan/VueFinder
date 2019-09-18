<template>
    <div>
        <input type="text" v-model="search" placeholder="search images"/>
    </div>
</template>

<script>
    export default {
        name: 'SearchForm',
        data() {
            return {
                search: ''
            }
        }
    }
</script>

<style scoped>

</style>