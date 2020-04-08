<template>
    <div class="flex flex-col items-center">
        <dev class="relative mb-8">
            <div class="w-100 h-64 overflow-hidden z-10">
                <img src="https://previews.123rf.com/images/solerf/solerf1311/solerf131100130/23650708-green-planet-in-your-heart-hands-usa-environment-concept.jpg" alt="" class="object-cover w-full">
            </div>
            <div class="absolute flex items-center buttom-0 left-0 -mb-8 ml-12 z-20">
                <div class="w-32">
                    <img src="https://cdn.pixabay.com/photo/2014/07/09/10/04/man-388104_960_720.jpg" alt="profile image for user" class="w-32 h-32 border-4 border-gray-200 object-cover rounded-full shadow-lg">
                </div>
                <p class="text-2xl text-gray-100 ml-4 ">{{ user.data.attributes.name }}</p>
            </div>
            <div class="absolute flex items-center buttom-0 right-0 mb-4 mr-12 z-20">
                <button class="py-1 px-3 bg-red-400 rounded">Add Friend</button>
            </div>
        </dev>

        <p v-if="postloading">loading posts...</p>
        <Post v-else v-for="post in posts.data" :key="post.data.post_id" :post="post"/>
        <p v-if=" ! postloading && posts.data.length < 1"></p>

    </div>
</template>

<script>
    import Post from '../../components/Post';
    import { mapGetters } from 'vuex';

    export default {
        name: "Show",

        components: {
            Post
        },

        data:() => {
            return {
                posts:null,
                postLoadiing:true,
            }
        },
        mounted() {

            this.$store.dispatch('fetchUser', this.$route.params.userId);

            axios.get('/api/users/' + this.$route.params.userId + '/posts')
                .then(res => {
                    this.posts = res.data;
                })
                .catch(error => {
                    console.log('unable to fetch posts');

                })
                .finally(() => {
                    this.postLoading = false;
                });
        },

        computed: {
            ...mapGetters({
                user: 'user'
            })
        }
    }
</script>

<style scoped>

</style>