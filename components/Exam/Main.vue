<template>
  <div
    class="block w-full p-4 bg-white border border-gray-200 rounded-lg shadow bg-gray-100 dark:bg-gray-800 dark:border-gray-700 dark:bg-gray-700 mt-2"
  >
    <div class="flex justify-end">
      <button
        type="button"
        class="rounded-full bg-indigo-600 p-4 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
        @click="openModal"
      >
        Add Student
      </button>
    </div>
    <ExamList
      v-if="contacts"
      :contacts="contacts"
      @emitData="emitData"
    />

  </div>

  <TransitionRoot appear :show="isOpen" as="template">
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
              </DialogTitle>
              <div>
                <ExamAdd  @add="add" @cancel="isOpen = false"></ExamAdd>
              </div>
              <div><ExamEdit @edit="edit" :contact="contact"></ExamEdit> </div>
            </DialogPanel>
          </TransitionChild>
        </div>
      </div>
    </Dialog>
  </TransitionRoot>
</template>

<script setup lang="ts">
import {
  TransitionRoot,
  TransitionChild,
  Dialog,
  DialogPanel,
  DialogTitle,
} from "@headlessui/vue";

const isOpen = ref(false);

function closeModal() {
  isOpen.value = false;
}
function openModal() {
  isOpen.value = true;
}

const contacts: any = ref([]);

onMounted(() => {
  contacts.value = JSON.parse(localStorage.getItem("contacts"));
  console.log("contacts.value-->", contacts.value);
});

const add = async (contact: any) => {
  contacts.value.push(contact);
  localStorage.setItem("contacts", JSON.stringify(contacts.value));
  getcontacts()
  isOpen.value = false;
};
// Edit notes
const edit = async (contact: any) => {
  contacts[contact.index] = contact;
  localStorage.setItem("contactDetails", JSON.stringify(contacts.value));
};
// Delete contacts
const deleteNote = async (note: any) => {
  contacts.value.splice(note.index, 1);
  localStorage.setItem("contactDetails", JSON.stringify(contacts.value));
};

// Edit and Delete events
const emitData = (contact: Object) => {
    contact.value == "edit" ? edit(contact) : deleteNote(contact);
};

// Get contacts
const getcontacts = async () => {
    contacts.value = JSON.parse(localStorage.getItem("contacts"));
};
</script>
