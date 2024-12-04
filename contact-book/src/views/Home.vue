<template>
    <div id="contact-book">
      <h1>Contact Book</h1>
      <input type="text" v-model="filter" placeholder="Search contacts..." />
      <ul>
        <li v-for="contact in filteredContacts" :key="contact.id">
          {{ contact.name }} - {{ contact.phone }}
          <button @click="editContact(contact.id)">Edit</button>
          <button @click="deleteContact(contact.id)">Delete</button>
        </li>
      </ul>
      <button @click="addContact">Add Contact</button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        filter: '',
        contacts: [
          { id: 1, name: 'Alice', phone: '123-456-7890' },
          { id: 2, name: 'Bob', phone: '987-654-3210' },
        ],
      };
    },
    computed: {
      filteredContacts() {
        return this.contacts.filter(contact =>
          contact.name.toLowerCase().includes(this.filter.toLowerCase())
        ).sort((a, b) => a.name.localeCompare(b.name));
      },
    },
    methods: {
      addContact() {
        const name = prompt('Enter contact name:');
        const phone = prompt('Enter contact phone:');
        if (name && phone) {
          this.contacts.push({ id: Date.now(), name, phone });
        }
      },
      editContact(id) {
        const contact = this.contacts.find(c => c.id === id);
        if (contact) {
          contact.name = prompt('Edit contact name:', contact.name) || contact.name;
          contact.phone = prompt('Edit contact phone:', contact.phone) || contact.phone;
        }
      },
      deleteContact(id) {
        this.contacts = this.contacts.filter(contact => contact.id !== id);
      },
    },
  };
  </script>
  
  <style>
  #contact-book {
    max-width: 500px;
    margin: 20px auto;
    border: 1px solid #ccc;
    padding: 20px;
    border-radius: 5px;
  }
  
  input {
    margin-bottom: 10px;
    padding: 8px;
    width: 100%;
  }
  
  button {
    margin-left: 10px;
  }
  </style>