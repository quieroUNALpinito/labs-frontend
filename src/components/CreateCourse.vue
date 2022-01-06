import axios from 'axios';
<template>
    
    <div >
        <h3>Crear Curso</h3>
        <label>Nombre del Curso</label>
        <input type="text" v-model="nombre"><br>
        <label>Horas del Curso</label>
        <input type="number" v-model="duracion"><br>
        <button @click="crearCurso">Crear</button>
    </div>
</template>

<script type="application/javascript">
import axios from 'axios';
import {getAuthenticationToken} from '@/dataStorage';

export default{
    data(){
        return{
            nombre:"",
            duracion:0
        }
    },
    methods:{
        crearCurso: function(){
            axios.post("http://localhost:8080/profesor/crear-curso", {
                "courseName": this.nombre,
                "durationHours": this.duracion
            },{ params: { access_token: getAuthenticationToken() } }
            ).then( response => {
                    if( response.status !== 201 ){
                        alert( "Error en la creación del curso" );
                    }else{
                        alert("Curso creado");
                    }
            }).catch( error => {
                alert( 'Error en la petición' );
                console.log( error );
            } );   
        }
    }
}


</script>