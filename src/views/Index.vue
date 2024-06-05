<template>
    <Navbar />
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
    import Navbar from '../components/Navbar.vue';
    import GeneratePassword from '../components/GeneratePassword.vue';

    export default {
    components: {
        Navbar,
        GeneratePassword
    }
    };
  </script>