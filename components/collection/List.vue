<template>
  <div>
    <PencilIcon
      class="h-5 w-5 sm:ml-[120px] sm:mb-[-20px] right-0"
      @click="emitData(note, 'edit')"
    />
    <TrashIcon
      class="h-5 w-5 sm:ml-[150px] sm:mb-[-20px] right-0"
      @click="emitData(note, 'delete')"
    />
  </div>
  <div class="relative mt-8 flex items-center gap-x-4">
    <div class="text-sm leading-6 group">
      <!--Notes body-->
      <span class="text-gray-600">{{ note.note }}</span>
    </div>
  </div>
</template>


<script setup lang="ts">
import { PencilIcon, TrashIcon } from "@heroicons/vue/24/outline";
const emit = defineEmits(["emitData"]);
const props = defineProps({
  note: { type: Object, required: true },
  index: { type: Number, required: true },
});


const emitData = (note: any, value: any) => {
  emit("emitData", { note: note, value: value, index: props.index });
};
</script>
