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
                'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAwNjU4NjIsImV4cCI6MTcwMDA2OTQ2Miwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6ImJvcmlzLmRvdWFkeUBlcGl0ZWNoLmRpZ2l0YWwifQ.Zi1aDhuftUEJakKG-aFyoeRRZHaiIJI_IsXqh0w9uCS4kbiR1a1Md5ESQoer59wC75rBAUo7R0flpMU-sofRMACdzZsUJQSf1klDj6cC4BBrQknYRlXKFHVaxJIEZsgVuy7UKZ3qdq4A9fAiKSJIK1TbLKZMuJnf6JiYOcnd48yJ7BW1eZNjtMER8ADEaRR1UxnRsZp_WBrUCWrdvcw0SX20AywixA-jy7KVJEaukOcVKlRPZv-fTLK3Ku-sku1FqDaQ0xT0qao9y4VebGEtKi425A-dgXYVWN8lth1FvIwuEu83a_mJ_BZv8AKafujUv7DcZ22UmO4bOwvhQPiNzA'
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