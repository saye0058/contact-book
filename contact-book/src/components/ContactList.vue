<template>
    <div>
      <h2>Contact List</h2>
      <ul>
        <li v-for="(contact, index) in contacts" :key="index">
          {{ contact.name }} - {{ contact.phone }}
          <button @click="deleteContact(index)">Delete</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: ['contacts'],
    methods: {
      deleteContact(index) {
        this.$emit('delete-contact', index);
      },
    },
  };
  </script>