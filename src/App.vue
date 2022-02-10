<template>
    <div class="app">
        <h1>Страница с постами</h1>
        <div class="app_btns">
            <my-button @click="showDialog">
                Создать пост
            </my-button>
            <my-select
                    v-model="selectedSort"
                    :options="sortOption"
            />
        </div>
        <my-dialog v-model:show="dialogVisible">
            <post-form @create="createPost"/>
        </my-dialog>
        <post-list
                :posts="sortedPosts"
                @remove="removePost"
                v-if="!isPostsLoading"
        />
        <div v-else>Идет загрузка...</div>
    </div>
</template>

<script>
    import PostList from "@/components/PostList";
    import PostForm from "@/components/PostForm";
    import MyDialog from "./components/UI/MyDialog";
    import MyButton from "./components/UI/MyButton";
    import axios from 'axios'
    import MySelect from "./components/UI/MySelect";

    export default {
        components: {
            MySelect,
            MyButton,
            MyDialog,
            PostForm,
            PostList
        },
        data() {
            return {
                posts: [],
                dialogVisible: false,
                isPostsLoading: false,
                selectedSort: '',
                sortOption: [
                    {value: 'title', name: 'По названию'},
                    {value: 'body', name: 'По описанию'},
                ],
            };
        },
        methods: {
            createPost(post) {
                this.posts.unshift(post)
                this.dialogVisible = false;
            },
            removePost(post) {
                this.posts = this.posts.filter(p => p.id !== post.id)
            },
            showDialog() {
                this.dialogVisible = true
            },
            async fetchPosts() {
                try {
                    this.isPostsLoading = true
                    const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
                    this.posts = response.data
                } catch (e) {
                    console.log(e)
                } finally {
                    this.isPostsLoading = false
                }

            },
        },
        mounted() {
            this.fetchPosts()
        },
        computed: {
            sortedPosts() {
                return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
            }
        },
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

    .app_btns {
        display: flex;
        justify-content: space-between;
        margin: 15px 0;
    }

</style>
