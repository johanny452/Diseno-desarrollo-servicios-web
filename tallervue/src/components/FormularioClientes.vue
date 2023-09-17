<template>
  <div class="container">
    <h1>Formulario de Clientes</h1>

    <form id="student-form" @submit.prevent="guardar">
      <div class="form-group">
        <label for="cedula">cedula:</label>
        <input type="number" id="cedula" name="cedula" required  v-model="cedula" />
      </div>
      
      <div class="form-group">
        <label for="nombre">nombre:</label>
        <input type="text" id="nombre" name="nombre" required v-model="nombre"/>
      </div>
      <div class="form-group">
        <label for="apellido">apellido:</label>
        <input type="text" id="apellido" name="apellido" required v-model="apellido"/>
      </div>
      <div class="form-group">
        <label for="direccion">direccion:</label>
        <input type="text" id="direccion" name="direccion" required v-model="direccion"/>
      </div>
      <div class="form-group">
        <label for="correo">correo:</label>
        <input type="text" id="correo" name="correo" required v-model="correo"/>
      </div>
      <div class="form-group">
        <label for="telefono">telefono:</label>
        <input type="number" id="telefono" name="telefono" required v-model="telefono" />
      </div>

      <button type="submit" id="guardar" name="guardar">Guardar</button><br />
      <button type="button" id="eliminar" name="eliminar" @click="eliminar"> Eliminar</button ><br />
      <button type="button" id="actualizar" name="actualizar"  @click="actualizar"> Actualizar</button><br />
      <button type="button" id="consultar" name="consultar" @click="consultar"> Consultar</button><br />
    </form>
  </div>
</template>

<script>

import axios from "axios";

export default {
  
  data() {

    return {
      cedula: '',
      nombre: '',
      apellido: '',
      direccion: '',
      correo: '',
      telefono: '',
    };

  },

  methods: {
    guardar() {
      
      axios
        .post('http://localhost:8082/api/clientes', {
          cedula: this.cedula,
          nombre: this.nombre,
          apellido: this.apellido,
          direccion: this.direccion,
          correo: this.correo,
          telefono: this.telefono,
        })
        .then((response) => {
          console.log('Cliente registrado con éxito:', response.data);
          alert("exito");
          this.cedula = '';
          this.nombre = '';
          this.apellido = '';
          this.direccion = '';
          this.correo = '';
          this.telefono = '';
         
        })
        .catch((error) => {
          console.error('Error al registrar cliente:', error);
        });
    },
    
    consultar() {
      
      axios
        .get('http://localhost:8082/api/clientes/'+this.cedula)
        .then((response) => {
          // Actualizar los campos del formulario con los datos del cliente consultado
          this.nombre = response.data.nombre;
          this.apellido = response.data.apellido;
          this.direccion = response.data.direccion;
          this.correo = response.data.correo;
          this.telefono = response.data.telefono;
        })
        .catch((error) => {
          console.error("Error al consultar cliente:", error);
        });
    },


    actualizar() {
      
      axios
        .put('http://localhost:8082/api/clientes/actualizar/' + this.cedula, {
          cedula:this.cedula,
          nombre: this.nombre,
          apellido: this.apellido,
          direccion: this.direccion,
          correo: this.correo,
          telefono: this.telefono,
        })
        .then((response) => {
          console.log("Cliente actualizado con éxito:", response.data);
        })
        .catch((error) => {
          console.error("Error al actualizar clientes:", error);
        });
    },
    eliminar() {
     
      axios
        .delete('http://localhost:8082/api/clientes/'+this.cedula)
        .then(() => {
          console.log("Cliente eliminado con éxito");
          // Limpiar los campos del formulario después de eliminar
          this.cedula = '';
          this.nombre = '';
          this.apellido = '';
          this.direccion = '';
          this.correo = '';
          this.telefono = '';
        })
        .catch((error) => {
          console.error("Error al eliminar cliente:", error);
        });
    },
  },
};
</script>
