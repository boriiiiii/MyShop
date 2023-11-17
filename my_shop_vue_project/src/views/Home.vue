<script setup>
import router from "@/router";
import {computed} from "vue";

let apiData = null;
let loading = true;

function redirectToLogin() {
  router.push({path : '/login'})
}

function getApiData(apiURL){
  fetch(apiURL, {
    headers: {
      'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAyMTcwNTAsImV4cCI6MTcwMDIyMDY1MCwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6IjEyMzQ1NkAxMjM0NTYifQ.TjC9VAk8xlMx97iHeJF7dKxFiBz_Vt8ptbtNQipP3uIpW76eh2T4FXaLgaNg39pTj_BIam4k-r4S6Nbagl6JhBsnMAh9ivGH_BpSaRKLs0vXy_EYTbBIJB5-9lwX2CwfIrMhohTJ1ZXkmlpJ7ZXX6H3v2wpE9H1KXuZ7DFTDnHVYZXjd9ZDB3WPdw34h7egGwMHqgo2apiXRqZeO4zKIrke_fjdpz_7fLdkh9ZXYwznwv84okh4Ve6ZT6NwWPVJc39f8UOV1g3XDZ4IP0O9kIFZC5s7PpixptIAzXkrvFOnYQBtSBwqUEf1iJABP-FaBdL3eeQ3qPpat-9y1GDXefA'
    }
  })
      .then(response => response.json())
      .then(data => {
        apiData = data;
        console.log(apiData)
      })
      .catch(error => console.error('Erreur:', error))
      .finally(() => {
        loading = false;
      });
}
getApiData('http://localhost/api/products')
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="../assets/logo.svg" width="125" height="125" />
    <input type="text" size="70">
    <button @click="redirectToLogin">Login</button>
  </header>

  <main>
    <div class="product" v-if="apiData" v-for="product in apiData['hydra:member']" :key="product['@id']" >
      <div class="none-image"></div>

      <div class="info-product">
        <div class="name-product">{{ product['name'] }} </div>
        <div class="category-product">{{ product['categories'] }}</div>
        <div class="price-product">{{ product['price'] }} €</div>
        <div class="id-product">{{ product['id'] }}</div>
      </div>
    </div>
    <div v-else>Loading</div>
  </main>
</template>

<style>
header{
  display: flex;
  justify-content: space-between;
  align-items: center;
}

main{
  display: flex;
  justify-content: space-evenly;
}

.product{
  background-color: white;
  height: 185px;
  width: 155px;
  padding: 5px;
  border-radius: 5%;
}


.none-image{
  background-color: grey;
  width: 100%;
  height: 50%;
  border-radius: 5%;
}


.name-product{
  font-weight: bold;
  color: #0a0a0a;
}

.category-product{
  color: #0a0a0a;
}

.price-product{
  color: #0a0a0a;
  font-size: 0.8em;
}
.id-product{
  color: #0a0a0a;
  font-size: 0.8em;
}

</style>