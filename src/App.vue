<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
      <h2>Données de l'API:</h2>
      <pre>{{ apiData }}</pre>
  </main>
</template>

<script setup>
import HelloWorld from './components/HelloWorld.vue';

let apiData = null;
let loading = true;

fetch('http://localhost/api/categories', {
  headers: {
    'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE2OTk5MDA2MjcsImV4cCI6MTY5OTkwNDIyNywicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6ImJvcmlzLmRvdWFkeUBlcGl0ZWNoLmRpZ2l0YWwifQ.eMNNjg_Mkk1SBIr5KH7y9S4kU7MuBMnXAXBr4plNrvk-CXebrB0_dDgN9MmUcTRBASla-jyX_z91R_EasmDI0IIXhS0pvkyJjSzGMmKJDaHED2GW0hNMzPVzBkrd_d2smz_iq51dAv3LSzuAoUjNZct6q7j4YS_7WEJFmxxAVslw4uLpcBAYgOpSQombNHosF2xnbbbvV0m52y6aPQG18DGLXP0bcRBZ6G-qkY7z3AEN6JdE21M7ezpRaLFOmZzlnv0BHY_Q_bmyqE3HQjbfP-XthQPVKwKd8PK94fHlIoMeF1fT-D0_LfYWTaZV-Uz1QTbd3y1RCuWi4MVqTH47Zg'
  }
})
    .then(response => response.json())
    .then(data => {
      apiData = data;
    })
    .catch(error => console.error('Erreur:', error))
    .finally(() => {
      loading = false;
    });
</script>

<style scoped>
/* Styles here */
</style>
