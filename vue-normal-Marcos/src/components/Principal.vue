<script setup>
    import { defineProps } from 'vue';
    import Login from './auth.vue/Login.vue';
    import Register from './auth.vue/Register.vue';
    import { ref } from 'vue';


    const props=defineProps({
        sTitulo:{
            type:String,
            default:'Titulo de tu app'
        }
    }); 

    const blLoginVisible= ref(true);
    const blRegistroVisible = ref(false);

    function MostrarRegistro(){
        blLoginVisible.value=false;
        blRegistroVisible.value=true;
    }

    function MostrarLogin(){
        blLoginVisible.value=true;
        blRegistroVisible.value=false;
    }

    
</script>

<template>
    <div class="contenedor">
        <h1>{{ sTitulo }}</h1>
        <div class="loginregister">
            <Login v-if="blLoginVisible" @cambioARegistro="MostrarRegistro"></Login>
            <Register v-if="blRegistroVisible" @cambioALogin="MostrarRegistro"></Register>
        </div>
    </div>>
</template>

<style scoped>

</style>
