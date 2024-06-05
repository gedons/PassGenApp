<template>

    <section class="relative mx-auto">
      <!-- navbar -->
    <nav class="flex justify-between bg-gray-900 text-white w-screen">
      <div class="px-5 xl:px-12 py-6 flex w-full items-center">
        <a class="text-3xl font-bold font-heading" href="/">
          <!-- <img class="h-9" src="logo.png" alt="logo"> -->
          SecurePass.App
        </a>
        <!-- Nav Links -->
        <ul class="hidden md:flex px-4 mx-auto font-semibold font-heading space-x-12">
          <li><a class="hover:text-gray-200" href="/">Home</a></li>
          <li><a class="hover:text-gray-200" href="#">Catagory</a></li>
          <li><a class="hover:text-gray-200" href="#">Collections</a></li>
          <li><a class="hover:text-gray-200" href="#">Contact Us</a></li>
        </ul>
        <!-- Header Icons -->
        <div class="hidden xl:flex space-x-5 items-center">                   
          <div v-if="isLoggedIn" class="flex">
              <button @click="logout" class="flex items-center hover:text-gray-200 font-semibold">
                    <span class="mr-2">End Session</span>                           
                </button>
                <router-link to="/dashboard">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 hover:text-gray-200" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5.121 17.804A13.937 13.937 0 0112 16c2.5 0 4.847.655 6.879 1.804M15 10a3 3 0 11-6 0 3 3 0 016 0zm6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>  
                </router-link>
                
          </div>
        
          <router-link v-else to="/register" class="flex items-center hover:text-gray-200 font-semibold">
              <span class="mr-2">Get Started</span>
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 hover:text-gray-200" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5.121 17.804A13.937 13.937 0 0112 16c2.5 0 4.847.655 6.879 1.804M15 10a3 3 0 11-6 0 3 3 0 016 0zm6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>                
          </router-link>
          
        </div>
      </div>
      <!-- Responsive navbar -->      
      <a class="navbar-burger self-center mr-12 xl:hidden" href="#">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 hover:text-gray-200" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
          </svg>
      </a>
    </nav>
    
   </section>

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
  // import Navbar from '../components/Navbar.vue';
  
  export default {
    // components: { NavBar },
    data() {
      return {
        password: '',
        loading: true,
        error: ''
      };
    },
    computed: {
      isLoggedIn() {
        return !!localStorage.getItem('token');
      }
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
    },
    logout(){
                localStorage.removeItem('token');
                 router.push('/login');
            }
  };
  </script>
  
  <style>
  /* Add any additional styles here */
  </style>
  