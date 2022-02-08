<template>
  <div class="app">
    <h2>Создать пост</h2>
    <input class="input" placeholder="Название" type="text" />
    <input class="input" placeholder="Описание" type="text" />
    <div v-for="post in posts" :key="posts.id" class="post">
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
    };
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
.input {
  display: flex;
  margin-top: 15px;
  width: 100%;
  padding: 10px 15px;
  border: 1px solid teal;
  font-size: 15px;
}
  .post {
    border: 2px solid teal;
    margin-top: 15px;
    padding: 15px;
  }
</style>
