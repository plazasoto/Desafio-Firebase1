<template>
    <div>
        <h2>Usuarios</h2>
        <ul>
            <li v-for="usuario in usuarios" :key="usuario.id">
                {{ usuario.Nombre }} - {{ usuario.Correo }}
            </li>
        </ul>
    </div>
</template>

<script>
    import { getFirestore, collection, onSnapshot, addDoc, doc, deleteDoc } from 'firebase/firestore';
    import firebaseApp from '../firebaseConfig';

    export default {
        data() {
            return {
                usuarios: [],
            };
        },
        mounted() {
            const db = getFirestore(firebaseApp);
            const usersRef = collection(db, 'Usuarios' );
            onSnapshot(usersRef, (snapshot) => {
                this.usuarios = snapshot.docs.map((doc) => ({ id: doc.id, ...doc.data() }));
            });
        },
    };
</script>