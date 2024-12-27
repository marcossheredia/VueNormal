<script setup>
import { ref } from 'vue'

const nombre = ref(' ');
const correo = ref(' ');
const password = ref(' ');

const errores = ref({
    nombre: '',
    correo: '',
    password: '',
});

const usuariosExistentes = ref(JSON.parse(localStorage.getItem('usuarios') || '[]'));

function registrarUsuario() {
    errores.value.nombre = ' ';
    errores.value.correo ='';
    errores.value.password ='';
   

let hayErrores=false;

if(!nombre.value.trim()){
    errores.value.nombre = 'El nombre es obligatorio';
    hayErrores=true;
}

if(!correo.value.trim() || !/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(correo.value)){
    errores.value.correo = 'El correo no es valido'
    hayErrores=true;
}else if (usuariosExistentes.value.some((u) => u.correo === correo.value)) {
    errores.value.correo = 'El correo ya existe';
    hayErrores=true;
}

if(!password.value.trim()){
    errores.value.password = 'La contraseña es obligatoria';
    hayErrores=true;
}

if(hayErrores) return;

const nuevoUsuario = { nombre: nombre.value, correo: correo.value, password: password.value };  
usuariosExistentes.value.push(nuevoUsuario);
localStorage.setItem('usuarios', JSON.stringify(usuariosExistentes.value));

window.alert('Usuario registrado correctamente');
}
</script>

<template>
    <div class="contenedor_registro">
        <h1>Registrarse</h1>
        <div>
            <label>Nombre</label>
            <input type="text" v-model="nombre" />
            <p v-if="errores.nombre" class="error">{{ errores.nombre }}</p>
        </div>
        <div>
            <label>Correo</label>
            <input type="text" v-model="correo" />
            <p v-if="errores.correo" class="error">{{ errores.correo }}</p>
        </div>
        <div>
            <label>Contraseña</label>
            <input type="password" v-model="password" />
            <p v-if="errores.password" class="error">{{ errores.password }}</p>
        </div>

        <button @click="registrarUsuario">Registrar</button>
    </div>
</template> 

<style scoped>

.contenedor_registro{
    background-color: fuchsia;
    padding: 20px;
    border-radius: 5px;
}

</style>
