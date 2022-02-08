<template>
    <div class="post" v-for="post in posts" :key="posts.id">
        <div><b>Название: </b>{{ post.title }}</div>
        <div><b>Описание: </b>{{ post.body }}</div>
    </div>
</template>

<script>
    export default {
        props: {
            posts: {
                type: Array,
                required: true,
            }
        }
    }
</script>

<style scoped>
    .post {
        border: 2px solid teal;
        margin-top: 15px;
        padding: 15px;
    }
</style>
