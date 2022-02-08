<template>
    <div class="post">
        <div>
            <div><b>Название: </b>{{ post.title }}</div>
            <div><b>Описание: </b>{{ post.body }}</div>
        </div>
        <div class="post__btns">
            <my-button>Удалить</my-button>
        </div>
    </div>
</template>

<script>
    import MyButton from "./UI/MyButton";
    export default {
        components: {MyButton},
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

    }
</style>
