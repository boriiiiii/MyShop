<script setup>
import { ref } from 'vue';

let balise_data_content = ref(null);
let apiData = ref([]);
let editingElement = ref(null);
function handleAddClick(){
  console.log('CLICKER BOUTTON !')
}

function handleEditClick(elem) {
  console.log('Edit', elem.id);
  editingElement.value = elem;
}
function handleSaveClick() {
  if (editingElement.value) {
    let apiUrl;
    let requestBody = {};

    if (editingElement.value['@type'] === 'Product') {
      apiUrl = "http://localhost/api/products/" + editingElement.value.id;
      requestBody = {
        "name": editingElement.value.name,
        "description": editingElement.value.description,
        "price": editingElement.value.price,
        "categories": [
          editingElement.value.categories
        ]
      };
    } else if (editingElement.value['@type'] === 'Category') {
      apiUrl = "http://localhost/api/categories/" + editingElement.value.id;
      requestBody = {
        "name": editingElement.value.name,
        "products": [
            editingElement.value.name
        ]
      };
    } else if (editingElement.value['@type'] === 'User') {
      apiUrl = "http://localhost/api/users/" + editingElement.value.id;
      requestBody = {
        "email": editingElement.value.email,
        "fullName": editingElement.value.fullName
      };
    }

    const requestOptions = {
      method: "PUT",
      headers: {
        "Content-Type": "application/json",
        "Authorization": "Bearer "},
      body: JSON.stringify(requestBody)
    };

    fetch(apiUrl, requestOptions)
        .then(response => response.json())
        .then(data => {
          console.log(data);
        })
        .finally(() => {
          editingElement.value = null;

          // Perform additional asynchronous action here if needed
        });
  }


    fetch("http://localhost/api/" + LowerCase(editingElement.value['@type'])+ "s" + "/" + editingElement.value.id, requestOptions)
        .then(response => response.json())
        .then(data => {
          console.log(data);
        })
        .finally(() => {
          editingElement.value = null;
        });
}

function handleDeleteClick(elem) {
  console.log('Delete');
  const requestOptions = {
    method: "DELETE",
    headers: { "Authorization": "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAxNTI0NTEsImV4cCI6MTcwMDE1NjA1MSwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6IjEyMzQ1NkAxMjM0NTYifQ.g9_jK-6Q606Q9IszznntLvZgMxsWgj0qNNvPwVzRdoPilgH90viB8CfSxTNWUG_CZ6Dwn-yt10-Fy-SLgSFusvu4NXNb3gIVGG3v5DxJnNgCb65ytk8H34wf4dvSqFZYj-s3sM4f3lsy5w-gX4tpJAa5RIJuZOk1UTp3gczEg2PxR6up2iSN2uNtSK1sBn_xEoTY6L5AFO1Gh1-b8-KuKy0kSVuICVRZXoUeBcxNslPtueuXhnx33D1zDInrdbjtSD0DE7iq0iaJFCOcEFc53V1c79ZlfIaXyid0bSk_PnlgeoMV1xqHZYgir_bO0vNTVIDiHza6Hd1MllAdbGB9vg"}
  };
  if (elem['@type'] === "category"){
    elem['@type'] = "categorie"
  }
  fetch("http://localhost/api/"+ elem['@type'].toLowerCase()+ "s" +"/"+ elem.id, requestOptions)
      .then(response => response.json())
      .then(data => {
        console.log(data)
      });
}
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
      'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAxNTI0NTEsImV4cCI6MTcwMDE1NjA1MSwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6IjEyMzQ1NkAxMjM0NTYifQ.g9_jK-6Q606Q9IszznntLvZgMxsWgj0qNNvPwVzRdoPilgH90viB8CfSxTNWUG_CZ6Dwn-yt10-Fy-SLgSFusvu4NXNb3gIVGG3v5DxJnNgCb65ytk8H34wf4dvSqFZYj-s3sM4f3lsy5w-gX4tpJAa5RIJuZOk1UTp3gczEg2PxR6up2iSN2uNtSK1sBn_xEoTY6L5AFO1Gh1-b8-KuKy0kSVuICVRZXoUeBcxNslPtueuXhnx33D1zDInrdbjtSD0DE7iq0iaJFCOcEFc53V1c79ZlfIaXyid0bSk_PnlgeoMV1xqHZYgir_bO0vNTVIDiHza6Hd1MllAdbGB9vg'
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
      <button id="add_button" v-if="apiData.length > 0" @click="handleAddClick">Add</button>
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

          <td>
            <a href="#" @click="handleEditClick(elem)">Edit </a>
            <a href="#" @click="handleDeleteClick(elem)">Delete</a>
          </td>
        </tr>
        </tbody>
      </table>
    </div>
    <div v-if="editingElement">
      <div id="edit_&_add_content">

        <input v-model="editingElement['@id']" />
        <input v-model="editingElement['@type']" />
        <input v-model="editingElement.id" />

        <input v-if="editingElement['@type'] === 'Product' || editingElement['@type'] === 'Category'" v-model="editingElement.name" />

        <input v-if="editingElement['@type'] === 'User'" v-model="editingElement.fullName" />

        <input v-if="editingElement['@type'] === 'Category'" v-model="editingElement.products" />
        <input v-if="editingElement['@type'] === 'User'" v-model="editingElement.roles" />
        <input v-if="editingElement['@type'] === 'Product'" v-model="editingElement.categories" />

        <input v-if="editingElement['@type'] === 'User'" v-model="editingElement.email" />
        <input v-if="editingElement['@type'] === 'Product'" v-model="editingElement.price" />

        <button @click="handleSaveClick()">Save</button>
      </div>
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

table {
  border: 2px solid white;
}

td {
  border: 2px solid white;
  text-align: center;
}

#data_content{
  display: flex;
  justify-content: center;
  margin-top: 10%;
  flex-direction: column;
}

#add_button {
  align-self: flex-end;
  margin-bottom: 2%;
}

#edit_&_add_content{
  background-color: whitesmoke;
  color: red;
}
</style>
