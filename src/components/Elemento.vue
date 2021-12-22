<template>
<!-- el array elementos es enviado desde la vista home -->
<v-container fluid md-4>
    <v-layout row wrap>
    <!-- <v-flex> -->
            <v-card
            v-for="(elemento,index) in elementos" :key="index"
            class="mx-auto mb-5 mt-4"
            max-width="400"
            color="orange"
        >
        <v-card-text>
        <p class="text-h4 text--primary">
            {{elemento.nombre}}
        </p>
        <p>{{elemento.apellidos}}</p>
        <div class="text--primary">
            <br>
            {{elemento.cargo}}
        </div>
        </v-card-text>
        <v-card-actions>

        <v-btn           
            depressed
            color="green"
            @click="editar(index)"
            
            >
            Editar
        </v-btn>
        
        <v-btn
            depressed
            color="error"
            @click="eliminar(index)"
        >
            Eliminar
        </v-btn>
        </v-card-actions>
            </v-card>
            
    <!-- </v-flex> -->
</v-layout>
</v-container>

 
</template>
<script>
  export default {
      data() {
          return {
            nombreeditado:'',
            apellido_edit:'',
            empleado_editar:{
                nombre:'',
                apellidos:'',
                cargo:'',
                form_editar:false,
                posi_emplea_edit:0,
                // probando en la consola me salía una advertencia así que declare otra variable
                //aparecer_mensaje_vacios2 con esto ya no sale esa advertencia(NO ES ERROR)
                aparecer_mensaje_vacios2:false
            },
            
          }
      },
      props:['elementos','aparecer_mensaje_vacios'],
      methods:{
          eliminar(posicion){
            //   alert("aksjkajsk"+posicion)
            this.elementos.splice(posicion,1);
            this.comprobar_si_elementos_vacio();
          },
          editar(posicion){
            
            this.nombreeditado=this.elementos[posicion].nombre;
            this.apellido_edit=this.elementos[posicion].apellidos;
            //   this.$emit("click",);
            //   console.log(this.elementos[posicion].nombre);
            // this.$emit('enviando_datos',this.nombreeditado,this.apellido_edit);

            this.empleado_editar.nombre=this.elementos[posicion].nombre;
            this.empleado_editar.apellidos=this.elementos[posicion].apellidos;
            this.empleado_editar.cargo =this.elementos[posicion].cargo;
            this.empleado_editar.form_editar = true;
            this.empleado_editar.posi_emplea_edit=posicion;
            // console.log('POSICION'+this.empleado_editar.posi_emplea_edit);
            this.$emit('enviando_datos',this.empleado_editar);
            
          },
          comprobar_si_elementos_vacio(){
              if(Object.keys(this.elementos).length===0){
                //   this.aparecer_mensaje_vacios=true;
                  this.aparecer_mensaje_vacios2=true;  
                  console.log(this.aparecer_mensaje_vacios2);
                  this.$emit('enviar_aparecer_mensaje',this.aparecer_mensaje_vacios2);
              }
          }
      }
  }
</script>