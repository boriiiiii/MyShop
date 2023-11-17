  <script setup>
  import { ref } from 'vue';

  let balise_data_content = ref(null);
  let apiData = ref([]);
  let editingElement = ref(null);
  let addElement = ref([]);

  let newProductName = ref('');
  let newProductDescription = ref('');
  let newProductPrice = ref('');
  let newProductCategory = ref('');

  let newCategoryName = ref('');

  let newUserFullName = ref('');
  let newUserEmail = ref('');
  let newUserPassword = ref('');


  function handleAddButtonClick(elem){

    if (elem[0]['@type'] === 'Product') {
      console.log('Product Name:', newProductName.value);
      console.log('Product Description:', newProductDescription.value);
      console.log('Product Price:', newProductPrice.value);
      console.log('Product Category:', newProductCategory.value);

      const requestOptions = {
        method: "POST",
        headers: { "Content-Type": "application/json", 'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAyNDEyNDAsImV4cCI6MTcwMDI0NDg0MCwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6IjEyMzQ1NkAxMjM0NTYifQ.J80oA3NEi47powZpjYu6CuicBHt0d5g1lo_XUxK42HWuVRxn77SVgbKo65w5lIIG15ElBHez1R91RD05Mrc4tpvIgqh2Oc8sa-85_VSxRt4YqJINjSnKYnN686fppmr--N8QD8ZGhLOPEk_2bbioaCUKbJSdzrlZRtwY6KSabywzwVUh9oEoHeNtlzhkkOOOubc2fjmxUTUorF7_7FkR85LrLjaWQYGdhhuQtrapkfMOzchxXMWqAfod0_SW2TdCGVimIXFgD9fjT6Dh2qDWFWhInwGgh1uXdWUFJDV9R_BJRqO_AxIxdU4HsHMyFwYe-SfXA2R9A5BrRIwErVBosg' },
        body: JSON.stringify({
          "name": newProductName.value,
          "description": newProductDescription.value,
          "price": parseInt(newProductPrice.value),
          "categories": [
            newProductCategory.value
          ]})
      };

      fetch('http://localhost/api/products', requestOptions)
          .then(response => response.json())
          .then(data => {
            console.log(data);
          })
          .catch(error => {
            console.error('Error:', error);
          });

    } else if (elem[0]['@type'] === 'Category') {
      console.log('Category Name:', newCategoryName.value);

      const requestOptions = {
        method: "POST",
        headers: { "Content-Type": "application/json", 'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAyNDEyNDAsImV4cCI6MTcwMDI0NDg0MCwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6IjEyMzQ1NkAxMjM0NTYifQ.J80oA3NEi47powZpjYu6CuicBHt0d5g1lo_XUxK42HWuVRxn77SVgbKo65w5lIIG15ElBHez1R91RD05Mrc4tpvIgqh2Oc8sa-85_VSxRt4YqJINjSnKYnN686fppmr--N8QD8ZGhLOPEk_2bbioaCUKbJSdzrlZRtwY6KSabywzwVUh9oEoHeNtlzhkkOOOubc2fjmxUTUorF7_7FkR85LrLjaWQYGdhhuQtrapkfMOzchxXMWqAfod0_SW2TdCGVimIXFgD9fjT6Dh2qDWFWhInwGgh1uXdWUFJDV9R_BJRqO_AxIxdU4HsHMyFwYe-SfXA2R9A5BrRIwErVBosg'},
        body: JSON.stringify({
          "name": newCategoryName.value
        })
      };

      fetch('http://localhost/api/categories', requestOptions)
          .then(response => response.json())
          .then(data => {
            console.log(data);
          })
          .catch(error => {
            console.error('Error:', error);
          });

    } else if (elem[0]['@type'] === 'User') {
      console.log('User Full Name:', newUserFullName.value);
      console.log('User Email:', newUserEmail.value);
      console.log('User Role:', newUserPassword.value);

      const requestOptions = {
        method: "POST",
        headers: { "Content-Type": "application/json", 'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAyNDEyNDAsImV4cCI6MTcwMDI0NDg0MCwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6IjEyMzQ1NkAxMjM0NTYifQ.J80oA3NEi47powZpjYu6CuicBHt0d5g1lo_XUxK42HWuVRxn77SVgbKo65w5lIIG15ElBHez1R91RD05Mrc4tpvIgqh2Oc8sa-85_VSxRt4YqJINjSnKYnN686fppmr--N8QD8ZGhLOPEk_2bbioaCUKbJSdzrlZRtwY6KSabywzwVUh9oEoHeNtlzhkkOOOubc2fjmxUTUorF7_7FkR85LrLjaWQYGdhhuQtrapkfMOzchxXMWqAfod0_SW2TdCGVimIXFgD9fjT6Dh2qDWFWhInwGgh1uXdWUFJDV9R_BJRqO_AxIxdU4HsHMyFwYe-SfXA2R9A5BrRIwErVBosg'},
        body: JSON.stringify({
          "email": newUserEmail.value,
          "password": newUserPassword.value,
          "fullName": newUserFullName.value})
      };

      fetch('http://localhost/api/users', requestOptions)
          .then(response => response.json())
          .then(data => {
            console.log(data);
          })
          .catch(error => {
            console.error('Error:', error);
          });

    }



    addElement.value = null;
  }
  function handleAddClick(data) {
      addElement.value = data;
      console.log(addElement.value[0]['@type'])
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
        console.log(editingElement.value.name, editingElement.value.description,editingElement.value.price, editingElement.value.categories[0])
        requestBody = {
          "name": editingElement.value.name,
          "description": editingElement.value.description,
          "price": parseInt(editingElement.value.price),
          "categories": [
            editingElement.value.categories[0]
          ]
        };
      } else if (editingElement.value['@type'] === 'Category') {
        apiUrl = "http://localhost/api/categories/" + editingElement.value.id;
        console.log(editingElement.value.name, editingElement.value.products)
        requestBody = {
          "name": editingElement.value.name,
          "products": [
              editingElement.value.products[0]
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
          "Authorization": "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAyNDEyNDAsImV4cCI6MTcwMDI0NDg0MCwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6IjEyMzQ1NkAxMjM0NTYifQ.J80oA3NEi47powZpjYu6CuicBHt0d5g1lo_XUxK42HWuVRxn77SVgbKo65w5lIIG15ElBHez1R91RD05Mrc4tpvIgqh2Oc8sa-85_VSxRt4YqJINjSnKYnN686fppmr--N8QD8ZGhLOPEk_2bbioaCUKbJSdzrlZRtwY6KSabywzwVUh9oEoHeNtlzhkkOOOubc2fjmxUTUorF7_7FkR85LrLjaWQYGdhhuQtrapkfMOzchxXMWqAfod0_SW2TdCGVimIXFgD9fjT6Dh2qDWFWhInwGgh1uXdWUFJDV9R_BJRqO_AxIxdU4HsHMyFwYe-SfXA2R9A5BrRIwErVBosg"},
        body: JSON.stringify(requestBody)
      };

      fetch(apiUrl, requestOptions)
          .then(response => response.json())
          .then(data => {
            console.log(data);
          })
          .finally(() => {
            editingElement.value = null;
          });
    }
  }

  function handleDeleteClick(elem) {
    console.log('Delete');
    const requestOptions = {
      method: "DELETE",
      headers: { "Authorization": "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAyNDEyNDAsImV4cCI6MTcwMDI0NDg0MCwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6IjEyMzQ1NkAxMjM0NTYifQ.J80oA3NEi47powZpjYu6CuicBHt0d5g1lo_XUxK42HWuVRxn77SVgbKo65w5lIIG15ElBHez1R91RD05Mrc4tpvIgqh2Oc8sa-85_VSxRt4YqJINjSnKYnN686fppmr--N8QD8ZGhLOPEk_2bbioaCUKbJSdzrlZRtwY6KSabywzwVUh9oEoHeNtlzhkkOOOubc2fjmxUTUorF7_7FkR85LrLjaWQYGdhhuQtrapkfMOzchxXMWqAfod0_SW2TdCGVimIXFgD9fjT6Dh2qDWFWhInwGgh1uXdWUFJDV9R_BJRqO_AxIxdU4HsHMyFwYe-SfXA2R9A5BrRIwErVBosg"}
    };
    if (elem['@type'] === "category"){
      elem['@type'] = "categorie"
    }
    fetch("http://localhost/api/"+ elem['@type'].toLowerCase()+ "s" +"/"+ elem.id, requestOptions)

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
        'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAyNDEyNDAsImV4cCI6MTcwMDI0NDg0MCwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6IjEyMzQ1NkAxMjM0NTYifQ.J80oA3NEi47powZpjYu6CuicBHt0d5g1lo_XUxK42HWuVRxn77SVgbKo65w5lIIG15ElBHez1R91RD05Mrc4tpvIgqh2Oc8sa-85_VSxRt4YqJINjSnKYnN686fppmr--N8QD8ZGhLOPEk_2bbioaCUKbJSdzrlZRtwY6KSabywzwVUh9oEoHeNtlzhkkOOOubc2fjmxUTUorF7_7FkR85LrLjaWQYGdhhuQtrapkfMOzchxXMWqAfod0_SW2TdCGVimIXFgD9fjT6Dh2qDWFWhInwGgh1uXdWUFJDV9R_BJRqO_AxIxdU4HsHMyFwYe-SfXA2R9A5BrRIwErVBosg'
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
        <button id="add_button" v-if="apiData.length > 0" @click="handleAddClick(apiData)">Add</button>
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
        <div v-if="editingElement">
          <div id="edit_&_add_content">

            <input v-if="editingElement['@type'] === 'Product' || editingElement['@type'] === 'Category'" v-model="editingElement['@id']" />
            <input v-if="editingElement['@type'] === 'Product' || editingElement['@type'] === 'Category'" v-model="editingElement['@type']" />
            <input v-if="editingElement['@type'] === 'Product' || editingElement['@type'] === 'Category'" v-model="editingElement.id" />

            <input v-if="editingElement['@type'] === 'Product' || editingElement['@type'] === 'Category'" v-model="editingElement.name" />
            <input v-if="editingElement['@type'] === 'User'" v-model="editingElement.fullName" />

            <input v-if="editingElement['@type'] === 'Category'" v-model="editingElement.products" />
            <input v-if="editingElement['@type'] === 'Product'" v-model="editingElement.categories" />

            <input v-if="editingElement['@type'] === 'User'" v-model="editingElement.email" />
            <input v-if="editingElement['@type'] === 'Product'" v-model="editingElement.price" />

            <button @click="handleSaveClick()">Save</button>
          </div>
      </div>
        <div v-if="addElement && addElement.length > 0">
          <div id="add_content">
            <div class="add_content" v-if="addElement[0]['@type'] === 'Product'">

              <input id="add_input_product_name" v-model="newProductName" placeholder="Name">
              <input id="add_input_product_description" v-model="newProductDescription" placeholder="Description">
              <input id="add_input_product_price" v-model="newProductPrice" placeholder="Price">
              <input id="add_input_product_category" v-model="newProductCategory" placeholder="Categories">

              <button @click="handleAddButtonClick(addElement)" >ADD NEW</button>
            </div>
            <div class="add_content" v-if="addElement[0]['@type'] === 'Category'">

              <input id="add_input_category_name" v-model="newCategoryName" placeholder="Name">

              <button @click="handleAddButtonClick(addElement)" >ADD NEW</button>
            </div>
            <div class="add_content" v-if="addElement[0]['@type'] === 'User'">

              <input id="add_input_user_fullname" v-model="newUserFullName" placeholder="Full Name">
              <input id="add_input_user_email" v-model="newUserEmail" placeholder="Email">
              <input id="add_input_user_role" v-model="newUserPassword" placeholder="Password">

              <button @click="handleAddButtonClick(addElement)" >ADD NEW</button>
            </div>
          </div>
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


  </style>
