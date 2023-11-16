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
      'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAxMzA0ODQsImV4cCI6MTcwMDEzNDA4NCwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6IjEyMzQ1NkAxMjM0NTYifQ.XKTnrBkSKLisESOT-3md8VKf_N_kiFxuJtCsj2O4MOU6kMNOu_tLkOaEwuVvINfXswcIw95jPHxlRq7jLGLZA2tzaP0HHKrfJYTTNbyw6QLgBLyHyaBBTZ9Q9R9Raqnx4VCcdSinYqg71Npo4XagW_siug7P17fod9uuxFA3pgmOkQHskIkMOd-nN7I3Wsq9qJeiihOII6NhHvTc0PeqI-1CeV9_GHyzPwoa0VmaGf_pY5nj4V9dHc0X2QO5Y2sk8sUiCEfpXzaxOJRk3g-hgXxjO7F3UBClOJCj8RKjHzDvMgqdfcdMmKZJrFq35h7vshImZEAAX5ixbP_A5XNSJw'
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
      <table v-if="apiData.length > 0">
        <thead>
        <th>ID</th>
        <th>Type</th>
        <th>D_ID</th>
        <th>Name</th>
        <th v-if="apiData.length > 0 && apiData[0]['@type'] === 'Product'">Category(ies)</th>
        <th v-else-if="apiData.length > 0 && apiData[0]['@type'] === 'Category'">Product(s)</th>
        <th v-else-if="apiData.length > 0 && apiData[0]['@type'] === 'User'">Role</th>
        <th v-if="apiData.length > 0 && apiData[0]['@type'] === 'Product'">Price</th>
        <th v-else-if="apiData.length > 0 && apiData[0]['@type'] === 'User'">E-mail</th>
        <th>Action</th>
        </thead>
        <tbody>
        <tr v-for="elem in apiData" :key="elem['@id']">
          <td>{{ elem['@id'] }}</td>
          <td>{{ elem['@type'] }}</td>
          <td>{{ elem.id }}</td>

          <td v-if="elem['@type'] === 'Product'">{{ elem.name }}</td>
          <td v-else-if="elem['@type'] === 'Category'">{{ elem.name }}</td>
          <td v-else-if="elem['@type'] === 'User'">{{ elem.fullName }}</td>

          <td v-if="elem && elem['@type'] === 'Product'">{{ elem.categories }}</td>
          <td v-else-if="elem && elem['@type'] === 'Category'">{{ elem.products }}</td>
          <td v-else-if="elem && elem['@type'] === 'User'">{{ elem.roles[0] }}</td>

          <td v-if="elem && elem['@type'] === 'Product'">{{ elem.price }}</td>
          <td v-else-if="elem && elem['@type'] === 'User'">{{ elem.email }}</td>

          <td>Edit Delete</td>
        </tr>
        </tbody>
      </table>
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

td,table {

  border: 2px solid white;

}

#data_content{
  display: flex;
  justify-content: center;
}

</style>
