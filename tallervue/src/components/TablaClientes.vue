<template>
    <div class="container">
        <h1>Tabla de clientes</h1>
        <table>
            <thead>
                <tr>
                    <th>Cedula</th>
                    <th>Nombre</th>
                    <th>Apellido</th>
                    <th>Direccion</th>
                    <th>Correo</th>
                    <th>Telefono</th>
                    
                </tr>
            </thead>
            <tbody>
              
                    <tr v-for="cliente in  clientes" :key="cliente.cedula">
                    <td>{{ cliente.cedula }}</td>
                    <td>{{ cliente.nombre }}</td>
                    <td>{{ cliente.apellido }}</td>
                    <td>{{ cliente.direccion }}</td>
                    <td>{{ cliente.correo }}</td>
                    <td>{{ cliente.telefono }}</td>
                </tr>
                   
                <router-view />
            
              
            </tbody>
        </table>
    </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      clientes: [],
    };
  },
  methods: {
    obtenerClientes() {
      // Método para obtener la lista de todos los clientes
      axios.get("http://localhost:8080/api/clientes/listar")
      .then((response) => {
        this.clientes = response.data;
      })
      .catch((error) => {
        console.error("Error al obtener clientes:", error);
      });
    },
  },
  mounted() {
    // Llamar al método para obtener la lista de clientes al cargar el componente
    this.obtenerClientes();
  },
};
</script>
