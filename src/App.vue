<template>
  <div id="app">
    <new-friend @friendadded="addItem" @friendupdated="updateFriend" :friend="newFriend"></new-friend>

    <ul v-for="(friend, index) in friends" :key="index">
      <li>
        {{ friend.name}} is {{ friend.age}} 
        <span @click="deleteFriend(friend)">Close</span>
        <span @click="setToEditFriend(friend)"> Edit</span>
      </li>
    </ul>
  </div>
</template>

<script>

import Firebase from 'firebase'
import NewFriend from './components/NewFriend'

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
  data(){
    return {
      newFriend: {
        age: '',
        name: ''
      }
    }
  },
  components: {
      NewFriend
  },
  firebase: {
      friends: friendRef
  },
    methods: {
      addItem(friend){
          friendRef.push({
              'name': friend.name ,
              'age': friend.age
          })
          this.clearInput()
      },
      deleteFriend(friend){
        this.getItemRef(friend).remove()
      },
      getItemRef(item){
        return friendRef.child(item['.key'])
      },
      setToEditFriend(friend){
        this.newFriend = friend
      },
      updateFriend(friend){
        console.log(friend)
        this.clearInput()
        //this.getItemRef(friend)
      },
      clearInput(){
          this.newFriend = {
              age: '',
              name: ''
          };
      }
    }
}
</script>

<style>

</style>
