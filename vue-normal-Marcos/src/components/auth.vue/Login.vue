<script setup>
import { ref } from 'vue'


const sUsuario = ref('');
const sPassword = ref('');    

const emit = defineEmits(['logueado','solicitarRegistro']);

const auth = useFirebaseAuth();

function presioneLogin() {
    signInWithEmailAndPassword(auth,sUsuario.value,sPassword.value)
        .then(loginOK)
        .catch(loginNOK);
}

function loginOK(userCredential) {
    const user = userCredential.user;
    alert("Usuario autenticado correctamente");
    emit('logueado')
}

function loginNOK(reason) {
    alert("Usuario erroneo vuelvelo a intentar " + reason);
}

function presioneRegistrar(){
        emit('solicitaRegistro');
}

function presionaRecuperar(){
        sendPasswordResetEmail(auth,sUsuario.value);
}

</script>

<template>

    <div class="contenedor_login">
        <h1>Login</h1>
        <div>
            <label>Usuario</label>
            <input v-model ="sUsuario" type="text"/></input>
        </div>

        <div>
            <label>Contraseña</label>
            <input type="password" v-model="sPassword" /></input>
        </div>

        
        <button @click="presioneLogin">Iniciar Sesión</button>
        <button @click="presioneRegistrar">Registrar</button>
        <button @click="presionaRecuperar">Recuperar Contraseña</button>       
    </div>

</template>

<style scoped>

    #contenedor_login {
        background-color: rgb(42, 50, 165);
        padding: 20px;
        border-radius: 5px;
        color: white;
    }

</style>
