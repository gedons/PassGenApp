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

    <div class="mx-auto max-w-screen-xl px-4 py-16 sm:px-6 lg:px-8 font-thin">
      <div class="mx-auto max-w-lg text-center">
        <h1 class="text-2xl mt-24 font-bold sm:text-3xl">Login</h1>
    
        <p class="mt-4 text-gray-500">
          Use the form below to login into your account
        </p>
      </div>
     
      <form @submit.prevent="login" class="mx-auto mb-0 mt-8 max-w-md space-y-4">
        <div>
          <div v-if="error" class="mt-4 mb-4 text-red-500">
            {{ error }}
          </div>
          <label for="email" class="sr-only">Email</label>
    
          <div class="relative">
            <input
              type="email"
              v-model="email"
              class="w-full rounded-lg border-gray-200 p-4 pe-12 text-sm shadow-sm"
              placeholder="Enter email"
            />
    
            <span class="absolute inset-y-0 end-0 grid place-content-center px-4">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="size-4 text-gray-400"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M16 12a4 4 0 10-8 0 4 4 0 008 0zm0 0v1.5a2.5 2.5 0 005 0V12a9 9 0 10-9 9m4.5-1.206a8.959 8.959 0 01-4.5 1.207"
                />
              </svg>
            </span>
          </div>
        </div>
    
        <div>
          <label for="password" class="sr-only">Password</label>
    
          <div class="relative">
            <input
              type="password"
              v-model="password"
              class="w-full rounded-lg border-gray-200 p-4 pe-12 text-sm shadow-sm"
              placeholder="Enter password"
            />
    
            <span class="absolute inset-y-0 end-0 grid place-content-center px-4">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="size-4 text-gray-400"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"
                />
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"
                />
              </svg>
            </span>
          </div>
        </div>
    
        <div class="flex items-center justify-between">
          <p class="text-sm text-gray-500">
            No account?
            <router-link to="/register" class="underline">Sign up</router-link>
          </p>
    
          <button
            type="submit"
            class="inline-block rounded-lg bg-gray-900 px-5 py-3 text-sm font-medium text-white"
          >
            Login
          </button>         
        </div>
      </form>
    </div>
  </template>
  
  <script>
  // import Navbar from '../components/Navbar.vue';
  import axios from 'axios';
  import router from '../router';
  
  export default {
    // components: { Navbar },
    data() {
      return {
        email: '',
        password: '',
        error: null
      };
    },
    computed: {
      isLoggedIn() {
        return !!localStorage.getItem('token');
      }
    },
    methods: {
      async login() {
        try {
          const response = await axios.post('https://passgenapp.onrender.com/api/auth/login', {
            email: this.email,
            password: this.password
          });
          localStorage.setItem('token', response.data.token);
            this.$toast.success('Login successful.', {
                  timeout: 5000, 
            });
          router.push('/dashboard');
        } catch (error) {
          this.error = error.response.data.message || 'Login failed. Please try again.';
        }
      },
      logout(){
        localStorage.removeItem('token');
        router.push('/login');
     }

    }
  };
  </script>
  