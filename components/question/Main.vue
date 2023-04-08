<template>
  <div>
    <button
      class="rounded bg-indigo-600 px-2 py-1 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
      @click="openAddForm = true"
    >
      Open Add Form
    </button>
    <QuestionList
      :questionsList="questionsList"
      @edit="editData"
      @delete="deleteData()"
    />

    <div v-if="openAddForm">
      <QuestionAdd
        v-if="openAddForm"
        :openAddQuestionForm="openAddForm"
        @add="addQuestion"
        @edit="edit"
        @cancel="cancel"
      />
    </div>

    <div v-if="openViewForm">
      <QuestionEdit
        v-if="openViewForm"
        :openViewSidebar="openViewForm"
        :question="question"
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
const questionsList = ref([]);
const openAddForm = ref(false);
const openViewForm = ref(false);
const question = ref({});

// Get Questions Data
const { data: questions } = await useAuthLazyFetch(`${props.geturl}`, {});
questionsList.value = questions.value;

const addQuestion = async (form: any) => {
  const postoptions = {
    body: [form],
  };
  const { data } = await useAuthLazyFetchPost(`${props.url}`, postoptions);
  console.log("data-->",data)
  questionsList.value.unshift(data.value);
  openAddForm.value=false
};
const edit = async (question: any) => {
  const postoptions = {
    body: [question],
  };
  await useAuthLazyFetchPut(
    `${props.url}${question.uid}?name=${question}`,
    postoptions
  );
  openViewForm.value = true;
};
const editData = (data: any) => {
  openViewForm.value = true;
  question.value = data;
};
const cancel = () => {
  openAddForm.value = false;
  openViewForm.value = false;
};
// Delete Question from the list
const deleteData = async (question: any) => {
  await useAuthLazyFetchDelete(`${props.url}${question.uid}`, {});
  // If the tag exists, delete it
  if (question.index !== -1) {
    // To remove deleted tag
    questions.value.splice(question.index, 1);
    getQuestions();
  }
};
const getQuestions = async () => {
  // Get tags from appconfig
  const { data: questions } = await useAuthLazyFetch(`${props.geturl}`, {});
  questionsList.value = questions.value;
};
</script>
