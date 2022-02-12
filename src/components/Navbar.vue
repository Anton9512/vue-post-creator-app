<template>
    <div class="navbar">
        <div @click="$router.push('/')" style="cursor: pointer">Vue</div>
        <div class="navbar__btns">
            <my-button @click="$router.push('/about')">Описание</my-button>
            <my-button
                    @click="$router.push('/posts')"
                    style="margin-left: 20px"
            >Посты</my-button>
        </div>
    </div>
</template>

<script>
    export default {
    }
</script>

<style scoped>
 .navbar {
     height: 50px;
     background: lightgrey;
     box-shadow: 2px 2px 4px gray;
     display: flex;
     align-items: center;
     padding: 0 15px;
 }
    .navbar__btns {
        margin-left: auto;
    }
</style>
