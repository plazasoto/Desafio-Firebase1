<template>
    <div>
        <h1>Usuarios registrados</h1>
        <table>
            <thead>
                <tr>
                    <th>Nombre</th>
                    <th>Correo</th>
                </tr>
            </thead>
            <tbody v-for="usuario in usuarios" :key="usuario.id">
                <tr>
                    <td>{{ usuario.Nombre }}</td>
                    <td>{{ usuario.Correo }}</td>
                    <td><button @click="deleteUsuario(usuario.id)" >Eliminar</button></td>
                </tr>
            </tbody>
        </table>
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
        methods: {
            async deleteUsuario(userID) {
                const db = getFirestore(firebaseApp);
                const usersRef = doc(db, 'Usuarios' , userID);
                await deleteDoc(usersRef);
            }
        }
    };
</script>

<style scoped>
td, th{
    padding: 2px  20px;
    border: 1px whitesmoke;
    border-style: solid;
}

th{
    background-color: black;
    color: whitesmoke;
}
</style>