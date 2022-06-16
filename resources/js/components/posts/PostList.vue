<template>
    <div>
        <!-- loader per evitare scritta v-else a lungo anche se ci sono post -->
        <Loader v-if="isLoading"/>
        <ul v-if="posts.lenght">
            <li :key="post.id" v-for="post in posts">
                {{post.title}}
            </li>
        </ul>
        <p v-else>Non ci sono Post</p>
    </div>
</template>

<script>
    import axios from 'axios';
    import Loader from '../Loader.vue'
    export default{
        name: "PostList",
        components: {
            Loader
        },
        data(){
            return{
                posts: [],
                isLoading: true
            }
        },
        methods: {
            getPosts(){
                axios.get("http://127.0.0.1:8000/api/posts")
                .then( (res) => {
                    //console.log( res.data );
                    this.posts = res.data.posts;
                } ).then( ()=>{
                    console.log('terminato il caricamento dei Post');
                    this.isLoading = false;
                } )
            }
        },
        mounted(){
            this.getPosts();
        }
    }
</script>

<style scoped>

</style>
