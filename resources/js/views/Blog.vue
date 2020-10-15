<template>
    <div>
        <spin v-if="loading"></spin>
        <div style="display:flex; flex-wrap: wrap;" v-else>
            <post
                v-for="post in posts"
                :title="post.title"
                :body="post.body"
                :date="post.created_at"
            />
        </div>
    </div>
</template>

<script>
    import Spin from "../components/Spin";
    import axios from 'axios';
    import Post from "../components/Blog/Post";
    export default {
        components: {
            Spin,
            Post
        },
        data: () => ({
            loading: true,
            posts: []
        }),
        mounted() {
            this.loadPosts();
        },
        methods: {
            loadPosts() {
                axios.get('/api/posts')
                .then(res => {
                    this.posts = res.data;
                    setTimeout(() => {
                        this.loading = false;
                    }, 500)
                })
            }
        }
    }
</script>

<style scoped>
    .uk-card {
        width: 40%;
        margin-right: 20px;
        margin-bottom: 20px;
    }

    .uk-card:last-child {
        margin-right: 0;
    }
</style>
