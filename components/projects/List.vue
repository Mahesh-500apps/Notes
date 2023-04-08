<template>
  
  <div class="px-4 sm:px-6 lg:px-8">
    <div class="mt-8 flow-root">
      <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
          <table class="min-w-full divide-y divide-gray-300">
            <thead>
              <tr>
                <th
                  scope="col"
                  class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-0"
                >
                  Name
                </th>
                <th
                  scope="col"
                  class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-0"
                >
                  Type
                </th>
                <th
                  scope="col"
                  class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                >
                  Description
                </th>
                <th
                  scope="col"
                  class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
                >
                  Placeholder
                </th>
                <th scope="col" class="relative py-3.5 pl-3 pr-4 sm:pr-0">
                  <span class="sr-only">Edit</span>
                </th>
              </tr>
            </thead>
            <tbody class="divide-y divide-gray-200">
              <tr v-for="(project, index) in projectsList" :key="index">
                <td
                  class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-0"
                >
                  {{ project.name }}
                </td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                  {{ project.listing_type_name }}
                </td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                  {{ project.status }}
                </td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                  {{ project.specifications }}
                </td>
                <td
                  class="relative whitespace-nowrap py-4 pl-3 pr-4 text-right text-sm font-medium sm:pr-0"
                >
                  <a href="#" class="text-indigo-600 hover:text-indigo-900">
                    <TrashIcon
                      class="h-5 w-5 sm:ml-[150px] sm:mb-[-20px] right-0"
                      @click="emit('delete', project,index)" /><span
                      class="sr-only"
                    ></span
                  ></a>
                </td>
                <td>
                  <div>
                    <a href="#" class="text-indigo-600 hover:text-indigo-900">
                      <PencilIcon
                        class="h-5 w-5 sm:ml-[150px] sm:mb-[-20px] right-0"
                        @click="emit('edit', project)" /><span
                        class="sr-only"
                      ></span
                    ></a>
                  </div>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { PencilIcon, TrashIcon } from "@heroicons/vue/24/outline";
const emit = defineEmits(["edit", "delete"]);
interface Projects {
  projectsList: { type: any; required: true };
}
const props = withDefaults(defineProps<Projects>(), {
  projectsList: {},
});
</script>
