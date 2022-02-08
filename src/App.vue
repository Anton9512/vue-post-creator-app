<template>
    <div class="app">
        <form>
            <h4>Создание поста</h4>
            <input v-model="title" class="input" type="text" placeholder="Название">
            <input v-model="body" class="input" type="text" placeholder="Описание">
            <button class="btn" @click.prevent="createPost">Создать</button>
        </form>
        <div class="post" v-for="post in posts" :key="posts.id">
            <div><b>Название: </b>{{ post.title }}</div>
            <div><b>Описание: </b>{{ post.body }}</div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                posts: [
                    {id: 1, title: 'js 1', body: 'description js 1'},
                    {id: 2, title: 'js 2', body: 'description js 2'},
                    {id: 3, title: 'js 3', body: 'description js 3'},
                ],
                title: '',
                body: '',
            };
        },
        methods: {
            createPost() {
                const newPost = {
                    id: Date.now(),
                    title: this.title,
                    body: this.body,
                }
                this.posts.unshift(newPost)
                this.title = '';
                this.body = '';
            }
        }
    };
</script>

<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        font-family: serif;
    }

    .app {
        padding: 20px;
    }

    .input {
        width: 100%;
        border: 1px solid teal;
        margin-top: 15px;
        padding: 10px 15px;
    }

    form {
        display: flex;
        flex-direction: column;

    }

    .btn {
        margin: 15px 0;
        align-self: flex-end;
        padding: 10px 15px;
        background: transparent;
        color: teal;
        border: 1px solid teal;
        cursor: pointer;
    }

    .post {
        border: 2px solid teal;
        margin-top: 15px;
        padding: 15px;
    }
</style>
