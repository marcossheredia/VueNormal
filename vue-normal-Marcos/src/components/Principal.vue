<script setup>
import { ref } from 'vue'

import Register from './Register.vue';

import Login from './Login.vue';

const mostrarLogin = ref(true);

function cambiarVista(){
    mostrarLogin.value =!mostrarLogin.value;
}

function usuarioLogueado(){
    window.alert('Redirigiendo al Inventario...')
}

</script>

<template>
    <div>
        <button @click="cambiarVista">
            {{ mostrarLogin ? 'Ir a registro' : 'Ir a login' }}
        </button>
        <Login v-if="mostrarLogin" @logueado="usuarioLogueado"/>
        <Register v-else/>
    </div>

</template>

<style scoped>



</style>
