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
      'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAyMjY5OTQsImV4cCI6MTcwMDIzMDU5NCwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6IjEyMzQ1NkAxMjM0NTYifQ.tWkKfsSz3V7VxWWoLrnXxsuBGXnXqT7-dCv7SGoBL2qD07q-tnR1Dj0hZsg1k6_aeFzaRZO06hQYXXH9rVfcgZjxUUnu_VpSJDBObgc1T4XpMwMNlQWvdTHUkseyiikNw5pov9FliFttAte0jjgwFlGzS5Tgi3NQUy0VjS1hdZ4risamPSbi8l58h1qGmETZbscAyqb4biJV8L53VcZrYs0zjVq1tqiZsdPPWwf99KRb9FcRgtl4gnvIZJp5VlrjY7Fku9GzXKTXgH7GuMfop_4sgajvePNF9YQ3hBIGYGrjlE8JRHzARxDA4FM_-jHcntQVFHd5lyG-Q6A8WHmsSA'
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
      <div  class = "product" v-if="apiData" v-for="product in apiData['hydra:member']" :key="product['@id']" >

        <div class="none-image"></div>

        <div class="info-product">
          <div class="name-product">{{ product['name'] }} </div>
          <div class="price-product">{{ product['price'] }} €</div>
          <div class="id-product">{{ product['id'] }}</div>
        </div>

      </div>
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