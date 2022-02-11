<template>
    <div v-if="posts.length > 0">
        <h3>Список постов</h3>
        <transition-group name="post-list">
            <post-item
                    @remove="$emit('remove', post)"
                    :post="post"
                    v-for="post in posts"
                    :key="posts.id"
            />
        </transition-group>
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
    .post-list-item {
        display: inline-block;
        margin-right: 10px;
    }
    .post-list-enter-active,
    .post-list-leave-active {
        transition: all 0.4s ease;
    }
    .post-list-enter-from,
    .post-list-leave-to {
        opacity: 0;
        transform: translateX(130px);
    }
</style>
