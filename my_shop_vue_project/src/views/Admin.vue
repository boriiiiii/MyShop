<script setup>
import { ref } from 'vue';

let balise_data_content = ref(null);
let apiData = ref([]);

function handleProductClick() {
  console.log('product')
  getApiData('http://localhost/api/products');
}

function handleCategoriesClick() {
  console.log('category')
  getApiData('http://localhost/api/categories');
}

function handleUsersClick() {
  console.log('user')
  getApiData('http://localhost/api/users');
}

function getApiData(apiURL) {
  fetch(apiURL, {
    headers: {
      'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAwNjE2NDQsImV4cCI6MTcwMDA2NTI0NCwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6ImJvcmlzLmRvdWFkeUBlcGl0ZWNoLmRpZ2l0YWwifQ.sfwy3ms6Yqyt7I7o_Zn8IHhoL6H-4LY3jMvkU7Sga1alFLMLEOAptnzlaAb2kzFuXIGmfwoHfY2O8poc5mp2uVZrQpSztwqqZAKakLyR7KLcYCnOZB9avMpZ-3luSbuDtBRgZ-YcWkd7IkjhbvbFv42uEn5J7z8D-30wycFvwBFtU0Q46S-ilbj509J94s1iNpO1H5pIwBHZN-4o5WgRZXkHaCsFBDra_-eO9al-DeN8THA80D-t5K-LFTKbyz299rPhrLQ-7f4EkIR-OFA3JihJbEfJ2tmi9hp6V5jyweMdwSp3zKUIR6akfEp2UmWQ1vWQiqRqHGROUrKmMmk-UA'
    }
  })
      .then(response => response.json())
      .then(data => {
        apiData.value = data['hydra:member'];
        console.log(apiData.value);
      })
      .catch(error => console.error('Erreur:', error));
}
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="../assets/logo.svg" width="125" height="125" />
    <input type="text" size="70">
    <button>Logged</button>
  </header>
  <main>
    <ul>
      <a href="#" @click="handleProductClick">Product</a>
      <a href="#" @click="handleCategoriesClick">Categories</a>
      <a href="#" @click="handleUsersClick">Users</a>
    </ul>
    <div id="data_content">
      <p v-for="item in apiData" :key="item.name">{{ item.id }} {{ item.name }}</p>
    </div>
  </main>
</template>

<style>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

ul {
  display: flex;
  justify-content: space-between;
}

a {
  cursor: pointer;
}
</style>
