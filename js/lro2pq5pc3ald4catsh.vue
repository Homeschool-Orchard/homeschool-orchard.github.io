<template>   <div>     <a :id="`basic-contact-form-${index}`"></a>     <div :class="colors.background" class="relative isolate px-6 py-24 sm:py-32 lg:px-8">       <div class="mx-auto max-w-2xl text-center">         <h2           v-if="settings.title"           :class="colors.text"           class="text-3xl font-bold tracking-tight sm:text-4xl"           v-text="settings.title"         />         <p           v-if="settings.content"           :class="colors.text_light"           class="mt-2 text-lg leading-8"           v-text="settings.content"         />       </div>        <form @submit.prevent="handleSubmit" id="my-form" class="mx-auto mt-16 max-w-xl sm:mt-20">         <div class="grid grid-cols-1 gap-x-8 gap-y-6 sm:grid-cols-2">           <div class="sm:col-span-2">
<label for="name" :class="colors.text" class="block text-sm font-semibold leading-6">Name <span class="text-red-600">*</span></label>
<div class="mt-2.5">
  <input v-model="formData.name" type="text" name="name" required autocomplete="given-name" class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset sm:text-sm sm:leading-6">
</div>           </div>           <div class="sm:col-span-2">
<label for="email" :class="colors.text" class="block text-sm font-semibold leading-6">Email <span class="text-red-600">*</span></label>
<div class="mt-2.5">
  <input v-model="formData.email" type="email" required name="email" autocomplete="email" class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset sm:text-sm sm:leading-6">
</div>           </div>             </div>          <div v-if="errors.length" class="rounded-md bg-red-50 p-4 mx-auto max-w-xl mt-10">           <div class="flex">
<div class="flex-shrink-0">
  <svg class="h-5 w-5 text-red-400" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
    <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.28 7.22a.75.75 0 00-1.06 1.06L8.94 10l-1.72 1.72a.75.75 0 101.06 1.06L10 11.06l1.72 1.72a.75.75 0 101.06-1.06L11.06 10l1.72-1.72a.75.75 0 00-1.06-1.06L10 8.94 8.28 7.22z" clip-rule="evenodd" />
  </svg>
</div>
<div class="ml-3">
  <h3 v-if="errors.length > 1" class="text-sm font-medium text-red-800">There were 2 errors with your submission</h3>
  <h3 v-else class="text-sm font-medium text-red-800">There was an error with your submission</h3>
  <div class="mt-2 text-sm text-red-700">
    <ul role="list" class="list-disc space-y-1 pl-5">
      <li v-for="(error, index) in errors" :key="index" v-text="error" />
    </ul>
  </div>
</div>
<div class="ml-auto pl-3">
  <div class="-mx-1.5 -my-1.5">
    <button @click="errors = []" type="button" class="inline-flex rounded-md bg-red-50 p-1.5 text-red-400 hover:bg-red-100 focus:outline-none focus:ring-2 focus:ring-offset-2">
      <span class="sr-only">Dismiss</span>
      <svg class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
        <path d="M6.28 5.22a.75.75 0 00-1.06 1.06L8.94 10l-3.72 3.72a.75.75 0 101.06 1.06L10 11.06l3.72 3.72a.75.75 0 101.06-1.06L11.06 10l3.72-3.72a.75.75 0 00-1.06-1.06L10 8.94 6.28 5.22z" />
      </svg>
    </button>
  </div>
</div>           </div>         </div>          <div v-else-if="success" class="rounded-md bg-green-50 p-4 mx-auto max-w-xl mt-10">           <div class="flex">
<div class="flex-shrink-0">
  <svg class="h-5 w-5 text-green-400" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
    <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.857-9.809a.75.75 0 00-1.214-.882l-3.483 4.79-1.88-1.88a.75.75 0 10-1.06 1.061l2.5 2.5a.75.75 0 001.137-.089l4-5.5z" clip-rule="evenodd" />
  </svg>
</div>
<div class="ml-3">
  <p class="text-sm font-medium text-green-800">Your form submission has been successfully received. Thank you!</p>
</div>
<div class="ml-auto pl-3">
  <div class="-mx-1.5 -my-1.5">
    <button @click="success = false" type="button" class="inline-flex rounded-md bg-green-50 p-1.5 text-green-500 hover:bg-green-100 focus:outline-none focus:ring-2 focus:ring-green-600 focus:ring-offset-2 focus:ring-offset-green-50">
      <span class="sr-only">Dismiss</span>
      <svg class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
        <path d="M6.28 5.22a.75.75 0 00-1.06 1.06L8.94 10l-3.72 3.72a.75.75 0 101.06 1.06L10 11.06l3.72 3.72a.75.75 0 101.06-1.06L11.06 10l3.72-3.72a.75.75 0 00-1.06-1.06L10 8.94 6.28 5.22z" />
      </svg>
    </button>
  </div>
</div>           </div>         </div>           <div class="mt-10">           <input type="hidden" name="hidden" v-model="hiddenValue">           <button
v-if="settings.button_text"
type="submit"
:style="[
  {'background-color': settings.button_background},
  {'color': settings.button_text_color}
]"
class="block w-full rounded-md px-3.5 py-2.5 text-center text-sm font-semibold shadow-sm focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2"
v-text="settings.button_text"           />         </div>       </form>     </div>   </div> </template><script> export default {   props: {     index: {       type: Number,       default: 0     },     schema: {       type: Object,       default: () => ({})     },     site: {       type: Object,       default: () => ({})     }   },    data() {     return {       errors: [],       hiddenValue: null,       success: false,       firstname: null,       lastname: null,       formData: {         name: null,         email: null,         phone: null,         subject: null,         message: null,         siteId: this.site.id       }     }   },    computed: {     settings() {       const data = {};        this.schema.settings?.forEach((setting) => {         data[setting.id] = setting.value;       });        return data;     },      colors() {       return themeColors(this.settings.theme);     }   },    methods: {     async handleSubmit() {       if (this.hiddenValue) {         this.errors.push('Failed to submit form. Please try again or contact the site administrator.');         return;       }
const form = document.getElementById('my-form');       const formData = new FormData(form); 
 const response = await fetch("https://script.google.com/macros/s/AKfycbwobbmIGOod3lCi7nxXgR0CaEO4pAhI0DbXMyGwwUnuJKQ2asJyOcD5M99ISQXVNTWz/exec" , 
  {     
  method: 'POST',         
  body: formData       });        const result = await response.json(); 
  console.log(result);
  if (result.result == 'success') {         this.success = true;         this.errors = [];         return;       }        Object.values(result.errors).forEach((error) => {         this.errors.push(error);       });       this.success = false;     }   } } </script><style></style>
