<template>
  <main>
    <h2>Пост</h2>
    <div>
      <p>Title</p>
      <input v-model="data.title">
    </div>
    <div>
      <p>Text</p>
      <input v-model="data.text">
    </div>
    
    <button @click="save">Сохранить</button>
    <button @click="remove">Удалить</button>

  </main>
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios';
import router from '@/router';
import { useRoute } from 'vue-router'

const data = ref([]);

const blog_id = useRoute().params.id

async function save() {
  let data1 = {
    title: data.value.title,
    text: data.value.text,
    blog_id: blog_id,
    access_token: localStorage.getItem('access_token')
  }
  await axios.post('http://127.0.0.1:5000/edit_blog', data1);
};
async function remove() {
  let data1 = {
    blog_id: blog_id,
    access_token: localStorage.getItem('access_token')
  }
  await axios.post('http://127.0.0.1:5000/delete_blog', data1);
  router.push('/')
}

</script>