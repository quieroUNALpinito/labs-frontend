<template>
  <div class="container-fluid mt-2">
    <h1>Bienvenido al dummy</h1>
    <div class="row">
      <router-view></router-view>
    </div>
    <div >
        <CreateCourse/>
    </div>
  </div>
</template>

<script>
  import {getAuthenticationToken} from '@/dataStorage';
  import CreateCourse from '@/components/CreateCourse.vue'
  export default{
    name: "Home",
    components: {
      CreateCourse
      },
    beforeCreate( ){
      if( !getAuthenticationToken( ) ){
        this.$router.push( {name: 'login'} )
      }
    }
  }
</script>

<style>

</style>
