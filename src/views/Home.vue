<template>
  <div>
      <!-- <hello-world /> -->
      <Formulario :elementos="elementos" 
      :recibir_obj_persona="recibir_obj_persona"
      :aparecer_mensaje_vacios="aparecer_mensaje_vacios"
      @enviar_aparecer_mensaje="aparecer_mensaje_vacios=$event"/>
      
      
      <!-- 2 EMIT UNO PARA RECIBIR LOS DATOS DE LA PERSONA EDITADA Y PARA CORROBOR SI HAN ELIMINADO
      TODOS LOS ELEMENTO DEL OBJETO QUE DEVUELVA TRUE PARA QUE APARESCA EL MENSAJE DE QUE YA NO ELEMENTOS  -->
      <Cards-empleado :elementos="elementos" 
      :aparecer_mensaje_vacios="aparecer_mensaje_vacios"
      @enviando_datos="recibir_obj_persona = $event "
      @enviar_aparecer_mensaje="aparecer_mensaje_vacios=$event"/>
      <!-- <p>{{recibir_obj_persona.nombre}}--{{recibir_obj_persona.apellidos}}</p> -->
      <Mensaje-Element-Vacio v-if="aparecer_mensaje_vacios"></Mensaje-Element-Vacio>
      <!-- para corroborar si esta traendo la variable aparecer_mensaje_vacios-->
      <!-- <h1>{{aparecer_mensaje_vacios}}</h1> -->
  </div>
  
</template>

<script>
// EL ARRAY ELEMENTOS ESTARÁ PREVIAMENTE CON DATOS
// RECIBIES EL OBJETO A EDITAR A TRAVES DE UN EMIT DEL COMPONENTE ELEMENTO Y LO VUELVES
//ENVIAR AL ELEMENTO FORMULARIO PARA QUE LO MUESTRO EN FORM EDITAR
  import HelloWorld from '../components/HelloWorld';
  import Formulario from '../components/Formulario';
  import Elemento from '../components/Elemento';
  import Mensaje_vacio from '../components/mensj_elem_vacio.vue'
  export default {
    data() {
      return {
        elementos:[
                {
                    nombre:'Yomar',
                    apellidos:'Quispe Montero',
                    cargo:'Empleado',
                    
                },
                {
                    nombre:'Raul',
                    apellidos:'Cordova',
                    cargo:'Jefe'
                }
              ],
        recibir_obj_persona:{
        },
        persona_editada:{
        },
        aparecer_mensaje_vacios:false
      }
    },
    name: 'Home',
    components: {
      HelloWorld,
      'Formulario':Formulario,
      'Cards-empleado':Elemento,
      'Mensaje-Element-Vacio':Mensaje_vacio
    }
  }
</script>
