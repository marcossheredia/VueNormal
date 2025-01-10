<script setup>
import { ref } from 'vue'
import { createUserWithEmailAndPassword,sendEmailVerification } from 'firebase/auth';
import { useFirebaseAuth,useFirestore } from 'vuefire';
import {collection, addDoc, setDoc,doc } from "firebase/firestore";

const sUsuarioRe=ref('');
const sPasswordRe=ref('');
const sRepetirPasswordRe=ref('');
const errorMensaje=ref('');
const buenMensaje=ref('');
const sNombreUser=ref('');

const emit=defineEmits(["cambiarALogin"]);
const auth=useFirebaseAuth();
const db = useFirestore();

function presioneAceptar() {
    errorMensaje.value='';
    buenMensaje.value='';

    if(!sUsuarioRe.value || !sPasswordRe.value){
        errorMensaje.value='Todos los campos son obligatorios';
    }
    else{
        createUserWithEmailAndPassword(auth, sUsuarioRe.value, sPasswordRe.value)
        .then(registerOK)
        .catch(registerOK);
    }
} 

function registerNOK(error){
        
        if(error=="FirebaseError: Firebase: Error (auth/email-already-in-use)."){
            alert("USUARIO YA EXISTE, INTENTA LOGEARTE");
        }
        else{
            errorMensaje.value="FALLA POR: "+error;
        }
}

function crearPerfil(){
        const profileRef = collection(db, "/Profiles");
        const postRef=doc(profileRef, auth.currentUser.uid);
        setDoc(postRef,{nombre:sNombreUser.value})
        //addDoc(collectionRefPerfiles,datosNuevoPerfil)
        .then(perfilInsertadoOK)
        .catch(perfilInsertadoNOK);
}

    function perfilInsertadoOK(nuevoPerfilRef){
        alert("SE HA INSERTADO CORRECTAMENTE UN PERFIL NUEVO "+nuevoPerfilRef.id);
        emit("cambiarALogin");
}

    function perfilInsertadoNOK(error){
        
}
    
    function presioneCancelar(){
        emit("cambiarALogin");
}

</script>

<template>
    <div class="contenedor_registro">
        <h1>Registrarse</h1>
        <div>
            <label>Nombre</label>
            <input type="text" v-model="sUsuarioRe" />
        </div>
        <div>
            <label>Contraseña</label>
            <input type="password" v-model="sPasswordRe" />
        </div>
        <div>
            <label>Repetir Contraseña</label>
            <input type="password" v-model="sRepetirPasswordRe" />
        </div>
        <div>
            <label>NOMBRE:</label>
            <input v-model="sNombreUser" type="text"></input>
        </div>

        <button @click="presioneAceptar">ACEPTAR</button>
        <button @click="presioneCancelar">CANCELAR</button>

        <label>{{ errorMensaje }}</label>
        <label>{{ buenMensaje }}</label>
    </div>
</template> 

<style scoped>

    #contenedor_registro{
        background-color: fuchsia;
        padding: 20px;
        border-radius: 5px;
}

</style>
