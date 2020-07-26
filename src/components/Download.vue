<template>

<div>
    <input v-model="youtubeURL" type="text">
</div>

</template>

<script lang="vue">
export default {
name: 'download',
mounted() {
    console.log('mounted');

},

data() {
    return {
        youtubeURL: ''
    }
}



}
</script>

<style>

</style>