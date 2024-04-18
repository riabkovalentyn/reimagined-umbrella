
<template>
    <form @submit.prevent="submitBid" class="form">
      <input type="text" v-model="name" placeholder="Your Name" class="input">
      <input type="number" v-model="amount" placeholder="Bid Amount" class="input">
      <button type="submit" class="button">Submit Bid</button>
    </form>
  </template>
  
  <script>
  export default {
    data() {
      return {
        name: '',
        amount: ''
      }
    },
    methods: {
                    submitBid() {
            // Assuming 'name' and 'amount' are data properties bound to input fields
            fetch('http://localhost:3000/bids', {
                method: 'POST',
                headers: {
                'Content-Type': 'application/json',
                'Authorization': localStorage.getItem('token') // Assuming you're using JWT for authentication
                },
                body: JSON.stringify({
                name: this.name,
                amount: this.amount
                })
            })
            .then(response => {
                if (response.ok) {
                // Bid submission successful
                this.$emit('bidsubmitted'); // Emitting event to notify parent component
                } else {
                // Bid submission failed
                throw new Error('Bid submission failed');
                }
            })
            .catch(error => {
                console.error('Bid submission error:', error);
                // Handle bid submission error (e.g., display error message to user)
            });
            }

    }
  }
  </script>
<style lang="scss" scoped>
@import "./style.scss"; 
</style>