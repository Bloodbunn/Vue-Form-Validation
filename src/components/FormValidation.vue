<template>
    <div class="mx-auto p-5 max-w-lg">
        <form @submit.prevent="submitForm">
           <div class="flex flex-col text-left mb-3">
              <label class="text-lg text-black font-semibold" for="name">Name:</label> 
              <input v-model="formData.name" class="p-1 border border-gray-300 max-[350px]:text-sm" id="name" type="text" placeholder="Enter Your Name">
              <span v-if="!isNameValid" class="text-sm text-red-500">Please enter your name</span>
           </div>

           <div class="flex flex-col text-left mb-3">
              <label  class="text-lg text-black font-semibold" for="email">Email:</label> 
              <input v-model="formData.email" class="p-1 border border-gray-300 max-[350px]:text-sm" id="email" type="email" placeholder="Enter Your Email">
              <span v-if="!isEmailValid" class="text-sm text-red-500">Please enter a valid email</span>
           </div>

           <div class="flex flex-col text-left mb-3">
              <label class="text-lg text-black font-semibold" for="password">Password:</label> 
              <input v-model="formData.password" class="p-1 border border-gray-300 max-[350px]:text-sm" id="password" type="password" placeholder="Enter Your Password">
              <span v-if="!isPasswordValid" class="text-sm text-red-500">Password must be at least 8 characters</span>
           </div>

           <button :disabled="!isFormValid"  class="p-2 disabled:opacity-50 disabled:cursor-not-allowed mt-2 bg-red-600 hover:bg-red-800 cursor-pointer text-white font-bold rounded" type="submit">Submit</button>
         <!--write submit function at the form above @submit.prevent, not in the button. because a button iside a form
        will invariably cause submission of of the form without the need to write @click in it.-->

        </form>
    </div>
</template>

<script setup>
import {ref, computed} from 'vue'
const formData = ref({
    name: '',
    email: '',
    password: ''
})

const isNameValid = computed (() => formData.value.name.trim() !== '');
const isEmailValid = computed (() =>  /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(formData.value.email));
const isPasswordValid = computed (() => formData.value.password.length >= 8);

const isFormValid = computed (() => isNameValid.value && isEmailValid.value && isPasswordValid.value) //if these are true

const submitForm = () => {
    if (isFormValid.value) {
        console.log(formData.value)
    } else {
        console.log("please re-check the form fields and try again")
    }
}

</script>