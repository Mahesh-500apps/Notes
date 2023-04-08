<template>
  <!-- Add Question Form Starts Here -->
  <TransitionRoot as="template" :show="openAddForm">
    <Dialog as="div" class="relative z-10" @close="openAddForm = false">
      <div class="fixed inset-0 overflow-hidden">
        <div class="absolute inset-0 overflow-hidden">
          <div
            class="pointer-events-none fixed inset-y-0 right-0 flex max-w-full pl-10"
          >
            <TransitionChild
              as="template"
              enter="transform transition ease-in-out duration-500 sm:duration-700"
              enter-from="translate-x-full"
              enter-to="translate-x-0"
              leave="transform transition ease-in-out duration-500 sm:duration-700"
              leave-from="translate-x-0"
              leave-to="translate-x-full"
            >
              <DialogPanel class="pointer-events-auto w-screen max-w-md">
                <div
                  class="flex h-full flex-col overflow-y-scroll bg-white py-6 shadow-xl"
                >
                  <div class="px-4 sm:px-6">
                    <div class="flex items-start justify-between">
                      <DialogTitle
                        class="text-base font-semibold leading-6 text-gray-900"
                        >Add Question</DialogTitle
                      >
                      <div class="ml-3 flex h-7 items-center">
                        <button
                          type="button"
                          class="rounded-md bg-white text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
                          @click="openAddForm = false"
                        >
                          <span class="sr-only">Close panel</span>
                          <XMarkIcon class="h-6 w-6" aria-hidden="true" />
                        </button>
                      </div>
                    </div>
                  </div>
                  <!-- Data is taken from the user through input fields -->
                  <form @submit.prevent="saveFormData" @reset.prevent="cancel">
                    <div>
                      <label />Name
                      <input
                        v-model="form.name"
                        type="text"
                        class="block mb-3 px-3 rounded-md border-0 py-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                      />
                      <label for="test-type">Type</label>
                      <select
                        v-model="form.type"
                        class="block mb-3 px-3 rounded-md border-0 py-3 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:text-sm sm:leading-6 w-[100%]"
                      >
                        <option selected value="">Please select Type</option>
                        <option value="TEXTBOX">TEXTBOX</option>
                        <option value="RADIO_BUTTONS">RADIO_BUTTONS</option>
                        <option value="MULTI_CHECKBOX">MULTI_CHECKBOX</option>
                        <option value="LIST">LIST</option>
                        <option value="DATEFIELD">DATEFIELD</option>
                        <option value="NUMBER">NUMBER</option>
                      </select>

                      <label />Description
                      <textarea
                        v-model="form.description"
                        type="text"
                        class="p-4 mb-3 block w-full rounded-md border-0 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:py-1.5 sm:text-sm sm:leading-6"
                      />
                      <label />Placeholder
                      <input
                        v-model="form.placeholder"
                        type="text"
                        class="p-4 block w-full rounded-md border-0 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-300 sm:py-1.5 sm:text-sm sm:leading-6"
                      />
                    </div>

                    <button
                      type="button"
                      class="text-sm font-semibold leading-6 text-gray-900"
                    >
                      Cancel
                    </button>
                    <button
                      type="submit"
                      class="rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                      @click="save"
                    >
                      Save
                    </button>
                  </form>
                </div>
              </DialogPanel>
            </TransitionChild>
          </div>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
  <!-- Add Question Form Ends Here -->
</template>
<script setup lang="ts">
import {
  Dialog,
  DialogPanel,
  DialogTitle,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";
import { XMarkIcon } from "@heroicons/vue/24/outline";
// Define Props
interface Question {
  openAddForm: Boolean;
}
const props = withDefaults(defineProps<Question>(), {
  openAddForm: {},
});

// Define Emits
const emit = defineEmits(["add", "cancel"]);
const form = ref({
  name: "",
  type: "",
  description: "",
  placeholder: "",
});
// On clicking on save button we emit form data to parent file
const save = () => {
  console.log("form.value---->", form.value);
  emit("add", form.value);
  form.value = {};
};
// On clicking on cancel button we will close Sidebar
const cancel = () => {
  emit("cancel");
};
</script>
