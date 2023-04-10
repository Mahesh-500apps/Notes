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
              emit('emitData', { note: note, value: 'delete', index: index })
            "
          />

          <PencilIcon
            class="h-5 w-5 sm:ml-[150px] sm:mb-[-20px] right-0"
            @click="
              emit('emitData', { note: note, value: 'edit', index: index })
            "
          />
        </div>
        <div class="px-6 py-4">
          <div class="font-bold text-xl mb-2">NAME: {{ contact.name }}</div>
          <p class="text-gray-700 text-base">Phone: {{ contact.phone }}</p>
          <p> country: {{ contact.phone }}</p>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
import { PencilIcon, TrashIcon } from "@heroicons/vue/24/outline";
const emit = defineEmits(["emitData"]);

const props = defineProps({
  contacts: { type: Object, required: true },
});
</script>
