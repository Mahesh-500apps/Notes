<template>
  <div>
    <button
      class="rounded bg-indigo-600 px-2 py-1 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
      @click="openAddForm = true"
    >
      Open Add Form
    </button>
    <ProjectsList
      :projectsList="projectsList"
      @edit="editData"
      @delete="deleteData()"
    />

    <div v-if="openAddForm">
      <ProjectsAdd
        v-if="openAddForm"
        :openAddForm="openAddForm"
        @add="addProject"
        @cancel="cancel"
      />
    </div>

    <div v-if="openEditForm">
      <ProjectsEdit
        v-if="openEditForm"
        :openEditForm="openEditForm"
        :Project="project"
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
const projectsList = ref([]);
const openAddForm = ref(false);
const openEditForm = ref(false);
const project = ref({});

// Get projectsList Data
const { data: Projects } = await useAuthLazyFetch(`${props.geturl}`, {});
projectsList.value = Projects.value;
console.log("projectsList--->", projectsList.value);

const addProject = async (form: any) => {
  console.log("form---->",form)
  const { data } = await useAuthLazyFetchPost(`${props.url}`, {
    body: {
      name: "sdasdasd",
      listing_type_name: "sadasda",
      category: "Residential",
      sub_category: "Apartment",
      status:"Fully Constructed" ,
      details: "ASdsad",
      specifications: "asdasdsad",
      possession_date: "2023-04-08",
      age_of_the_project: 0,
      logo_ur: "string",
      total_project_area: 0,
      metric: "sq/ft",
      default_image_url: "string",
      visit_count: 0,
      rera_approved: true,
      approve_status: "Active",
    },
  });
  console.log("datat",data.value);
  projectsList.value.unshift(data.value);
  openAddForm.value = false;
};
const edit = async (project: any) => {
  console.log("Project-**->", project);
  await useAuthLazyFetchPut(`${props.url}${project.uid}?name=${project}`, {
    body: {
      project_id: 1,
      name: form.Name,
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
  openEditForm.value = false;
  getprojectsList();
};
const editData = (data: any) => {
  console.log("dataaaa--->",data)
  openEditForm.value = true;
  project.value = data;
};
const cancel = () => {
  openAddForm.value = false;
  openEditForm.value = false;
};
// Delete Project from the list
const deleteData = async (project: any) => {
  console.log("Project--->", project);
  await useAuthLazyFetchDelete(`${props.url}${project.uid}`, {});
  // If the tag exists, delete it
  if (project.index !== -1) {
    // To remove deleted tag
    projectsList.value.splice(project.index, 1);
    getprojectsList();
  }
};
const getprojectsList = async () => {
  // Get tags from appconfig
  const { data: projectsList } = await useAuthLazyFetch(`${props.geturl}`, {});
  projectsList.value = projectsList.value;
};
</script>
