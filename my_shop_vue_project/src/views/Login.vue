<script>
import router from "@/router";

document.addEventListener('DOMContentLoaded', function() {
  let input_name = document.getElementById('name');
  let input_password = document.getElementById('password');
  const login_button = document.getElementById('login_button');

  login_button.addEventListener('click', function() {

    const requestOptions = {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({"email": input_name.value, "password": input_password.value})
    };
      console.log('attends je fetch là')
    fetch("http://localhost/authentication_token", requestOptions)
        .then(response => {
          if (response.status === 200) {
            console.log("Status Code:", response.status);
            fetch('http://localhost/api/users', {
              headers: {
                'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAyMTE1NTIsImV4cCI6MTcwMDIxNTE1Miwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6IjEyMzQ1NkAxMjM0NTYifQ.rpyRBKxL74bi5HNC7TekOQcR8C_MA6urL2twr43mM_Iqe5KT1XCvr_HNrnAQn49_TAqbqf52PINCuarZE-qi3-IYhtcyDTVyGlTnkGoM54e2mOzZbscw4PysB6bI59SCvSLd4-fwqW5YuDTrGS_k1Fh3by8t6O5XGfDqWucKhQorvKluMiJEfi5ZgA__NgHbRSBggFRKjimTHjv-lUP_iXsLoPW__MGMn-i2cgruWaWR58Urc0jAn8KHz5VHuZuxQNq2-Ms8AbfBc6NgND1g6TgwXsu6hmBrzweqsKaiTFcAcbYzmaYhGg99lCfJnjsz53p0W51CWUIb6LJKobRjtA'
              }
            })
                .then(response => response.json())
                .then(data => {
                  for (let i = 0; i < data['hydra:member'].length;i++){
                    if (data['hydra:member'][i]['email'] === input_name.value){
                      console.log(data['hydra:member'][i]['roles'][0])
                      if(data['hydra:member'][i]['roles'][0]==='ROLE_ADMIN'){
                        console.log('MISTER ADMIN')
                        router.push({ path: '/admin' });
                        break
                      }else{
                        console.log('DEAR CLIENT')
                        router.push({ path: '/' });
                        break
                    }
                    }
                  }
                })
          }
        })

    console.log(input_name.value);
    console.log(input_password.value);
  });
});

</script>

<template>
  <h1>LOG IN</h1>
  <section id = "login_stuff">
    <section id="login_info">
      <h3>Name</h3>
      <input id = 'name' type="text">
      <h3>Password</h3>
      <input id = 'password' type="password">
    </section>
    <button id="login_button">Log in</button>

    <p>Don't have an account?</p><router-link to="/register">Register here</router-link>
  </section>
</template>

<style>
body {
  display: flex;
  justify-content: center;
  margin: 0;
}

#login_info {
  margin-bottom: 20px;
}
</style>