
<template>
    <div>
      <Header class="Header" />
      <div class="full">
        <div class="container">
          <div class="form-container">
            <div class="form-group">
              <label for="formInput">Username or Email</label><br>
              <input type="text" v-model="usernameOrEmail" />
              <button @click="checkUserExists">Check</button>
  
              <div v-if="userExists">
                <router-link :to="{ name: 'resetPassword', params: { usernameOrEmail: usernameOrEmail }}">
                  Go to Reset Password
                </router-link>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        usernameOrEmail: '',
        userExists: false,
      };
    },
    methods: {
      async checkUserExists() {
        try {
          const response = await fetch('http://localhost:8080/mannit/login', {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json',
            },
            body: JSON.stringify({
              usernameOrEmail: this.usernameOrEmail,
            }),
          });
  
          if (response.ok) {
            const result = await response.json();
            this.userExists = result.exists;
  
            if (this.userExists) {
              // User exists, route to the reset password page
              this.$router.push({ name: 'resetPassword', params: { usernameOrEmail: this.usernameOrEmail } });
            }
          } else {
            console.error('Failed to check user existence');
          }
        } catch (error) {
          console.error('An error occurred while checking user existence', error.message);
        }
      },
    },
  };
  </script>
  
  <style scoped>
  /* @import '@/styles/forgot.css'; */
  </style>
  