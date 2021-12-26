<template>
  <div class="signup">
    <h2>Sign up</h2>
    <input type="text" placeholder="Username" v-model="email">
    <input type="text" placeholder="Password" v-model="password">
    <button @click="signUp">Resister</button>
  </div>
</template>

<script>
import firebase from 'firebase/compat/app'
import 'firebase/compat/auth'
export default {
  name: 'Signup',
  data () {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    signUp: function () {
      firebase.auth().createUserWithEmailAndPassword(this.email, this.password).then(res => {
        console.log('Create account: ', res.user.email)
        firebase.auth().signInWithEmailAndPassword(this.email, this.password).then(r => {
          r.user.getIdToken().then(idToken => {
            // localStorage.setItem('jwt', idToken.toString())
            console.log(idToken)
          })
        }, err => {
          alert(err.message)
        })
      }).catch(error => {
        console.log(error.message)
      })
    }
  }
}
</script>

<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.signup {
  margin-top: 20px;
  display: flex;
  flex-flow: column nowrap;
  justify-content: center;
  align-items: center
}
input {
  margin: 10px 0;
  padding: 10px;
}
button {
  margin: 10px 0;
  padding: 10px;
}
</style>
