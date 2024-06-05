<template>
    <Navbar />

    <div class="mx-auto max-w-screen-xl px-4 py-16 sm:px-6 lg:px-8 font-thin">
      <div class="mx-auto max-w-lg text-center">
        <h1 class="text-2xl mt-24 font-bold sm:text-3xl">Register</h1>
    
        <p class="mt-4 text-gray-500">
         Use the form below to create an account
        </p>
      </div>
     
      <form @submit.prevent="register" class="mx-auto mb-0 mt-8 max-w-md space-y-4">
        <div>
          <div v-if="error" class="mt-4 mb-4 text-red-500">
            {{ error }}
          </div>
          <label for="email" class="sr-only">Name</label>
    
          <div class="relative">
            <input
              type="text"
              v-model="name"
              class="w-full rounded-lg border-gray-200 p-4 pe-12 text-sm shadow-sm"
              placeholder="Enter Name"
            />
     
          </div>
        </div>
        <div>
          <label for="email" class="sr-only">Email</label>
    
          <div class="relative">
            <input
              type="email"
              v-model="email"
              class="w-full rounded-lg border-gray-200 p-4 pe-12 text-sm shadow-sm"
              placeholder="Enter Email"
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
              placeholder="Enter Password"
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
            Already have an account?
            <router-link to="/login" class="underline">Sign in</router-link>
          </p>
    
          <button
            type="submit"
            class="inline-block rounded-lg bg-gray-900 px-5 py-3 text-sm font-medium text-white"
          >
            Register
          </button>
          
        </div>
      </form>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  import router from '../router';
  import Navbar from '../components/Navbar.vue';
  
  export default {
    components: { Navbar },
    data() {
      return {
        name: '',
        email: '',
        password: '',
        error: null
      };
    },
  methods: {
      async register() {
        try {
          const response = await axios.post('http://localhost:5000/api/auth/register', {
            name: this.name,
            email: this.email,
            password: this.password
          });
          localStorage.setItem('token', response.data.token);
          this.$toast.success('Registration successful.', {
		            timeout: 5000, 
		  });  
          router.push('/dashboard');
        } catch (error) {
          this.error = error.response.data.message || 'Registration failed. Please try again.';
        }
      }
    }
  };
  </script>
  