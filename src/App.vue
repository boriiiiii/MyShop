<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />
  </header>

  <main>
    <h2>Données de l'API:</h2>
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

fetch('http://localhost/api/categories', {
  headers: {
    'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE2OTk5NTA0MTgsImV4cCI6MTY5OTk1NDAxOCwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6ImJvcmlzLmRvdWFkeUBlcGl0ZWNoLmRpZ2l0YWwifQ.dIio2Ek2KO_TTlzN1_1kLx-Jbk8gRmvvMBoWphxic9PosLSU0e0DYTyanlDbcTWQK5XIxQSTvduG9-xahWRZV2m4Hs-BdsItmL-Pt7TOP4hiGvpB_ZN5AgPlIOgd9ThL7bubwm0p9mdIMiZEFD1jLlWnN_9dLh036pESaHufKaSCW_R_9Ug7FPzxuRxbiKdqaEQiHMOBwf_pgsIT6Ba3fTLSnGm0rBi67c5AFvC9HO78YhxAL5YtEaiMcIITgh4kLkptD5e8J5XssTwT70X9HNxrGX0yW3gbnPJAazE4wr6MxDulLtVTHYWCNmlCGLqrW2cMaj1u4vEgFAJTTA0__Q'
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
</script>

<style scoped>
/* Styles here */
</style>