<script setup>
import { ref } from 'vue'


const correo = ref('');
const password = ref('');    
const errorLogin = ref('');

const emit = defineEmits(['logueado']);

function iniciarSesion() {
    errorLogin.value = '';

    const usuariosExistentes = JSON.parse(localStorage.getItem('usuarios')) || [];
    const usuarioValido = usuariosExistentes.find(
        (u) => u.correo === correo.value && u.password === password.value
    );

    if(usuarioValido) {
        emit('authenticated' );
        window.alert('Inicio de sesión exitoso');
    } else {
        errorLogin.value = 'Correo o contraseña incorrectos';
    }
}
</script>

<template>

    <div class="contenedor_login">
        <h1>Login</h1>
        <div>
            <label>Correo</label>
            <input type="email" v-model="correo" />
        </div>

        <div>
            <label>Contraseña</label>
            <input type="password" v-model="password" />
        </div>

        
        <button @click="iniciarSesion">Iniciar Sesión</button>
        <p v-if="errorLogin">{{ errorLogin }}</p>
        
    </div>

</template>

<style scoped>

.contenedor_login {
    background-color: rgb(42, 50, 165);
    padding: 20px;
    border-radius: 5px;
    color: white;
}

</style>
