<script lang="ts">
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import HelloWorld from '../components/HelloWorld.vue';

interface IPost {
  albumId: number,
  id: number,
  thumbnailUrl: string,
  title:string,
  url: string,
}

export default {
    name: 'Post',
    setup() {
        const post = ref<IPost>();
        const isLoading = ref(false);
        const route = useRoute();
        const id = Number(route.params.id);

        const fetchPost = (id: Number) => {
            isLoading.value = true;
            fetch("https://jsonplaceholder.typicode.com/albums/1/photos")
                .then(res => res.json())
                .then(res => {
                isLoading.value = false;
                post.value = res.filter((post: IPost) => post.id === id)[0];
            });
        };
        
        onMounted(() => fetchPost(id));

        return {
            post,
            isLoading,
        };
    },
    components: { HelloWorld }
}
</script>

<template>
    <router-link to="/" class="link">Voltar</router-link>
    <p v-if="isLoading" class="center">Loading...</p>
    <div v-else>
        <h1 class="center">Post {{ $route.params.id }}</h1>
        <img :src="post?.url" :alt="post?.title">
        <p class="center">{{ post?.title }}</p>
    </div>
</template>

<style scoped>
    div {
        display: flex;
        max-width: 600px;
        margin: 0 auto;
        flex-direction: column;
        justify-content: center;
    }
    .center {
        text-align: center;
    }
    .link {
        position: absolute;
        display: inline-block;
        text-decoration: none;
        border: 1px solid #000;
        border-radius: 4px; 
        color: #000;
        padding: 8px 16px;
        top: 20px;
        left: 20px;
        transition: .5s;
    }
    .link:hover {
        background-color: #000;
        color: #fff;
    }
</style>
