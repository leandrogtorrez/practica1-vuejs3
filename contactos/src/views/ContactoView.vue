<template>
    <div>
        <h1>{{ titulo }}</h1>
        <div class="filtro-container">
            <label for="busqueda" class="filtro-label">Filtro: </label>
            <input type="text" id="busqueda" v-model="busqueda" @input="buscaContactos">
        </div>
        <br>
        <table>
            <thead>
                <tr>
                    <th>ID</th>
                    <th>NAME</th>
                    <th>EMAIL</th>
                    <th>ADDRESS</th>
                    <th>PHONE</th>
                    <th>COUNTRY</th>
                    <th>CITY</th>
                    <th>ACTIONS</th>
                </tr>
                <tr v-if="indexParaEditar === null">
                    <th><input type="text" v-model="contactoNuevoObj.id"></th>
                    <th><input type="text" v-model="contactoNuevoObj.name"></th>
                    <th><input type="text" v-model="contactoNuevoObj.email"></th>
                    <th><input type="text" v-model="contactoNuevoObj.address"></th>
                    <th><input type="text" v-model="contactoNuevoObj.phone"></th>
                    <th><input type="text" v-model="contactoNuevoObj.country"></th>
                    <th><input type="text" v-model="contactoNuevoObj.city"></th>
                    <th><button @click="guardaNuevo()">Add</button></th>
                </tr>
                <tr v-else>
                    <th><input type="text" v-model="contactoEditarObj.id"></th>
                    <th><input type="text" v-model="contactoEditarObj.name"></th>
                    <th><input type="text" v-model="contactoEditarObj.email"></th>
                    <th><input type="text" v-model="contactoEditarObj.address"></th>
                    <th><input type="text" v-model="contactoEditarObj.phone"></th>
                    <th><input type="text" v-model="contactoEditarObj.country"></th>
                    <th><input type="text" v-model="contactoEditarObj.city"></th>
                    <th><button @click="guardaEdicion()">Save</button></th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(contacto, index) in contactosParaMostrar" :key="contacto.id">
                    <td>{{ contacto.id }}</td>
                    <td>{{ contacto.name }}</td>
                    <td>{{ contacto.email }}</td>
                    <td>{{ contacto.address }}</td>
                    <td>{{ contacto.phone }}</td>
                    <td>{{ contacto.country }}</td>
                    <td>{{ contacto.city }}</td>
                    <td>
                        <button @click="eliminarContacto(index)">Delete</button>
                        <button @click="editarContacto(contacto, index)">Edit</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>


<script>
export default {
    name: 'MiComponente',
    data() {
        return {
            titulo: 'Agenda de contactos',
            busqueda: '',
            contactoNuevoObj: {
                id: "",
                name: "",
                email: "",
                address: "",
                phone: "",
                country: "",
                city: ""
            },
            contactoEditarObj: {
                id: "",
                name: "",
                email: "",
                address: "",
                phone: "",
                country: "",
                city: ""
            },
            indexParaEditar: null,
            contactos: [
                
                {
                    id: 1,
name: "Alice Johnson",
email: "alice.johnson@example.com",
address: "123 Maple Street",
phone: "123-456-7890",
country: "USA",
city: "New York"
                },
                {
                    id: 2,
name: "Bob Smith",
email: "bob.smith@example.com",
address: "456 Oak Avenue",
phone: "987-654-3210",
country: "Canada",
city: "Toronto"
                },
                {
                    id: 3,
                    name: "Carol White",
                    email: "carol.white@example.com",
                    address: "789 Pine Road",
                    phone: "555-123-4567",
                    country: "UK",
                    city: "London"
                },
                {
                    id: 4,
                    name: "David Brown",
                    email: "david.brown@example.com",
                    address: "321 Elm Street",
                    phone: "444-555-6666",
                    country: "Australia",
                    city: "Sydney"
                },
                {
                    id: 5,
name: "Emily Davis",
email: "emily.davis@example.com",
address: "654 Spruce Lane",
phone: "333-444-5555",
country: "USA",
city: "Los Angeles"
                }
            ]
        }
    },
    computed: {
        contactosParaMostrar() {
            if (this.busqueda) {
                const busquedaLower = this.busqueda.toLowerCase();
                return this.contactos.filter(contacto =>
                    contacto.name.toLowerCase().includes(busquedaLower) ||
                    contacto.email.toLowerCase().includes(busquedaLower) ||
                    contacto.address.toLowerCase().includes(busquedaLower) ||
                    contacto.phone.toLowerCase().includes(busquedaLower) ||
                    contacto.country.toLowerCase().includes(busquedaLower) ||
                    contacto.city.toLowerCase().includes(busquedaLower)
                );
            }
            return this.contactos;
        }
    },
    methods: {
        guardaNuevo() {
            this.contactos.push(Object.assign({}, this.contactoNuevoObj));
            this.resetContactoNuevo();
        },
        eliminarContacto(index) {
            this.contactos.splice(index, 1);
        },
        guardaEdicion() {
            this.contactos[this.indexParaEditar] = Object.assign({}, this.contactoEditarObj);
            this.indexParaEditar = null;
            this.resetContactoEditar();
        },
        editarContacto(contacto, index) {
            this.indexParaEditar = index;
            this.contactoEditarObj = Object.assign({}, contacto);
        },
        resetContactoNuevo() {
            this.contactoNuevoObj = {
                id: "",
                name: "",
                email: "",
                address: "",
                phone: "",
                country: "",
                city: ""
            };
        },
        resetContactoEditar() {
            this.contactoEditarObj = {
                id: "",
                name: "",
                email: "",
                address: "",
                phone: "",
                country: "",
                city: ""
            };
        },
        buscaContactos() {
            /*
            Este método se mantiene por compatibilidad con el clic del botón.

            Ahora, el filtrado se realiza automáticamente a través de la propiedad calculada.
            */ 
        }
    }
}
</script>




<style scope>

h1 {
    color: #42b983;
}

table {
    width: 100%;
    border-collapse: collapse;
}

th,
td {
    border: 1px solid #ddd;
    padding: 8px;
}

th {
    background-color: #f2f2f2;
    text-align: left;
}

.filtro-container {
    display: flex;
    align-items: center;
}

.filtro-label {
    margin-right: 10px; 
}
</style>
