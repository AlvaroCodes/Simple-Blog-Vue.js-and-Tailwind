<script setup>
import { ref } from 'vue';
import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';

const postXpage = 10

const posts = ref([]);
const inicio = ref(0)
const fin = ref(postXpage)
const loading = ref(true)

const favorito = ref("")
const cambiarFavorito = (post) => {
   favorito.value = post
}

const next = () => {
  inicio.value = inicio.value + postXpage
  fin.value = fin.value + postXpage
}

const previus = () => {
  inicio.value = inicio.value - postXpage
  fin.value = fin.value - postXpage
}

fetch('https://jsonplaceholder.typicode.com/posts')
      .then(response => response.json())
      .then(json => posts.value = json)
      .catch((e) => console.log(e))
      .finally(() => {
        // Para mostrar el loading, en pro eliminar
        setTimeout(() => {
          loading.value = false
        }, 1000);
      })
</script>

<template>
    <LoadingSpinner 
    v-if="loading"/>
    <section 
    class="p-10"
    v-else>
      <h1
      class="text-3xl font-bold pr-1 text-slate-800"
      >Blog</h1>
      <h2
      class="text-xl font-bold pr-1 text-slate-800"
      >Mi post favorito: {{favorito}}</h2>
      <PaginatePost 
      @next="next" @previus="previus"
      :inicio="inicio" :fin="fin"
      :postLength="posts.length"
      />
      <BlogPost
      class="my-5"
      v-for="post in posts.slice(inicio, fin)"
        :key="post.id"
        :title="post.title"
        :id="post.id"
        :body="post.body"
        @cambiarFavorito="cambiarFavorito"
      />
    </section>
   
</template>


