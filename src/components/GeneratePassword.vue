<template>
    <div class="flex -mt-11 items-center justify-center p-4">
      <div class="bg-white p-6 rounded-lg shadow-md w-full max-w-md">
        <h2 class="text-2xl font-bold mb-4">Generate Password</h2>
        <form @submit.prevent="generatePassword" class="space-y-4 font-thin">
          <div>
            <label class="block mb-2">Password Length: {{ passwordLength }}</label>
            <input 
              type="range" 
              min="8" 
              max="32" 
              v-model="passwordLength" 
              class="w-full bg-gray-900"
              style="accent-color: #1f2937;"
            >
          </div>
          <div class="flex items-center">
            <input 
              type="checkbox" 
              v-model="options.lowercase" 
              id="lowercase"
              class="bg-gray-200 rounded"
              style="accent-color: #1f2937;"
            >
            <label for="lowercase" class="ml-2">Include Lowercase</label>
          </div>
          <div class="flex items-center">
            <input 
              type="checkbox" 
              v-model="options.uppercase" 
              id="uppercase"
              class="bg-gray-200 rounded"
              style="accent-color: #1f2937;"
            >
            <label for="uppercase" class="ml-2">Include Uppercase</label>
          </div>
          <div class="flex items-center">
            <input 
              type="checkbox" 
              v-model="options.numbers" 
              id="numbers"
              class="bg-gray-200 rounded"
              style="accent-color: #1f2937;"
            >
            <label for="numbers" class="ml-2">Include Numbers</label>
          </div>
          <div class="flex items-center">
            <input 
              type="checkbox" 
              v-model="options.specialChars" 
              id="specialChars"
              class="bg-gray-200 rounded"
              style="accent-color: #1f2937;"
            >
            <label for="specialChars" class="ml-2">Include Special Characters</label>
          </div>
          <button type="submit" class="w-full bg-gray-900 text-white p-2 rounded">Generate</button>
        </form>
        <div v-if="generatedPassword" class="mt-4 p-2 bg-green-100 rounded">
          <p class="font-thin mb-2"><span class="font-bold">Generated Password:</span> {{ generatedPassword }}</p>

          <!-- <div class="mt-2">
            <p class="font-thin"><span class="font-bold">Strength:</span> {{ strength.score }}</p>             
          </div> -->
          <div v-if="strength.feedback.warning" class="mt-2 text-yellow-600">
            <p class="font-semibold">Warning:</p>
            <p class="ml-2">{{ strength.feedback.warning }}</p>
          </div>
          <div v-if="strength.feedback.suggestions.length" class="mt-2">
            <p class="font-semibold">Suggestions:</p>
            <ul class="list-disc list-inside ml-4">
              <li v-for="(suggestion, index) in strength.feedback.suggestions" :key="index">{{ suggestion }}</li>
            </ul>
          </div>


            <button @click="copyToClipboard" class="w-50 text-gray-900 font-thin underline p-2 rounded">Copy to Clipboard</button>
            <button v-if="isAuthenticated" @click="savePassword" class="w-full bg-gray-800 text-white p-2 rounded">Save Password</button>
            <router-link to="/login" v-else class="w-50 ml-4 bg-gray-900 font-thin text-white p-2 rounded">save password</router-link>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  import router from '../router';
  
  export default {
    data() {
      return {
        passwordLength: 12,
        options: {
          lowercase: true,
          uppercase: true,
          numbers: true,
          specialChars: true,
        },
        generatedPassword: '',
        strength: {
        score: '',
        feedback: {
          warning: '',
          suggestions: []
        }
      },
      isAuthenticated: !!localStorage.getItem('token')
      };
    },
    methods: {
      async generatePassword() {
          try {
            const response = await axios.post('https://passgenapp.onrender.com/api/passwords/generate', {
              length: this.passwordLength,
              options: this.options
            });
            this.generatedPassword = response.data.password || '';
            this.$toast.success('Password Generated Successfully.', {
                      timeout: 5000, 
            });
            this.strength = response.data.strength || { score: '', feedback: { warning: '', suggestions: [] } };

          } catch (error) {
            alert('Failed to generate password. Please try again.');
            this.generatedPassword = '';
            this.strength = { score: '', feedback: { warning: '', suggestions: [] } };
          }
      },

      copyToClipboard() {
            navigator.clipboard.writeText(this.generatedPassword)
            .then(() => {
              this.$toast.success('Password copied to clipboard.', {
                  timeout: 5000, 
                });
            })
            .catch(err => {
              this.$toast.error('Failed to copy password.', {
                  timeout: 5000, 
                });
                console.error('Failed to copy password:', err);
            });
       },

       async savePassword() {
          try {
            const token = localStorage.getItem('token');
            if (!token) {
              alert('You must be logged in to save passwords.');
              return;
            }

            await axios.post('https://passgenapp.onrender.com/api/passwords/save', {
              password: this.generatedPassword,
              strength: this.strength
            }, {
              headers: {
                'Authorization': `Bearer ${token}`
              }
            });
            this.$toast.success('Password Saved Successfully.', {
                      timeout: 5000, 
            });
            router.push('/dashboard');
          } catch (error) {
            this.$toast.error('Failed to save password. Please try again.', {
                      timeout: 5000, 
            });
           
          }
       }
     
    }
  };
  </script>
  