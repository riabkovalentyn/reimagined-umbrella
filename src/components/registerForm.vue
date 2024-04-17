
<template>
    <form @submit.prevent="registerUser" class="form">
      <input type="text" v-model="username" placeholder="Username" class="input">
      <input type="password" v-model="password" placeholder="Password" class="input">
      <button type="submit" class="button">Register</button>
    </form>
  </template>
  
  <script>
  export default {
    data() {
      return {
        username: '',
        password: ''
      }
    },
    methods: {
                registerUser() {
        // Assuming 'username' and 'password' are data properties bound to input fields
        fetch('http://localhost:3000/register', {
            method: 'POST',
            headers: {
            'Content-Type': 'application/json'
            },
            body: JSON.stringify({
            username: this.username,
            password: this.password
            })
        })
        .then(response => {
            if (response.ok) {
            // Registration successful
            this.$emit('registered'); // Emitting event to notify parent component
            } else {
            // Registration failed
            throw new Error('Registration failed');
            }
        })
        .catch(error => {
            console.error('Registration error:', error);
            // Handle registration error (e.g., display error message to user)
        });
        }
    }
  }
  </script>
  
