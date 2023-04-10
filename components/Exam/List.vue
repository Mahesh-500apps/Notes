<template>
  <div>
    <div
      class="grid grid-cols-1 border-b border-gray-200 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4"
    >
      <div v-for="(contact, index) in contacts" :key="index">
        <div class="flex">
          <TrashIcon
            class="h-5 w-5 sm:ml-[150px] sm:mb-[-20px] right-0"
            @click="
              emitData(contact, index, 'delete')
            "
          />

          <PencilIcon
            class="h-5 w-5 sm:ml-[150px] sm:mb-[-20px] right-0"
            @click="emitData(contact, index, 'edit')"
          />
        </div>
        <div class="px-6 py-4">
          <div class="font-bold text-xl mb-2">NAME: {{ contact.name }}</div>
          <p class="text-gray-700 text-base">Phone: {{ contact.phone }}</p>
          <p>country: {{ contact.phone }}</p>
        </div>
      </div>
    </div>
    <TransitionRoot appear :show="openModal" as="template">
      <Dialog as="div" @close="closeModal" class="relative z-10">
        <TransitionChild
          as="template"
          enter="duration-300 ease-out"
          enter-from="opacity-0"
          enter-to="opacity-100"
          leave="duration-200 ease-in"
          leave-from="opacity-100"
          leave-to="opacity-0"
        >
          <div class="fixed inset-0 bg-black bg-opacity-25" />
        </TransitionChild>

        <div class="fixed inset-0 overflow-y-auto">
          <div
            class="flex min-h-full items-center justify-center p-4 text-center"
          >
            <TransitionChild
              as="template"
              enter="duration-300 ease-out"
              enter-from="opacity-0 scale-95"
              enter-to="opacity-100 scale-100"
              leave="duration-200 ease-in"
              leave-from="opacity-100 scale-100"
              leave-to="opacity-0 scale-95"
            >
              <DialogPanel
                class="w-full max-w-md transform overflow-hidden rounded-2xl bg-white p-6 text-left align-middle shadow-xl transition-all"
              >
                <DialogTitle
                  as="h3"
                  class="text-lg font-medium leading-6 text-gray-900"
                >
                  {{ edit ? "Edit" : "Delete" }}
                </DialogTitle>

                <div v-if="edit">
                  <ExamEdit
                    :contact="editContact"
                    @edit="
                      (openModal = false),
                        (edit = false),
                        emit('emitData', {
                          note: $event,
                          value: 'edit',
                          index: editIndex,
                        })
                    "
                    @cancel="closeModal"
                  />
                </div>
                <div v-if="deleteContact">
                  <p>do you want to delete?</p>
                  <div class="mt-10 flex">
                    <button
                      type="submit"
                      @click="
                        (openModal = false),
                          emit('emitData', {
                            note: $event,
                            value: 'delete',
                            index: editIndex,
                          })
                      "
                      class="block mr-2 rounded-md bg-indigo-600 px-3.5 py-2.5 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                    >
                      yes
                    </button>

                    <button
                      type="submit"
                      @click="closeModal"
                      class="block rounded-md bg-indigo-600 px-3.5 py-2.5 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                    >
                      no
                    </button>
                  </div>
                </div>
              </DialogPanel>
            </TransitionChild>
          </div>
        </div>
      </Dialog>
    </TransitionRoot>
  </div>
</template>
<script setup>
import {
  TransitionChild,
  DialogPanel,
  TransitionRoot,
  Dialog,
} from "@headlessui/vue";

import { TrashIcon, PencilIcon } from "@heroicons/vue/24/outline";
const fields = ref([
  "s_no",
  "name",
  "age",
  "gender",
  "date_of_birth",
  "designation",
]);
const props = defineProps({
  contacts: { type: Object, required: true },
});
const emit = defineEmits(["emitData"]);
const editContact = ref({});
const editIndex = ref(-1);
const edit = ref(false);

const deleteContact = ref(false);

const openModal = ref(false);

const emitData = (contact, index,value) => {
  openModal.value = true;
  editIndex.value = index;
  editContact.value =contact;
  if (value == "edit") {
    edit.value = true;
  } else {
    deleteContact.value = true;
  }
};
const closeModal = () => {
  openModal.value = false;
  edit.value = false;
  deletecontact.value = false;
};
</script>
