<template>
    <div class="app">
        <h1>Страница с постами</h1>
        <my-button @click="showDialog">
            Создать пост
        </my-button>
        <my-dialog v-model:show="dialogVisible">
            <post-form @create="createPost"/>
        </my-dialog>
      <post-list
              :posts="posts"
              @remove="removePost"
      />
    </div>
</template>

<script>
  import PostList from "@/components/PostList";
  import PostForm from "@/components/PostForm";
  import MyDialog from "./components/UI/MyDialog";
  import MyButton from "./components/UI/MyButton";
    export default {
      components: {
          MyButton,
          MyDialog,
        PostForm,
        PostList
      },
        data() {
            return {
                posts: [
                    {id: 1, title: 'js 1', body: 'description js 1'},
                    {id: 2, title: 'js 2', body: 'description js 2'},
                    {id: 3, title: 'js 3', body: 'description js 3'},
                ],
                dialogVisible: false,
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

</style>
