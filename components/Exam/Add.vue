<template>
  <!-- Add Question Form Starts Here -->
  <div class="mt-2 pl-2">
    <label
      for="name"
      class="block text-sm font-medium leading-6 text-gray-900 mr-[31.75rem]"
      >Name:
    </label>
    <div class="mt-2">
      <input
        id="name"
        v-model="contact.name"
        class="pl-2 block rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        placeholder="Enter Name"
      />
    </div>
  </div>
 
  <div class="mt-2 pl-2">
    <label
      for="phone"
      class="block text-sm font-medium leading-6 text-gray-900 mr-[31.75rem]"
      >phone:
    </label>
    <div class="mt-2">
      <input
        type="number"
        id="phone"
        v-model="contact.phone"
        class="pl-2 block rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        placeholder="Enter Phone"
      />
    </div>
  </div>
  <div class="mt-2 pl-2">
    <label
      for="age"
      class="block text-sm font-medium leading-6 text-gray-900 mr-[31.75rem]"
      >Age:
    </label>
    <div class="mt-2">
      <input
        type="number"
        id="age"
        v-model="contact.age"
        class="pl-2 block rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        placeholder="Enter Phone"
      />
    </div>
  </div>
  <div class="mt-2 pl-2">
    <label
      for="email"
      class="block text-sm font-medium leading-6 text-gray-900 mr-[25.75rem]"
    >
      country:
    </label>
    <div class="mt-2">
      <input
        type="email"
        id="email"
        v-model="contact.country"
        class="pl-2 block rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        placeholder="Enter Email"
      />
    </div>
  </div>
  <div>
    <button
      type="reset"
      class="mr-1 rounded bg-white px-2 py-1 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50"
    >
      Cancel
    </button>
  </div>
  <div>
    <button
      type="submit"
      @click="emit('add', contact)"
      class="rounded bg-indigo-600 px-2 py-1 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
    >
      Save
    </button>
  </div>
  <!-- Add Question Form Ends Here -->
</template>
<script setup lang="ts">
// Define Emits
const emit = defineEmits(["add", "cancel"]);
const contact = ref({});
// On clicking on save button we emit form data to parent file

// On clicking on cancel button we will close Sidebar
const cancel = () => {
  emit("cancel");
};
</script>
