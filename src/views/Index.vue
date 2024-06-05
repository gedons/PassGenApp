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
    
    <div class="relative flex flex-col-reverse py-16 lg:pt-0 lg:flex-col lg:pb-0">
        <div class="inset-y-0 top-0 right-0 z-0 w-full max-w-xl px-4 mx-auto md:px-0 lg:pr-0 lg:mb-0 lg:mx-0 lg:w-7/12 lg:max-w-full lg:absolute xl:px-0">
            <svg class="absolute left-0 hidden h-full text-white transform -translate-x-1/2 lg:block" viewBox="0 0 100 100" fill="currentColor" preserveAspectRatio="none slice">
            <path d="M50 0H100L50 100H0L50 0Z"></path>
            </svg>
            <img
            class="object-cover w-full h-56 rounded shadow-lg lg:rounded-none lg:shadow-none md:h-96 lg:h-full"
            src="https://images.unsplash.com/photo-1589935447067-5531094415d1?q=80&w=1260&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
            alt=""
            />
        </div>
        <div class="relative flex flex-col items-start w-full max-w-xl px-4 mx-auto md:px-0 lg:px-8 lg:max-w-screen-xl">
            <div class="mb-16 lg:my-40 lg:max-w-lg lg:pr-5">
            <p class="inline-block px-3 py-px mb-4 text-xs font-semibold tracking-wider text-teal-900 uppercase rounded-full bg-green-100">
                Brand new
            </p>
            <h2 class="mb-5 font-sans text-3xl font-bold tracking-tight text-gray-900 sm:text-4xl sm:leading-none">
                Welcome to SecurePass<br class="hidden md:block" />                            
            </h2>
            <p class="pr-5 mb-5 text-base font-thin text-gray-700 md:text-lg">
                SecurePass is a cutting-edge password management application designed to simplify and secure your digital life. With SecurePass, you can generate strong, unique passwords, store them securely, and access them whenever you need them all from one convenient platform.
            </p>
            <div class="flex items-center">
                <router-link
                to="/login"
                class="inline-flex items-center justify-center h-12 px-6 mr-6 font-medium tracking-wide text-white transition duration-200 rounded shadow-md bg-gray-900 hover:bg-gray-700 focus:shadow-outline focus:outline-none"
                >
                Get started
                </router-link>
                <a href="https://www.techopedia.com/definition/31414/password-generator" target="_blank" aria-label="" class="inline-flex items-center font-semibold text-gray-800 transition-colors duration-200 hover:text-gray-700">Learn more</a>
            </div>
            </div>
        </div>
    </div>

    <div class="flex flex-col-reverse py-16 lg:pt-0 lg:flex-col lg:pb-0">
        <div class="inset-y-0 top-0 right-0 z-0 w-full max-w-xl px-4 mx-auto md:px-0 lg:pr-0 lg:mb-0 lg:mx-0 lg:w-7/12 lg:max-w-full lg:absolute xl:px-0 xl:mt-56">
            <GeneratePassword />
        </div>         
    </div>

    
   
  </template>

  <script>
    // import Navbar from '../components/Navbar.vue';
    import GeneratePassword from '../components/GeneratePassword.vue';

    export default {
    components: {
        // Navbar,
        GeneratePassword
    },
    computed: {
          isLoggedIn() {
            return !!localStorage.getItem('token');
          }
    },

    methods: {
            logout(){
                localStorage.removeItem('token');
                 router.push('/login');
            }
        },

    };
  </script>