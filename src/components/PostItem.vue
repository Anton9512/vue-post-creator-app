<template>
    <div class="post">
        <div>
            <div>{{ post.id }}</div>
            <div><b>Название: </b>{{ post.title }}</div>
            <div><b>Описание: </b>{{ post.body }}</div>
        </div>
        <div class="post__btns">
            <my-button
                    @click="$router.push(`/posts/${post.id}`)"
            >Открыть</my-button>
            <my-button
                    @click="$emit('remove', post)"
            >Удалить</my-button>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            post: {
                type: Object,
                required: true,
            }
        },
    }
</script>

<style scoped>
    .post {
        border: 2px solid teal;
        margin-top: 15px;
        padding: 15px;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
    .post__btns {
        display: flex;
    }
</style>
