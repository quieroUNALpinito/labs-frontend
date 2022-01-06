<template>
  <div class="container-fluid mt-2">
    <h1>Bienvenido al dummy</h1>
    <div>
      <button @click="cursos" >Mis cursos</button>
      <button @click="nuevoRol" >Nuevo rol</button>
      <button @click="roles" >Roles</button>
      <button @click="nuevoCurso" v-if="this.profesor">Crear curso</button>
      <button @click="logout" >Logout</button>
    </div>
    <div class="row">
      <div class="m-5 p-5">
        <router-view></router-view>
      </div>
    </div>
  </div>
</template>

<script>
  import {getAuthenticationToken} from '@/dataStorage';
import axios from 'axios';

  export default{
    name: "Home",
    data(){
      return{
        misroles: null,
        profesor: false
      }
    },
    beforeCreate( ){
      if( !getAuthenticationToken( ) ){
        this.$router.push( {name: 'login'} )
      }
    },
    mounted: function(){
      this.checkRol()
    },
    methods:{
      logout: function(){
        localStorage.clear();
        this.$router.push("/")
      },
      cursos: function(){
        this.$router.push("/mis-cursos")
      },
      nuevoRol: function(){
        this.$router.push("/principal/nuevo-rol")
      },
      nuevoCurso: function(){
        this.$router.push("/principal/nuevo-curso")
      },
      roles: function(){
        this.$router.push("/principal/roles")
      },
      checkRol: function(){
        axios.get( this.$store.state.backURL+'/mis-roles', { params: { access_token: getAuthenticationToken( ) } } )
        .then( response => {
          if( response.status !== 200 ){
            alert( 'Error Obteniendo sus roles' );
          }else{
            this.misroles = response.data;
            for (const rol of this.misroles) {
              if(rol.id === 2){
                this.profesor = true;
                break;
              }
            }
          }
        } ).catch( error => {
          alert( 'Error en la petición' );
          console.log( error );
        } );
      }
    }
  }
</script>

<style>

</style>
