<template>
  <div class="hello">
    <form @submit.prevent="onSubmit">
      <div class="group">
        <label>Name</label>
        <input type="text" v-model="friend.name">
      </div>
      <div class="group">
        <label>age</label>
        <input type="text" v-model="friend.age">
      </div>
      <input type="submit" :value="this.getOperationString">
    </form>
  </div>
</template>

<script>
export default {
  name: 'new-friend',
  computed:{
    getOperationString(){
      return this.operation == false ? 'Modifier' : 'Ajouter';
    }
  },
  props: ['operation', 'friend'],
  methods:{
    onSubmit(){
        if(this.friend.name && this.friend.age){
            var friend_edited = this.friend 
            this.friend = null
            
            if(this.operation == true){
              this.$emit('friendadded', friend_edited)
              return;
            }

            this.$emit('friendupdated', friend_edited)
        }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
