<template>
<!-- el propios formulario de VUETIFY contiene ya funciones predeterminadas muy importantes -->
<!-- VOY A CREAR DOS FORMULARIOS UNO PARA CREAR UN ELEMENTO Y OTRO PARA  EDITAR-->
<v-layout justify-center>

    <v-flex md4 v-if="!recibir_obj_persona.form_editar" > 
      <!-- FORMULARIO PARA AGREGAR -->
         <v-form
    ref="form"
    v-model="valid"
    lazy-validation
    
  >
    <div class="font-weight-medium blue--text text-center text-decoration-underline">AGREGAR ELEMENTO</div>
    <v-text-field
      v-model="nombre"
      :rules="nameRules"
      label="Nombre"
      required
    ></v-text-field>

    <v-text-field
      v-model="apellidos"
      :rules="nameRules"
      label="Apellidos"
      required
    ></v-text-field>

    <v-select
      v-model="cargo"
      :items="items"
      :rules="[v => !!v || 'Item is required']"
      label="Cargo"
      required
    ></v-select>

    <v-btn
      :disabled="!valid"
      color="success"
      class="mr-4"
      @click="agregar"
    >
      Agregar
    </v-btn>
    
    <v-btn
      color="error"
      class="mr-4"
      @click="reset"
    >
      Limpiar campos
    </v-btn>
  </v-form>
    </v-flex>
<!-- FORMULARIO DE EDITAR -->
<v-flex md4 v-else>
        <div class="font-weight-medium orange--text text-center text-decoration-underline">EDITAR ELEMENTO</div>
         <v-form
    ref="form"
    v-model="valid"
    lazy-validation
    
  >
    <!-- <p>{{recibir_obj_persona}}</p> //para imprimir el objeto recibido(prueba)-->
    <v-text-field
      v-model="recibir_obj_persona.nombre"
      :rules="nameRules"
      label="Nombre"
      required
    ></v-text-field>

    <v-text-field
      v-model="recibir_obj_persona.apellidos"
      :rules="nameRules"
      label="Apellidos"
      required
    ></v-text-field>

    <v-select
      v-model="recibir_obj_persona.cargo"
      :items="items"
      :rules="[v => !!v || 'Item is required']"
      label="Cargo"
      required
    ></v-select>

    <v-btn
      :disabled="!valid"
      color="orange"
      class="mr-4"
      @click="editar()"
    >
      Editar
    </v-btn>
    
    <v-btn
      color="error"
      class="mr-4"
      @click="reset_salir_edit"
    >
      Salir
    </v-btn>
  </v-form>
    </v-flex>
</v-layout>
 


 
</template>
<script>
  export default {
    data: () => ({
      valid: true,
      aparecer_agregar:true,
      nombre: '',
      apellidos:'',
      nameRules: [
        v => !!v || 'Name is required',
      ],
      cargo: null,
      items: [
        'Jefe',
        'Empleado',
      ],
      //VOY A CREAR UNA VARIABLE DUPLICADA YA QUE ME ARROJA UNA ADVERTENCIA EN LA CONSOLA AL IGUAL QUE EN EL 
      //COMPONENTE ELEMENTO aquí me piden que la inicialice por que el data esta así de esta manera data:()=>({....})
      aparecer_mensaje_vacios2:true,
      checkbox: false,
    }),
    props:['elementos','recibir_obj_persona','aparecer_mensaje_vacios'],
    methods: {
      agregar() {
        if(this.$refs.form.validate()){
          this.elementos.push({'nombre':this.nombre,'apellidos':this.apellidos,'cargo':this.cargo});
          this.$refs.form.reset()
          if(this.aparecer_mensaje_vacios===true){
            this.aparecer_mensaje_vacios2=false;
            this.$emit('enviar_aparecer_mensaje',this.aparecer_mensaje_vacios2);
          }
        }
      },
      reset () {
        this.$refs.form.reset()
      },
      editar(){
        let posicion = this.recibir_obj_persona.posi_emplea_edit;
        this.elementos[posicion].nombre = this.recibir_obj_persona.nombre;
        this.elementos[posicion].apellidos = this.recibir_obj_persona.apellidos;
        this.elementos[posicion].cargo = this.recibir_obj_persona.cargo;
        // this.$emit('empleado_editado',recibir_obj_persona);
        this.$refs.form.reset();
      },
      resetValidation () {
        this.$refs.form.resetValidation()
      },
      reset_salir_edit(){
        this.$refs.form.reset()
        this.recibir_obj_persona.form_editar=false;
      },
      // PROBANDO
      comprobar_si_elementos_vacio(){
        if(Object.keys(this.elementos).length===0){
          //   this.aparecer_mensaje_vacios=true;
          this.aparecer_mensaje_vacios2=true;  
          console.log(this.aparecer_mensaje_vacios2);
          this.$emit('enviar_aparecer_mensaje',this.aparecer_mensaje_vacios2);
        }
      }
    },
  }
</script>