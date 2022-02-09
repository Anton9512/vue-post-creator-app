<template>
    <div v-if="posts.length > 0">
        <h3>Список постов</h3>
        <post-item
                @remove="$emit('remove', post)"
                :post="post"
                v-for="post in posts"
                :key="posts.id"
        />
    </div>
    <div v-else style="color: tomato; font-size: 20px;">
        Список постов пуст
    </div>
</template>

<script>
    import PostItem from "./PostItem";
    export default {
        components: {PostItem},
        props: {
            posts: {
                type: Array,
                required: true,
            }
        }
    }
</script>

<style scoped>

</style>
