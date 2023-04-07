<template>
  <form>
    <div class="space-y-12">
      <div
        class="grid grid-cols-1 gap-x-8 gap-y-10 border-b border-gray-900/10 pb-12 md:grid-cols-3"
      >
        <div
          class="grid max-w-2xl grid-cols-1 gap-x-6 gap-y-8 sm:grid-cols-6 md:col-span-2"
        >
          <div class="sm:col-span-3">
            <label
              for="first-name"
              class="block text-sm font-medium leading-6 text-gray-900"
              >Category</label
            >
            <div class="mt-2">
              <input
                type="text"
                name="first-name"
                v-model="form.category"
                id="first-name"
                autocomplete="given-name"
                class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
              />
            </div>
          </div>

          <div class="sm:col-span-3">
            <label
              for="last-name"
              class="block text-sm font-medium leading-6 text-gray-900"
              >industry</label
            >
            <div class="mt-2">
              <input
                type="text"
                name="last-name"
                v-model="form.industry"
                id="last-name"
                autocomplete="family-name"
                class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
              />
            </div>
          </div>

          <div class="sm:col-span-4">
            <label
              for="name"
              class="block text-sm font-medium leading-6 text-gray-900"
              >Name</label
            >
            <div class="mt-2">
              <input
                id="name"
                name="name"
                v-model="form.name"
                type="name"
                autocomplete="email"
                class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
              />
            </div>
          </div>

          <div class="sm:col-span-4">
            <label
              for="email"
              class="block text-sm font-medium leading-6 text-gray-900"
              >Email address</label
            >
            <div class="mt-2">
              <input
                id="email"
                name="email"
                v-model="form.email"
                type="email"
                autocomplete="email"
                class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
              />
            </div>
          </div>

          <div class="sm:col-span-3">
            <label
              for="country"
              class="block text-sm font-medium leading-6 text-gray-900"
              >Country</label
            >
            <div class="mt-2">
              <select
                id="country"
                name="country"
                autocomplete="country-name"
                v-model="form.country"
                class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:max-w-xs sm:text-sm sm:leading-6"
              >
                <option>United States</option>
                <option>Canada</option>
                <option>Mexico</option>
              </select>
            </div>
          </div>

          <div class="col-span-full">
            <label
              for="street-address"
              class="block text-sm font-medium leading-6 text-gray-900"
              >Street address</label
            >
            <div class="mt-2">
              <input
                type="text"
                name="street-address"
                id="street-address"
                v-model="form.street"
                autocomplete="street-address"
                class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
              />
            </div>
          </div>

          <div class="sm:col-span-2 sm:col-start-1">
            <label
              for="city"
              class="block text-sm font-medium leading-6 text-gray-900"
              >City</label
            >
            <div class="mt-2">
              <input
                type="text"
                name="city"
                v-model="form.city"
                id="city"
                autocomplete="address-level2"
                class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
              />
            </div>
          </div>

          <div class="sm:col-span-2">
            <label
              for="region"
              class="block text-sm font-medium leading-6 text-gray-900"
              >State / Province</label
            >
            <div class="mt-2">
              <input
                type="text"
                name="region"
                id="region"
                v-model="form.state"
                autocomplete="address-level1"
                class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
              />
            </div>
          </div>

          <div class="sm:col-span-2">
            <label
              for="postal-code"
              class="block text-sm font-medium leading-6 text-gray-900"
              >ZIP / Postal code</label
            >
            <div class="mt-2">
              <input
                type="text"
                name="postal-code"
                id="postal-code"
                v-model="form.code"
                autocomplete="postal-code"
                class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="mt-6 flex items-center justify-end gap-x-6">
      <button
        type="button"
        class="text-sm font-semibold leading-6 text-gray-900"
      >
        Cancel
      </button>
      <button
        type="submit"
        class="rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        @click="emit('edit',form)"
      >
        Save
      </button>
    </div>
  </form>
</template>
<script setup lang="ts">
const props = defineProps({
  partner: { type: Object, required: true }, // Edited note
});
const emit = defineEmits(["edit"]);
const note = ref("");
console.log("partner--->",props.partner.name)
const form = ref({
  name: props.partner.name,
  email: props.partner.email,
  category: props.partner.category,
  industry: props.partner.industry,
  street: props.partner.address.street,
  city: props.partner.address.street,
  state: props.partner.address.state,
  country: props.partner.address.country,
  code: props.partner.address.code,
});

// const add = () => {
//   console.log("form--->", form.value);
//   emit("add", form.value);
//   form.value = {};
// };
</script>
