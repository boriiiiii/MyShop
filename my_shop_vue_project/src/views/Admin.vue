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
      'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAwNjU4NjIsImV4cCI6MTcwMDA2OTQ2Miwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6ImJvcmlzLmRvdWFkeUBlcGl0ZWNoLmRpZ2l0YWwifQ.Zi1aDhuftUEJakKG-aFyoeRRZHaiIJI_IsXqh0w9uCS4kbiR1a1Md5ESQoer59wC75rBAUo7R0flpMU-sofRMACdzZsUJQSf1klDj6cC4BBrQknYRlXKFHVaxJIEZsgVuy7UKZ3qdq4A9fAiKSJIK1TbLKZMuJnf6JiYOcnd48yJ7BW1eZNjtMER8ADEaRR1UxnRsZp_WBrUCWrdvcw0SX20AywixA-jy7KVJEaukOcVKlRPZv-fTLK3Ku-sku1FqDaQ0xT0qao9y4VebGEtKi425A-dgXYVWN8lth1FvIwuEu83a_mJ_BZv8AKafujUv7DcZ22UmO4bOwvhQPiNzA'
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
      <p v-for="elem in apiData" :key="elem.name">
        <span v-if="elem['@type'] === 'Product'">
          {{ elem['@id'] }} {{ elem['@type'] }} {{ elem.id }} {{ elem.name }} {{ elem.description }} {{ elem.price }} {{ elem.categories }}
        </span>
        <span v-if="elem['@type'] === 'Category'">
          {{ elem['@id'] }} {{ elem['@type'] }} {{ elem.id }} {{ elem.name }} {{ elem.products }}
        </span>
        <span v-if="elem['@type'] === 'User'">
          {{ elem['@id'] }} {{ elem['@type'] }} {{ elem.id }} {{ elem.email }} {{ elem.fullName }} {{ elem.roles }}
        </span>
      </p>
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
