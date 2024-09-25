<template>
    <div>
        <h1>Formulario</h1>
        <form @submit.prevent="addUsuario">
            <input v-model="nombreUsuario" placeholder="Nombre Completo" />
            <input v-model="correoUsuario" type="email" placeholder="Correo Electrónico">
            <button type="submit">Agregar</button>
        </form>


    </div>
</template>

<script>
    import { getFirestore, collection, onSnapshot, addDoc, doc, deleteDoc } from 'firebase/firestore';
    import firebaseApp from '../firebaseconfig';
    export default {
        data() {
            return {
                nombreUsuario: '',
                correoUsuario: '',
            };
        },
        methods: {
            async addUsuario() {
                if (this.nombreUsuario.trim() === '' ) return;
                const db = getFirestore(firebaseApp);
                const usersRef = collection(db, 'Usuarios' );
                await addDoc(usersRef, { Nombre: this.nombreUsuario, Correo: this.correoUsuario });
                this.nombreUsuario = ''; 
                this.correoUsuario = ''; 
            },
        }
    };
</script>