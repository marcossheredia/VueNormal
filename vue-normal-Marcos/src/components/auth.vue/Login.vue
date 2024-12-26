<script setup>

import { ref } from 'vue';
import { defineEmits } from 'vue';

const emit = defineEmits(['cambioARegiter', 'evento2', 'evento3']);


function loginPresionado() {
    alert("El usuario se ha logueado correctamente: " + sUsuariio.value + " y la contraseña es: " + sPassword.value);
}


function registroPresionado() {
    emit('cambioARegiter');
}
</script>

<template>

    <div class="contenedor">
        <div id="login">
            <h2>Login</h2>
            <input type="text" placeholder="Email" v-model="sEmail" />
            <input type="password" placeholder="Contraseña" v-model="sPassword" />
            <button @click="loginPresionado">Login</button>
            <button @click="registroPresionado">Registro</button>
        </div>
    </div>
</template>

<style scoped>

</style>
