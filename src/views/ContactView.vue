<template>
  <div class="container mt-5" id="app">
    <h1 class="text-center mb-4">Agenda de Contactos</h1>
    <div class="mb-3">
      <input v-model="filter" class="form-control" placeholder="Filtro: nombre, correo electrónico o país" />
    </div>
    <table class="table table-bordered">
      <thead class="thead-light">
        <tr>
          <th>ID</th>
          <th>Nombre</th>
          <th>Correo Electrónico</th>
          <th>Dirección</th>
          <th>Teléfono</th>
          <th>País</th>
          <th>Ciudad</th>
          <th>Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>
            <button @click="addContact" class="btn btn-primary btn-sm">Agregar</button>
          </td>
          <td><input v-model="newContact.name" class="form-control form-control-sm" placeholder="Nombre" /></td>
          <td><input v-model="newContact.email" class="form-control form-control-sm" placeholder="Correo Electrónico" /></td>
          <td><input v-model="newContact.address" class="form-control form-control-sm" placeholder="Dirección" /></td>
          <td><input v-model="newContact.phone" class="form-control form-control-sm" placeholder="Teléfono" /></td>
          <td><input v-model="newContact.country" class="form-control form-control-sm" placeholder="País" /></td>
          <td><input v-model="newContact.city" class="form-control form-control-sm" placeholder="Ciudad" /></td>
          <td>
            <button @click="saveContact" class="btn btn-success btn-sm">Guardar</button>
          </td>
        </tr>
        <tr v-for="contact in filteredContacts" :key="contact.id">
          <td>{{ contact.id }}</td>
          <td>{{ contact.name }}</td>
          <td>{{ contact.email }}</td>
          <td>{{ contact.address }}</td>
          <td>{{ contact.phone }}</td>
          <td>{{ contact.country }}</td>
          <td>{{ contact.city }}</td>
          <td>
            <button @click="editContact(contact)" class="btn btn-warning btn-sm">Editar</button>
            <button @click="deleteContact(contact.id)" class="btn btn-danger btn-sm">Eliminar</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
data() {
  return {
    filter: '',
    contacts: [],
    newContact: this.getEmptyContact(),
    contactToEdit: null
  };
},
created() {
    this.fetchContacts();
},
computed: {
  filteredContacts() {
    return this.contacts.filter(contact => 
      contact.name.toLowerCase().includes(this.filter.toLowerCase()) || 
      contact.email.toLowerCase().includes(this.filter.toLowerCase()) ||
      contact.country.toLowerCase().includes(this.filter.toLowerCase())
    );
  }
},
methods: {
  fetchContacts() {
   //this.axios.get(this.baseUrl + '/contactos')
   this.axios.get('http://localhost:3000/contactos')
   
      .then(response => {
          this.contacts = response.data;
        })
        .catch(error => {
          console.error('Hubo un error al obtener los datos:', error);
        });
    },
  getEmptyContact() {
    return {
      id: null,
      name: '',
      email: '',
      address: '',
      phone: '',
      country: '',
      city: ''
    };
  },
  addContact() {
    this.newContact = this.getEmptyContact();
    this.contactToEdit = null;
  },
  saveContact() {
    if (this.contactToEdit) {
      Object.assign(this.contactToEdit, this.newContact);
    } else {
      this.newContact.id = this.contacts.length + 1;
      this.contacts.push(this.newContact);
    }
    this.newContact = this.getEmptyContact();
    this.contactToEdit = null;
  },
  editContact(contact) {
    this.contactToEdit = contact;
    this.newContact = { ...contact };
  },
  deleteContact(id) {
    this.contacts = this.contacts.filter(contact => contact.id !== id);
    if (confirm("¿Esta Seguro de eliminar el registro?")) {
                const vm = this;
                this.axios.delete(this.baseUrl + "/clientes/" + id)
                    .then(function (response) {
                        console.log(response);
                        vm.getList();
                        vm.$toast.show("Registro eliminado.", "danger");
                    })
                    .catch(function (error) {
                        console.error(error);
                    });
            }


  }
}
};
</script>

<style>
#app {
max-width: 90%;
margin: auto;
padding: 20px;
}

table {
width: 90%;
border-collapse: collapse;
}

th, td {
border: 1px solid #ddd;
padding: 8px;
}

th {
background-color: #f2f2f2;
}

input {
width: 100%;
padding: 8px;
box-sizing: border-box;
margin-bottom: 10px;
}

button {
padding: 5px 5px;
margin: 5px 0;
}

@media (max-width: 768px) {
table, thead, tbody, th, td, tr {
  display: block;
}

th {
  display: none;
}

tr {
  margin-bottom: 10px;
}

td {
  border: none;
  position: relative;
  padding-left: 50%;
}

td:before {
  content: attr(data-label);
  position: absolute;
  left: 10px;
  font-weight: bold;
}
}
</style>