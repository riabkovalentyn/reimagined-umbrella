<template>
  <div id="app" class="container">
    <h1 class="title">Bidding System</h1>
    <div v-if="!loggedIn">
      <RegisterForm @registered="loginUser"/>
      <LoginForm @loggedin="fetchBids"/>
    </div>
    <div v-else>
      <BidForm @bidsubmitted="fetchBids"/>
      <ul class="bid-list">
        <li v-for="(bid, index) in bids" :key="index" class="bid-item">{{ bid.name }} - ${{ bid.amount }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
 import RegisterForm from './components/registerForm.vue';
 import LoginForm from './components/loginUser.vue';
 import BidForm from './components/bidForm.vue';

export default {
  name: 'App',
  components: {
    RegisterForm,
    LoginForm,
    BidForm
  },
  data() {
    return {
      bids: [],
      loggedIn: false
    }
  },
  methods: {
    fetchBids() {
            fetch('http://localhost:3000/bids')
              .then(response => response.json())
              .then(data => {
                this.bids = data;
              })
              .catch(error => {
                console.error('Error fetching bids:', error);
              });
          },
          loginUser() {
            this.loggedIn = true;
            this.fetchBids();
          }
  }
}
</script>

<style lang="scss" >
@import './style';
</style>
