<template>
    <div>
        <h1>Home Page</h1>
        <div class="posts">
            <h3>Latest from our Blog</h3>
            <div class="post" v-for="post in posts" :key="post.id">
                <h4>{{post.post_title}}</h4>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios";

export default {
    head: {
        title: "Home"
    },

    fetch({ store }) {
        return axios
            .get("http://localhost/wp_vue/wp-json/markers/v1/post")
            .then(res => {
                store.commit("frontPagePosts", res.data);
            })
            .catch(error => {
                console.log(error);
            });
    },

    computed: {
        posts() {
            return this.$store.state.posts;
        }
    }
};
</script>

