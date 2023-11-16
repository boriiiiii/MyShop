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
                'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAxNTI0NTEsImV4cCI6MTcwMDE1NjA1MSwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6IjEyMzQ1NkAxMjM0NTYifQ.g9_jK-6Q606Q9IszznntLvZgMxsWgj0qNNvPwVzRdoPilgH90viB8CfSxTNWUG_CZ6Dwn-yt10-Fy-SLgSFusvu4NXNb3gIVGG3v5DxJnNgCb65ytk8H34wf4dvSqFZYj-s3sM4f3lsy5w-gX4tpJAa5RIJuZOk1UTp3gczEg2PxR6up2iSN2uNtSK1sBn_xEoTY6L5AFO1Gh1-b8-KuKy0kSVuICVRZXoUeBcxNslPtueuXhnx33D1zDInrdbjtSD0DE7iq0iaJFCOcEFc53V1c79ZlfIaXyid0bSk_PnlgeoMV1xqHZYgir_bO0vNTVIDiHza6Hd1MllAdbGB9vg'
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