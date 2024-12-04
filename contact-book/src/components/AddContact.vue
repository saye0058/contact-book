<template>
    <div>
      <h2>Add Contact</h2>
      <form @submit.prevent="submitContact">
        <input v-model="name" placeholder="Name" required />
        <input v-model="phone" placeholder="Phone" required />
        <button type="submit">Add</button>
      </form>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    setup(props, { emit }) {
      const name = ref('');
      const phone = ref('');
  
      const submitContact = () => {
        emit('add-contact', { name: name.value, phone: phone.value });
        name.value = '';
        phone.value = '';
      };
  
      return { name, phone, submitContact };
    },
  };
  </script>