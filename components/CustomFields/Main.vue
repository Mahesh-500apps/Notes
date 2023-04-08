<template>
  <div>
    <button
      class="rounded bg-indigo-600 px-2 py-1 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
      @click="openAddForm = true"
    >
      Open Add Form
    </button>
    <CustomFieldsList
      :customFieldsList="customFieldsList"
      @edit="editData"
      @delete="deleteData()"
    />

    <div v-if="openAddForm">
      <CustomFieldsAdd
        v-if="openAddForm"
        :openAddForm="openAddForm"
        @add="addcustomField"
        @cancel="cancel"
      />
    </div>

    <div v-if="openEditForm">
      <CustomFieldsEdit
        v-if="openEditForm"
        :openEditForm="openEditForm"
        :customField="customField"
        @save="edit"
        @cancel="cancel"
      />
    </div>
  </div>
</template>
<script setup lang="ts">
interface Collection {
  url: String;
  geturl: String;
}
const props = withDefaults(defineProps<Collection>(), {
  url: "",
  geturl: "",
});
const customFieldsList = ref([]);
const openAddForm = ref(false);
const openEditForm = ref(false);
const customField = ref({});

// Get customFieldsList Data
const { data: customFields } = await useAuthLazyFetch(`${props.geturl}`, {});
console.log("customFields--->", customFields.value);
customFieldsList.value = customFields.value;
console.log("customFieldsList--->", customFieldsList.value);

const addcustomField = async (form: any) => {
  const { data } = await useAuthLazyFetchPost(`${props.url}`, {
    body: {
      project_id: 1,
      name: form.name,
      entity: "CONTACTS",
      type_data: {
        is_required: 1,
        show_in_filter: 1,
        length: 100,
        description: form.description,
        placeholder: form.placeholder,
      },
      type: form.type,
      role_id: 1,
    },
  });
  console.log(data.value);
  customFieldsList.value.unshift(data.value);
  openAddForm.value = false;
};
const edit = async (customField: any) => {
  console.log("customField-->",customField)
  await useAuthLazyFetchPut(
    `${props.url}${customField.uid}?name=${customField}`,
    {
      body: {
        project_id: 1,
        name: customField.name,
        entity: "CONTACTS",
        type_data: {
          is_required: 1,
          show_in_filter: 1,
          length: 100,
          description: customField.type_data.description,
          placeholder: customField.type_data.placeholder,
        },
        type: customField.type,
        role_id: 1,
      },
    }
  );
  openEditForm.value = false;
};
const editData = (data: any) => {
  console.log("data--->", data);
  openEditForm.value = true;
  customField.value = data;
  console.log("customField-->", customField.value);
};
const cancel = () => {
  openAddForm.value = false;
  openEditForm.value = false;
};
// Delete customField from the list
const deleteData = async (customField: any) => {
  console.log("customField--->",customField)
  await useAuthLazyFetchDelete(`${props.url}${customField.uid}`, {});
  // If the tag exists, delete it
  if (customField.index !== -1) {
    // To remove deleted tag
    customFieldsList.value.splice(customField.index, 1);
    getcustomFieldsList();
  }
};
const getcustomFieldsList = async () => {
  // Get tags from appconfig
  const { data: customFieldsList } = await useAuthLazyFetch(
    `${props.geturl}`,
    {}
  );
  customFieldsList.value = customFieldsList.value;
};
</script>
