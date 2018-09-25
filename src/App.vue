<template>
  <div id="app">

    <new-friend></new-friend>

    <ul v-for="friend in friends">
      <li> {{ friend.name}} is {{ friend.age}}</li>
    </ul>
  </div>
</template>

<script>

import Firebase from 'firebase'
let config =  {
    apiKey: "AIzaSyC1s58h60yYPHc_4Jq1VOwp1XlJPVHpTUc",
    authDomain: "just-talk-6c835.firebaseapp.com",
    databaseURL: "https://just-talk-6c835.firebaseio.com",
    projectId: "just-talk-6c835",
    storageBucket: "just-talk-6c835.appspot.com",
    messagingSenderId: "44245148892"
};

let app = Firebase.initializeApp(config);
let db = app.database();

let friendRef = db.ref('books');

export default {
  name: 'app',
  firebase: {
      friends: friendRef
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
