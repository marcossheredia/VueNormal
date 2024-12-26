<script setup>

import { ref } from 'vue'
import { defineEmits } from 'vue';

const sEmailre=ref('');
const sPasswordre=ref('');
const sRepetirPassword=ref('');

const emit = defineEmits('cambioALogin');

function registarPresionado(){
    alert ("El usuario es: " + sEmailre.value + " y la contraseña es: " + sPasswordre.value);
}

function cancelarPresionado(){
    emit('cambioALogin');
}
</script>

<template>
    <div class="contenedor">

        <div id="register">
            <h2>Registro</h2>
            <input type="text" placeholder="Email" v-model="sEmailre">
            <input type="password" placeholder="Contraseña" v-model="sPasswordre">
            <input type="password" placeholder="Repetir contraseña" v-model="sRepetirPassword">
            <button @click="registarPresionado">REGISTRAR</button>
            <button @click="cancelarPresionado">CANCELAR</button>
        </div>
    </div>
</template>

<style scoped>

</style>
