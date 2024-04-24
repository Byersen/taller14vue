<template>
  <div id="app">
    <h1>Sistema de nombres</h1>

    <div id="app">
      <h2>Agregar nombres</h2>
      <form @submit.prevent="agregarNombre">
        <input v-model.trim="nuevoNombre" placeholder="nombre">
        <input v-model.trim="nuevoApellido" placeholder="apellido">
        <button type="submit">agregar</button>
      </form>
    </div>

    <div>
      <h2>Lista de nombres</h2>
      <ul>
        <li v-for="(nombre, index) in nombres" :key="index">
          {{nombre.nombre}} {{nombre.apellido}}
          <button @click="eliminarNombre(index)">Eliminar </button>
          <button @click="editorNombre(index)">Editar</button>

        </li>
      </ul>
    </div>

  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      nombres: [], nuevoNombre: '', nuevoApellido: '', editor: false, indexEditor: null, editorNombre: '', editorApellido: ''
    }
  },

  methods: {
      agregarNombre() {
        const nombre = this.cambiarTexto(this.nuevoNombre);
        const apellido = this.cambiarTexto(this.nuevoApellido);
        this.nombres.push({ nombre, apellido });
        this.nuevoNombre = '';
        this.nuevoApellido = '';
      },
      eliminarNombre(index) {
        this.nombres.splice(index, 1);
      },
      editarNombre(index) {
        this.editor = true;
        this.indexEditor = index;
        const nombre = this.nombres[index];
        this.editorNombre = nombre.nombre;
        this.editorApellido = nombre.apellido;

      },
      actualizarNombre() {
        const index = this.indexEditor;
        const nombre = this.cambiarTexto(this.editorNombre);
        const apellido = this.cambiarTexto(this.editorApellido);
        this.nombres.splice(index, 1, { nombre, apellido });
    
      },
    
      cambiarTexto(texto) {
        return texto.charAt(0).toUpperCase() + texto.slice(1).toLowerCase();
      }
    }
  };
</script>

<style >
/*Parte de css */
body {
  font-family: Arial, Helvetica, sans-serif;
  margin: 20px;
}

h1, h2 {
  text-align: center;
}

form {
  display: flex;
  justify-content: center;
  margin-bottom: 24px;
}

input {
  padding: 10px;
  margin-right: 15px;
}

button {
  padding: 10px 15px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>

