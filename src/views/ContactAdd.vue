<template>
    <div>
      <h1>Create Contact</h1>
      <form>
        <label for="name">Name:</label>
        <input type="text" id="name" v-model="name">
        <label for="email">Email:</label>
        <input type="email" id="email" v-model="email">
        <label for="address">Address:</label>
        <input type="text" id="address" v-model="address">
        <label for="phone">Phone:</label>
        <input type="tel" id="phone" v-model="phone">
        <label for="favorite">Favorite:</label>
        <input type="checkbox" id="favorite" v-model="favorite">
        <button type="submit" @click.prevent="createContact">Create</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        name: '',
        email: '',
        address: '',
        phone: '',
        favorite: false
      }
    },
    methods: {
      createContact() {
        const newContact = {
          name: this.name,
          email: this.email,
          address: this.address,
          phone: this.phone,
          favorite: this.favorite
        }
   
fetch('http://localhost:3001/api/contacts', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(newContact)
})
.then(response => {
  if (response.ok) {
    // If the response is successful, redirect to the contact list page
    this.$router.push('/contacts')
  } else {
    // If the response is not successful, display an error message
    alert('Failed to create contact')
  }
})
.catch(error => {
  // If there is an error, display an error message
  alert('Failed to create contact')
})
      }
    }
  }
  </script>