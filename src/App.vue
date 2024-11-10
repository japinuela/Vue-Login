<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>

    <div class="login-container">
      <h2>Iniciar Sesión</h2>
      <form @submit.prevent="login" class="login-form">
        <input v-model="username" placeholder="Usuario" class="input-field" />
        <input v-model="password" type="password" placeholder="Contraseña" class="input-field" />
        <button type="submit" class="login-button">Login</button>
      </form>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import axios from 'axios' // Importa Axios

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data() {
    return {
      username: '', // Almacena el nombre de usuario
      password: ''  // Almacena la contraseña
    }
  },
  methods: {
    async login() {
      const formData = new URLSearchParams();
      formData.append('loginName', this.username);
      formData.append('password', this.password);

      try {
        const response = await axios.post('http://localhost:8080/login.php', formData, {
          headers: { 'Content-Type': 'application/x-www-form-urlencoded' }
        });
        console.log('Respuesta del servidor:', response.data);
      } catch (error) {
        console.error('Error en el inicio de sesión:', error);
      }
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}


/* Estilos del formulario de inicio de sesión */
.login-container {
  max-width: 400px;
  margin: 50px auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  background-color: #f9f9f9;
}

.login-container h2 {
  margin-bottom: 20px;
  color: #333;
  font-size: 24px;
}

.login-form {
  display: flex;
  flex-direction: column;
}

.input-field {
  margin-bottom: 15px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
}

.input-field:focus {
  outline: none;
  border-color: #42b983;
  box-shadow: 0 0 5px rgba(66, 185, 131, 0.3);
}

.login-button {
  padding: 10px;
  font-size: 16px;
  color: #fff;
  background-color: #42b983;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.login-button:hover {
  background-color: #369e6b;
}

.login-button:focus {
  outline: none;
}
</style>