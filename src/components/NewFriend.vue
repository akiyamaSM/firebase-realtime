<template>
  <div class="hello">
    <form @submit.prevent="onSubmit">
      <div class="group">
        <label>Name</label>
        <input type="text" v-model="name">
      </div>
      <div class="group">
        <label>age</label>
        <input type="text" v-model="age">
      </div>
      <input type="submit" value="Add new Friend">
    </form>
  </div>
</template>

<script>
export default {
  name: 'new-friend',
    data(){
      return {
          name: '',
          age: ''
      }
    },
    methods:{
      onSubmit(){
          if(this.name && this.age){
              var name = this.name
              var age = this.age
              this.name = this.age = ''
              this.$emit('friendadded', name, age)
          }
      }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
