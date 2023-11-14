<script setup>
import { ref } from 'vue';

let balise_data_content = ref(null);
let apiData = ref([]);

function handleProductClick() {
  getApiData('http://localhost/api/products');
}

function handleCategoriesClick() {
  getApiData('http://localhost/api/categories');
}

function handleUsersClick() {
  getApiData('http://localhost/api/users');
}

function getApiData(apiURL) {
  fetch(apiURL, {
    headers: {
      'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE2OTk5ODExMjgsImV4cCI6MTY5OTk4NDcyOCwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6ImJvcmlzLmRvdWFkeUBlcGl0ZWNoLmRpZ2l0YWwifQ.HylbcA2dHkOpEzBtk8j2DRx4xg5EFi_YS6Jq4Xi4oZBUAiDbA8UPy90FJ2Fieq27_zlPN_kgPrgAwNJGFXcDtDuZNfWo2H9zVvHEEbmwLzzND-EFJLJaxRbfh0hd1Cb4awQJTEM0beoXRT41Yngpwr3gKncaWDBpdztcpndwKfCyn4H-p9uB52S51eXx7D3UnHUWMAIGzQAq9e1ttVyPQfBi0vJN4Q-hPd0We_OTn2qKoQkiZNI1f1NrIFQfcSxT6A3T9kgE3igpGjwnAlLT63ga0V2tjrP70Od6A8wKQ3jr0homgxmXQytNFMGDPJbZJF7J86nopitKsaOiS1OlgQ'
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
      <p v-for="item in apiData" :key="item.name">{{ item.name }}</p>
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
