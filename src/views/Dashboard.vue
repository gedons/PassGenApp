<template>
  <DashboardNav/>
  <div class="container mx-auto mt-10 font-thin">
    <h1 class="text-2xl text-center text-gray-800 lg:text-4xl">User Dashboard!</h1>

    <section class="mt-8">
      <div class="container px-6 py-10 mx-auto">
          <h1 class="text-3xl font-semibold text-gray-800 capitalize lg:text-4xl ">explore our <br> awesome <span class="underline decoration-gray-800">Features</span></h1>
          
          <p class="mt-4 text-gray-500 xl:mt-6">
            SecurePass.App lets you  securely store, manage, and access your login credentials. Developed by {DIVINE}, {}, {}, {}, {}
          </p>
          
          <h1 class="text-2xl font-semibold mt-6 capitalize text-gray-800 lg:text-4xl">Available Passwords</h1>
          <div v-if="passwords.length === 0">
              <p class="mt-8 mb-4 font-semibold">No Password Available</p>
              <router-link to="/" class="bg-gray-900 text-white px-4 py-2 rounded ">New Password</router-link>
          </div>
         
          <div v-else class="grid grid-cols-1 gap-8 mt-8 xl:mt-4 xl:gap-12 md:grid-cols-2 xl:grid-cols-3">
            <div v-for="password in passwords" :key="password._id">
              <div class="p-8 space-y-3 border-2 border-gray-400 dark:border-gray-300 rounded-xl">
                    <div class="flex">
                        <span class="inline-block text-gray-500 dark:text-gray-400">
                          <svg fill="#000000" width="30px" height="30px" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <path d="M16.9499909,19 C16.7183558,20.1411202 15.709479,21 14.5,21 L5.5,21 C4.11928813,21 3,19.8807119 3,18.5 L3,11.5 C3,10.290521 3.85887984,9.28164422 5,9.05000906 L5,8 C5,5.23857625 7.23857625,3 10,3 C12.7614237,3 15,5.23857625 15,8 L15,9.05000906 C16.1411202,9.28164422 17,10.290521 17,11.5 L17,13 L18.5,13 C19.8807119,13 21,14.1192881 21,15.5 L21,16.5 C21,17.8807119 19.8807119,19 18.5,19 L16.9499909,19 L16.9499909,19 Z M15.9146471,19 L11.5,19 C10.1192881,19 9,17.8807119 9,16.5 L9,15.5 C9,14.1192881 10.1192881,13 11.5,13 L16,13 L16,11.5 C16,10.710487 15.3900375,10.0634383 14.6156506,10.0043921 C14.5785296,10.0131823 14.5398081,10.0178344 14.5,10.0178344 C14.4540106,10.0178344 14.4094714,10.0116254 14.367175,10 L5.5,10 C4.67157288,10 4,10.6715729 4,11.5 L4,18.5 C4,19.3284271 4.67157288,20 5.5,20 L14.5,20 C15.1531094,20 15.7087289,19.5825962 15.9146471,19 L15.9146471,19 Z M6,9 L14,9 L14,8 C14,5.790861 12.209139,4 10,4 C7.790861,4 6,5.790861 6,8 L6,9 Z M20,16.5 L20,15.5 C20,14.6715729 19.3284271,14 18.5,14 L11.5,14 C10.6715729,14 10,14.6715729 10,15.5 L10,16.5 C10,17.3284271 10.6715729,18 11.5,18 L18.5,18 C19.3284271,18 20,17.3284271 20,16.5 Z M11.5,15 L12.5,15 C12.7761424,15 13,15.2238576 13,15.5 L13,16.5 C13,16.7761424 12.7761424,17 12.5,17 L11.5,17 C11.2238576,17 11,16.7761424 11,16.5 L11,15.5 C11,15.2238576 11.2238576,15 11.5,15 Z M14.5,15 L15.5,15 C15.7761424,15 16,15.2238576 16,15.5 L16,16.5 C16,16.7761424 15.7761424,17 15.5,17 L14.5,17 C14.2238576,17 14,16.7761424 14,16.5 L14,15.5 C14,15.2238576 14.2238576,15 14.5,15 Z M17.5,15 L18.5,15 C18.7761424,15 19,15.2238576 19,15.5 L19,16.5 C19,16.7761424 18.7761424,17 18.5,17 L17.5,17 C17.2238576,17 17,16.7761424 17,16.5 L17,15.5 C17,15.2238576 17.2238576,15 17.5,15 Z"></path> </g></svg>
                        </span>
                        <div class="justify-end mt-1 ml-2">
                          <p><span class="font-semibold">Date:</span> {{formatDate(password.date)}}</p>
                        </div>
                    </div>
  
                  <h1 class="text-2xl font-semibold text-gray-700 capitalize ">password</h1>
  
                  <p class="text-gray-500">
                    {{ password.visible ? password.password : '✨✨✨'  }}
                  </p>
  
                  <button @click="toggleVisibility(password)" class="inline-flex p-2 text-gray-500 capitalize transition-colors duration-200 transform bg-gray-100 rounded-full  hover:underline hover:text-gray-600 dark:hover:text-gray-500">
                    <svg class="w-6 h-6" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <path opacity="0.5" d="M2 12C2 8.22876 2 6.34315 3.17157 5.17157C4.34315 4 6.22876 4 10 4H14C17.7712 4 19.6569 4 20.8284 5.17157C22 6.34315 22 8.22876 22 12C22 15.7712 22 17.6569 20.8284 18.8284C19.6569 20 17.7712 20 14 20H10C6.22876 20 4.34315 20 3.17157 18.8284C2 17.6569 2 15.7712 2 12Z" stroke="#1C274C" stroke-width="1.5"></path> <path d="M12 10V14M10.2676 11L13.7317 13M13.7314 11L10.2673 13" stroke="#1C274C" stroke-width="1.5" stroke-linecap="round"></path> <path d="M6.73241 10V14M4.99999 11L8.46409 13M8.46386 11L4.99976 13" stroke="#1C274C" stroke-width="1.5" stroke-linecap="round"></path> <path d="M17.2681 10V14M15.5356 11L18.9997 13M18.9995 11L15.5354 13" stroke="#1C274C" stroke-width="1.5" stroke-linecap="round"></path> </g></svg>
                  </button>
                  <button v-if="password.visible" @click="copyToClipboard(password.password)" class="w-50  text-gray-900 font-thin underline p-2 rounded">Copy to Clipboard</button>

                  <div class="flex justify-end mb-2">
                    <button @click="editPassword(password)" class=" text-white px-1 py-1 rounded mr-2">
                      <svg class="w-6 h-6" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <path d="M21.2799 6.40005L11.7399 15.94C10.7899 16.89 7.96987 17.33 7.33987 16.7C6.70987 16.07 7.13987 13.25 8.08987 12.3L17.6399 2.75002C17.8754 2.49308 18.1605 2.28654 18.4781 2.14284C18.7956 1.99914 19.139 1.92124 19.4875 1.9139C19.8359 1.90657 20.1823 1.96991 20.5056 2.10012C20.8289 2.23033 21.1225 2.42473 21.3686 2.67153C21.6147 2.91833 21.8083 3.21243 21.9376 3.53609C22.0669 3.85976 22.1294 4.20626 22.1211 4.55471C22.1128 4.90316 22.0339 5.24635 21.8894 5.5635C21.7448 5.88065 21.5375 6.16524 21.2799 6.40005V6.40005Z" stroke="#000000" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path> <path d="M11 4H6C4.93913 4 3.92178 4.42142 3.17163 5.17157C2.42149 5.92172 2 6.93913 2 8V18C2 19.0609 2.42149 20.0783 3.17163 20.8284C3.92178 21.5786 4.93913 22 6 22H17C19.21 22 20 20.2 20 18V13" stroke="#000000" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path> </g></svg>
                    </button>
                    <button @click="deletePassword(password._id)" class="text-white px-1 py-1 rounded">
                      <svg class="w-6 h-6" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <path d="M10 12V17" stroke="#ff0000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"></path> <path d="M14 12V17" stroke="#ff0000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"></path> <path d="M4 7H20" stroke="#ff0000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"></path> <path d="M6 10V18C6 19.6569 7.34315 21 9 21H15C16.6569 21 18 19.6569 18 18V10" stroke="#ff0000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"></path> <path d="M9 5C9 3.89543 9.89543 3 11 3H13C14.1046 3 15 3.89543 15 5V7H9V5Z" stroke="#ff0000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"></path> </g></svg>
                    </button>
                    <button @click="sharePassword(password._id)" class="text-white px-1 py-1 rounded">
                      <svg class="w-6 h-6" viewBox="-1 0 26 26" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:sketch="http://www.bohemiancoding.com/sketch/ns" fill="#000000"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <title>share</title> <desc>Created with Sketch Beta.</desc> <defs> </defs> <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd" sketch:type="MSPage"> <g id="Icon-Set" sketch:type="MSLayerGroup" transform="translate(-312.000000, -726.000000)" fill="#000000"> <path d="M331,750 C329.343,750 328,748.657 328,747 C328,745.343 329.343,744 331,744 C332.657,744 334,745.343 334,747 C334,748.657 332.657,750 331,750 L331,750 Z M317,742 C315.343,742 314,740.657 314,739 C314,737.344 315.343,736 317,736 C318.657,736 320,737.344 320,739 C320,740.657 318.657,742 317,742 L317,742 Z M331,728 C332.657,728 334,729.343 334,731 C334,732.657 332.657,734 331,734 C329.343,734 328,732.657 328,731 C328,729.343 329.343,728 331,728 L331,728 Z M331,742 C329.23,742 327.685,742.925 326.796,744.312 L321.441,741.252 C321.787,740.572 322,739.814 322,739 C322,738.497 321.903,738.021 321.765,737.563 L327.336,734.38 C328.249,735.37 329.547,736 331,736 C333.762,736 336,733.762 336,731 C336,728.238 333.762,726 331,726 C328.238,726 326,728.238 326,731 C326,731.503 326.097,731.979 326.235,732.438 L320.664,735.62 C319.751,734.631 318.453,734 317,734 C314.238,734 312,736.238 312,739 C312,741.762 314.238,744 317,744 C318.14,744 319.179,743.604 320.02,742.962 L320,743 L326.055,746.46 C326.035,746.64 326,746.814 326,747 C326,749.762 328.238,752 331,752 C333.762,752 336,749.762 336,747 C336,744.238 333.762,742 331,742 L331,742 Z" id="share" sketch:type="MSShapeGroup"> </path> </g> </g> </g></svg>
                    </button>
                  </div>
              </div>      
            </div>       
          </div>
      </div>
    </section>

  <div v-if="showEditModal" class="fixed inset-0 bg-gray-600 bg-opacity-75 flex items-center justify-center">
    <div class="bg-white p-6 rounded-lg shadow-md w-full max-w-md">
      <h2 class="text-2xl font-bold mb-4">Edit Password</h2>
      <form @submit.prevent="updatePassword" class="space-y-4">
        <div>
          <label class="block mb-2">Password</label>
          <input type="text" v-model="currentPassword.password" class="w-full p-2 border rounded">
        </div>         
        <div class="flex justify-end space-x-2">
          <button @click="showEditModal = false" class="bg-red-500 text-white px-4 py-2 rounded">Cancel</button>
          <button type="submit" class="bg-gray-900 text-white px-4 py-2 rounded">Update</button>
        </div>
      </form>
    </div>
  </div>

    <div v-if="shareableLink" class="fixed inset-0 bg-gray-600 bg-opacity-75 flex items-center justify-center">
      <div class="bg-white p-6 rounded-lg shadow-md w-full max-w-md">
        <h2 class="text-2xl font-bold mb-4">Shareable Link</h2>
        <div class="space-y-4">
          <input type="text" :value="shareableLink" readonly class="w-full p-2 border rounded">
          <div class="flex justify-end space-x-2">
            <button @click="shareableLink = ''" class="bg-gray-500 text-white px-4 py-2 rounded">Close</button>
            <button @click="copyToClipboard(shareableLink)" class="bg-blue-500 text-white px-4 py-2 rounded">Copy Link</button>
          </div>
        </div>
      </div>
    </div>
</div>
  </template>
  
  <script>
  import router from '../router';
  import axios from 'axios';
  import DashboardNav from '../components/DashboardNav.vue';
 
  
  export default {
    components: { DashboardNav },
    data() {
      return {
        passwords: [],
        showEditModal: false,
        shareableLink: '',
        currentPassword: {
          _id: '',
          password: '',           
        }
      };
    },

    methods: {
      
      async fetchPasswords() {
      try {
        const token = localStorage.getItem('token');
        const response = await axios.get('http://localhost:5000/api/passwords', {
          headers: {
            'Authorization': `Bearer ${token}`
          }
        });
        this.passwords = response.data.map(password => ({
          ...password,
          visible: false
        }));
      } catch (error) {
        console.error('Error :', error);
      }
      },
      toggleVisibility(password) {
        password.visible = !password.visible;
      },
      editPassword(password) {
        this.currentPassword = { ...password };
        this.showEditModal = true;
      },
      async updatePassword() {
        try {
          const token = localStorage.getItem('token');
          await axios.put(`http://localhost:5000/api/passwords/${this.currentPassword._id}`, this.currentPassword, {
            headers: {
              'Authorization': `Bearer ${token}`
            }
          });
          this.showEditModal = false;
          this.fetchPasswords();
          this.$toast.success('Password Updated Successfully.', {
                      timeout: 5000, 
          });
        } catch (error) {
          alert('Failed to update password. Please try again.');
        }
      },
      async deletePassword(id) {
        const confirmation = confirm('Are you sure you want to delete this password?');
        if (confirmation) {
            try {
            const token = localStorage.getItem('token');
            await axios.delete(`http://localhost:5000/api/passwords/${id}`, {
              headers: {
                'Authorization': `Bearer ${token}`
              }
            });
            this.fetchPasswords();
            this.$toast.success('Password Deleted Successfully.', {
                  timeout: 5000, 
            });
          } catch (error) {
            this.$toast.success('Failed to delete password. Please try again', {
                  timeout: 5000, 
            });          
          }
        }

      },
      formatDate(date) {
        const options = { year: 'numeric', month: 'long', day: 'numeric', hour: '2-digit', minute: '2-digit', second: '2-digit' };
        return new Date(date).toLocaleDateString('en-US', options);
      },
      async sharePassword(id) {
        try {
          const token = localStorage.getItem('token');
          const response = await axios.post(`http://localhost:5000/api/passwords/share/${id}`, {}, {
            headers: {
              'Authorization': `Bearer ${token}`
            }
          });
          this.shareableLink = response.data.shareableLink;
        } catch (error) {
          alert('Failed to generate shareable link. Please try again.');
        }
      },
      copyToClipboard(password) {
        navigator.clipboard.writeText(password).then(() => {
          this.$toast.success('Password copied to clipboard.', {
                  timeout: 5000, 
            });
        }).catch(err => {
          this.$toast.error('Failed to copy password.', {
                  timeout: 5000, 
          });
          console.error('Failed to copy password:', err);
        });
      } 
    },
      created() {
        this.fetchPasswords();
      }
  };
  </script>
  