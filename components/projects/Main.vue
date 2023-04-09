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
      @delete="deleteData"
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
        :project="project"
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
  console.log("form---->", form);
  const { data } = await useAuthLazyFetchPost(`${props.url}`, {
    body: {
      name: form.name,
      listing_type_name: form.type,
      category: "Residential",
      sub_category: "Apartment",
      status: form.status,
      details: form.details,
      specifications: form.specifications,
      possession_date: "2023-04-08",
      age_of_the_project: form.projectAge,
      logo_url: "string",
      total_project_area: form.totalProject,
      metric: "sq.ft",
      default_image_url: "string",
      visit_count: 0,
      rera_approved: true,
      approve_status: form.approveStatus,
    },
  });
  console.log("datat", data.value);
  projectsList.value.unshift(data.value);
  openAddForm.value = false;
};
const edit = async (project: any) => {
  console.log("Project-**->", project);
  await useAuthLazyFetchPut(`${props.url}${project.uid}?name=${project}`, {
    body: {
      name: project.name,
      listing_type_name: project.type,
      category: "Residential",
      sub_category: "Apartment",
      status: project.status,
      details: project.details,
      specifications: project.specifications,
      possession_date: "2023-04-08",
      age_of_the_project: project.projectAge,
      logo_url: "string",
      total_project_area: project.totalProject,
      metric: "sq.ft",
      default_image_url: "string",
      visit_count: 0,
      rera_approved: true,
      approve_status: project.approveStatus,
      },
     
  });
  openEditForm.value = false;
  getprojectsList();
};
const editData = (data: any) => {
  openEditForm.value = true;
  project.value = data;
  console.log(" data.value--->", data,project.value)
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
