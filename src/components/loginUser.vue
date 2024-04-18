<template>
  <form @submit.prevent="loginUser" class="form">
    <input type="text" v-model="username" placeholder="Username" class="input">
    <input type="password" v-model="password" placeholder="Password" class="input">
    <button type="submit" class="button">Login</button>
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
            loginUser() {
        fetch('http://localhost:3000/login', {
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
            return response.json();
            } else {
            throw new Error('Invalid username or password');
            }
        })
        .then(data => {
            // Assuming the backend responds with a token upon successful login
            const token = data.token;
            localStorage.setItem('token', token);
            this.$emit('loggedin');
        })
        .catch(error => {
            console.error('Login error:', error);
            // Handle login error (e.g., display error message to user)
        });
        }
  }
}
</script>

<style lang="scss" scoped>
@import "./style.scss"; 
</style>