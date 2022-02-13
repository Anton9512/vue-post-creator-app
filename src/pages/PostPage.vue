<template>
    <div >
        <h1>Страница с постами</h1>
        <my-input
                v-focus
                v-model="searchQuery"
                placeholder="Поиск..."
        />
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
        <div class="page__wrapper">
            <div
                    v-for="pageNumber in totalPages"
                    :key="pageNumber"
                    class="page"
                    :class="{
                        'current-page': page === pageNumber
                    }"
                    @click="changePage(pageNumber)"
            >
                {{ pageNumber }}
            </div>
        </div>
        <post-list
                :posts="sortedAndSearchedPosts"
                @remove="removePost"
                v-if="!isPostsLoading"
        />
        <div v-else>Идет загрузка...</div>
    </div>
</template>

<script>
    import PostList from "@/components/PostList";
    import PostForm from "@/components/PostForm";
    import axios from 'axios'


    export default {
        components: {
            PostForm,
            PostList
        },
        data() {
            return {
                posts: [],
                dialogVisible: false,
                isPostsLoading: false,
                page: 1,
                limit: 10,
                totalPages: 0,
                selectedSort: '',
                searchQuery: '',
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
            changePage(pageNumber) {
                this.page = pageNumber;
            },
            async fetchPosts() {
                try {
                    this.isPostsLoading = true
                    const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                        params: {
                            _page: this.page,
                            _limit: this.limit,
                        }
                    });
                    this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
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
            },
            sortedAndSearchedPosts () {
                return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
            },
        },
        watch: {
            page() {
                this.fetchPosts()
            }
        }
    };
</script>

<style>


    .app_btns {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin: 15px 0;
    }

    .page__wrapper {
        display: flex;
        align-items: center;
        margin: 15px 0;
    }
    .page {
        cursor: pointer;
        border: 1px solid #000;
        padding: 10px;
    }

    .current-page {
        border: 2px solid teal;
    }
</style>
