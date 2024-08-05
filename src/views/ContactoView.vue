<template>
    <div>
        <h1>{{ title }}</h1>
        <div class="filter">
            Filtro: <input type="search" v-model="searchText">
        </div>
    </div>
    <table>
        <thead>
            <tr>
                <th>Id</th>
                <th>Name</th>
                <th>Email</th>
                <th>Address</th>
                <th>Phone</th>
                <th>Country</th>
                <th>City</th>
                <th></th>
            </tr>
            <tr>
                <th></th>
                <th><input type="text" v-model="contactNewObj.name"></th>
                <th><input type="text" v-model="contactNewObj.email"></th>
                <th><input type="text" v-model="contactNewObj.address"></th>
                <th><input type="text" v-model="contactNewObj.phone"></th>
                <th><input type="text" v-model="contactNewObj.country"></th>
                <th><input type="text" v-model="contactNewObj.city"></th>
                <th><button @click="saveNewContact()">Agregar</button></th>
            </tr>
            <tr v-if="updateIndexId !== null">
                <th></th>
                <th><input type="text" v-model="contactUpdateObj.name"></th>
                <th><input type="text" v-model="contactUpdateObj.email"></th>
                <th><input type="text" v-model="contactUpdateObj.address"></th>
                <th><input type="text" v-model="contactUpdateObj.phone"></th>
                <th><input type="text" v-model="contactUpdateObj.country"></th>
                <th><input type="text" v-model="contactUpdateObj.city"></th>
                <th><button @click="saveUpdatedContact()">Guardar</button></th>
            </tr>
    </thead>
    <tbody>
        <tr v-for="(contact,index) in contactsList" :key="contact.id">
            <td>{{ contact.id }}</td>
            <td>{{ contact.name }}</td>
            <td>{{ contact.email }}</td>
            <td>{{ contact.address }}</td>
            <td>{{ contact.phone }}</td>
            <td>{{ contact.country }}</td>
            <td>{{ contact.city }}</td>
            <td>
                <button class="delete-btn" @click="deleteContact(index)">Eliminar {{ index }}</button>
                <button class="edit-btn" @click="editContact(contact,index)">Editar {{ index }}</button>
            </td>
        </tr>
    </tbody>
    </table>
</template>
<script>
export default {
    name: 'MiComponente',
    data() { 
        return {
            title: 'Agenda de Contactos',
            searchText: '',
            updateIndexId:null,
            contactNewObj: {
                id: null,
                name: '',
                email: '',
                address: '',
                phone: '',
                country: '',
                city: ''
            },
            contactUpdateObj: {
                id: null,
                name: '',
                email: '',
                address: '',
                phone: '',
                country: '',
                city: ''
            },
            contactsList: [
                { id: 1, name: 'John Doe', email: 'john.doe@example.com', address: '123 Main St', phone: '123-456-7890', country: 'USA', city: 'New York' },
                { id: 2, name: 'Jane Smith', email: 'jane.smith@example.com', address: '456 Elm St', phone: '987-654-3210', country: 'Canada', city: 'Ottawa' },
                { id: 3, name: 'Alice Johnson', email: 'alice.johnson@example.com', address: '789 Park Ave', phone: '321-654-9870', country: 'USA', city: 'Los Angeles' },
                { id: 4, name: 'Emily Johnson', email: 'emily.johnson@x.dummyjson.com', address: '626 Main Street', phone: '+81 965-431-3024', country: 'United States', city: 'Phoenix' },
                { id: 5, name: 'Michael Williams', email: 'michael.williams@x.dummyjson.com', address: '385 Fifth Street', phone: '+49 258-627-6644', country: 'United States', city: 'Los Angeles' },
                { id: 6, name: 'Sarah Davis', email:'sarah.davis@x.dummyjson.com', address: '274 Elm Street', phone: '+44 789-654-3210', country: 'United Kingdom', city: 'London' },
                { id: 7, name: 'David Lee', email: 'david.lee@x.dummyjson.com', address: '174 Elm Street', phone: '+654-3210', country: 'United Kingdom', city: 'London' },
                { id: 8, name: 'Jessica Brown', email: 'jessica.brown@x.dummyjson.com', address: '567 Park Avenue', phone: '+358 123-456-7890', country: 'Finland', city: 'Helsinki' },
                { id: 9, name: 'Christopher Wilson', email: 'christopher.wilson@x.com', address: '1642 Ninth Street', phone: '+81 210-652-2785', country: 'United States', city: 'Dallas' },
                { id: 10, name: 'Daniel Rodriguez', email: 'daniel.rodriguez@x.dummyjson.com', address: '123 Main Street', phone: '+55 123-456-7890', country: 'Brazil', city: 'Sao Paulo' },
                { id: 11, name: 'Matthew Thompson', email: 'matthew.thompson@x.dummyjson.com', address: '456 Elm Street', phone: '+62 812-345-6789', country: 'Indonesia', city: 'Jakarta' },
                { id: 12, name: 'David Garcia', email: 'david.garcia@x.dummyjson.com', address: '789 Park Ave', phone: '+44 789-654-3210', country: 'United Kingdom', city: 'London' },
                { id: 13, name: 'John Smith', email: 'john.smith@x.dummyjson.com', address: '607 Fourth Street', phone: '+91 759-776-1614', country: 'United States', city: 'Jacksonville' },
                { id: 14, name: 'Emily Davis', email: 'emily.davis@x.dummyjson.com', address: '626 Main Street', phone: '+81 965-431-3024', country: 'United States', city: 'Phoenix' },
            ]
        }
    },
    components: {
        // Registro de componentes que se utilizaran.
    },
    methods: {
        saveNewContact() {
            this.contactNewObj.id = this.contactsList.length + 1;
            this.contactsList.push(Object.assign({}, this.contactNewObj));
        },
        deleteContact(index) { 
            this.contactsList.splice(index, 1);
        },
        editContact(contact, index) {
            this.updateIndexId = index;
            this.contactUpdateObj = Object.assign({}, contact);
        },
        saveUpdatedContact(contact) { 
            this.contactsList[this.updateIndexId] = Object.assign({}, this.contactUpdateObj);
            this.updateIndexId = null;
        }
    },
    computed: {
        contactsList() {
            return this.contactsList.filter(contact =>
                contact.name.toLowerCase().includes(this.searchText.toLowerCase()) || 
                contact.email.toLowerCase().includes(this.searchText.toLowerCase())
        )
        }
    },
    props: {
        // propiedades que el componente puede recibir.
    },
    emits: [] // los eventos personalizados que el componente puede emitir.
}
</script>
<style scoped>
h1 {
    color: #42b983;
}
table {
    width: 100%;
    border-collapse: collapse;
}
th, td {
    border: 1px solid #ddd;
    padding: 8px;
}
th {
    background-color: #f2f2f2;
    /*text-align: left;*/
}
button{
    margin-left: 4px;
    padding: 5px;
    color: white;
    border: none;
    cursor: pointer; 
}
th button {
    background-color: #4CAF50;
}
.delete-btn{
    background-color: #f44336;
}
.edit-btn{
    background-color: #FF8000;
}
.filter{
    margin-bottom: 12px;
}
</style>