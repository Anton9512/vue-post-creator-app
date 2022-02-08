<template>
    <div class="app">
      <post-form @create="createPost"/>
      <post-list
              :posts="posts"
      />
    </div>
</template>

<script>
  import PostList from "@/components/PostList";
  import PostForm from "@/components/PostForm";
    export default {
      components: {
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
            };
        },
        methods: {
            createPost(post) {
                this.posts.unshift(post)
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

</style>
