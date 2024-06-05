<template>

    <NavBar/>

    <div class="min-h-screen flex flex-col items-center justify-center bg-gray-100 p-4">
      <div class="bg-white p-6 rounded-lg shadow-md w-full max-w-md">
        <h2 class="text-2xl font-bold mb-4">Shared Password</h2>
        <div v-if="loading" class="text-center">Loading...</div>
        <div v-if="error" class="text-center text-red-500">{{ error }}</div>
        <div v-if="password" class="text-center">
          <p class="mb-4">Here is the shared password:</p>
          <p class="font-mono text-lg bg-gray-100 p-2 rounded">{{ password }}</p>
          <button @click="copyToClipboard(password)" class="mt-4 bg-blue-500 text-white px-4 py-2 rounded">Copy to Clipboard</button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  import Navbar from '../components/Navbar.vue';
  
  export default {
    components: { NavBar },
    data() {
      return {
        password: '',
        loading: true,
        error: ''
      };
    },
    methods: {
      async fetchPassword() {
        const id = this.$route.params.id;
        try {
          const response = await axios.get(`https://passgenapp.onrender.com/api/passwords/share/${id}`);
          this.password = response.data.password;
        } catch (error) {
          this.error = 'Failed to retrieve the password. Please try again.';
        } finally {
          this.loading = false;
        }
      },
      copyToClipboard(text) {
        navigator.clipboard.writeText(text).then(() => {
          alert('Password copied to clipboard!');
        }).catch(err => {
          alert('Failed to copy password. Please try again.');
        });
      }
    },
    created() {
      this.fetchPassword();
    }
  };
  </script>
  
  <style>
  /* Add any additional styles here */
  </style>
  