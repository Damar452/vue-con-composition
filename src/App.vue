<script setup>
import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';
import { ref, onMounted } from 'vue';

const posts = ref([]);
const postXPage = 10;
const start = ref(0);
const end = ref(postXPage);
const favorite = ref('');
const loading = ref(true);

const changeFavorite = (title) => {
  favorite.value = title;
}

const next = () => {
  start.value += postXPage;
  end.value += postXPage;
}

const previus = () => {
  start.value += - postXPage;
  end.value += - postXPage;
}

onMounted(async () => {
  try {
   const res = await fetch('https://jsonplaceholder.typicode.com/posts');
   posts.value = await res.json();
  } catch (error) {
    console.log(error)
  } finally {
    loading.value = false;
  }
});


</script>

<template>
  <LoadingSpinner v-if="loading" />
  <div class="container" v-else="!loading">
    <h1>APP</h1>
    <h2>Mis Post Favorito: {{ favorite }}</h2>

    <PaginatePost @next="next" @previus="previus" :start="start" :end="end" :total="posts.length" class="mb-2" />

    <BlogPost 
    v-for="post in posts.slice(start, end)" 
    :title="post.title" 
    :id="post.id" 
    :body="post.body"
    :key="post.id"
    @changeFavorite="changeFavorite"
    class="mb-2"
    ></BlogPost>

  </div>
</template>