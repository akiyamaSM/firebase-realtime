<template>
  <div class="hello">
    <form @submit.prevent="onSubmit">
      <div class="group">
        <label>Name</label>
        <input type="text" v-model="friend_input.name">
      </div>
      <div class="group">
        <label>age</label>
        <input type="text" v-model="friend_input.age">
      </div>
      <input type="submit" :value="this.getOperationString">
    </form>
  </div>
</template>

<script>
export default {
  name: 'new-friend',
  data(){
    return {
        friend_input : {}
      };
  },
  computed:{
    getOperationString(){
      return this.friend_input[".key"] ? 'Modifier' : 'Ajouter';
    }
  },
  watch: {
      friend(newValue){
          this.friend_input = Object.assign({},newValue);
      }
  },
  props: ['friend'],
  methods:{
    onSubmit(){
        if(this.friend_input.name && this.friend_input.age){

            if(! this.friend_input[".key"]){
              this.$emit('friendadded', this.friend_input)
              return;
            }

            this.$emit('friendupdated', this.friend_input)
        }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
