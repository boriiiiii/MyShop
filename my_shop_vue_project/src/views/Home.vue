<template>
  <header>
    <img alt="Vue logo" class="logo" src="../assets/logo.svg" width="125" height="125" />
    <input type="text" size="70">
    <button @click="redirectToLogin">Login</button>
  </header>

  <main>
    <h2>Données de l'API :</h2>
    <div v-if="apiData && apiData['hydra:member']">
      <div v-for="category in apiData['hydra:member']" :key="category['@id']">
        <h3>Category {{ category['id'] }}</h3>
        <p>ID: {{ category['id'] }}</p>
        <p>Type: {{ category['@type'] }}</p>
        <p>Name: {{ category['name'] }}</p>
        <p>Product's List: {{ category['products'] }}</p>
      </div>
    </div>
  </main>
</template>

<script setup>
let apiData = null;
let loading = true;

function getApiData(apiURL){
  fetch(apiURL, {
    headers: {
      'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE2OTk5NzIyMjMsImV4cCI6MTY5OTk3NTgyMywicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6ImJvcmlzLmRvdWFkeUBlcGl0ZWNoLmRpZ2l0YWwifQ.1AgtOtGZOX5EewUzu74wHX5b4f_0Nrkzx_1aE_w31A61-qp8hzLVAxm75FKPOxZHLoNyZ1QSmRssfhHFPCtaWpMJcCAjYz2xm_7ELb0qPib1G0fz4uTyr2eFmMoAYvNvIF3m1zYi2mH2zCt46lgKpwflmxD691lx0xZoMoyO0zf8QjIJ9hbmoCWHaHxFBncwv3B56LsX4538XM9ZCl6LJhuze3lshog6-JTgvI3OPUlUFo11FsUMjuBFy8QRzvMwN3RK_2IO2OHCtcT8Xm36lE-IVoU-bHUpI-_N0wfvXOHeJjteLrTJ6_noxmSC8ZIYep0eW7vQW26l95FRjIjHkA'
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
function redirectToLogin() {
  // Assuming you want to redirect to http://localhost:5173/login
  window.location.href = 'http://localhost:5173/login';
}

</script>

<style>
header{
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>