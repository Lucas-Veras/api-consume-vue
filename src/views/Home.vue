<script lang="ts">
import { onMounted, ref } from 'vue'

interface IPost {
  albumId: number,
  id: number,
  thumbnailUrl: string,
  title:string,
  url: string,
}

export default {
    setup() {
        const posts = ref<IPost[]>([]);
        const isLoading = ref(false);

        const fetchPosts = async () => {
            isLoading.value = true;
            fetch("https://jsonplaceholder.typicode.com/albums/1/photos")
              .then(res => res.json())
              .then(res => {
              posts.value = res;
              isLoading.value = false;
              })
        };
        onMounted(fetchPosts);
        return { 
          posts, 
          isLoading
        };
    },
}
</script>

<template>
  <h1 class="center">Posts</h1>
  <p v-if="isLoading" class="center">Loading...</p>
  <div v-else class="container">
    <div v-for="post in posts" :key="post.id" class="box">
      <img :src="post.thumbnailUrl" :alt="post.title">
      <p class="title">{{ post.title }}</p>
      <router-link :to="{name: 'Post' , params:{ id: post.id }}" class="link">Ver mais</router-link>
    </div>
  </div>
</template>

<style scoped>
  .center {
    text-align: center;
  }
  .link {
    width: 100%;
    text-decoration: none;
    border: 1px solid #000;
    border-radius: 4px; 
    color: #000;
    padding: 4px 0;
    transition: .5s;
  }
  .link:hover {
    background-color: #000;
    color: #fff;
  }
  .box {
    max-width: 150px;
    display: flex;
    flex-direction: column;
    text-align: center;
  }
  .box img {
    max-width: 150px;
  }
  .title {
    display: -webkit-box;
    -webkit-line-clamp: 1;
    overflow: hidden;
    -webkit-box-orient: vertical;
}
  .container {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 10px;
    margin: 0 auto;
  }
</style>