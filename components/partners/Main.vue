<template>
  <div>
    <PartnersList :partners="partners" @emitdata="emitData"></PartnersList>

    <div v-if="addPartner" class="block justify-end">
      <PartnersAdd @add="add"></PartnersAdd>
    </div>
    <button
      type="button"
      class="block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
      @click="addPartner=true"
    >
      Add partner
    </button>
  </div>
</template>
<script setup lang="ts">


interface CollectionForm {
  url: String;
  geturl: String;
}
const props = withDefaults(defineProps<CollectionForm>(), {
  url: "",
  geturl: "",
});
const addPartner = ref(false);
const open = ref(true);
const partners = ref([]);
// Get tags from appconfig
const { data: formData } = await useAuthLazyFetch(`${props.geturl}`, {});
console.log("tagsData--->", formData);
partners.value = formData.value;
console.log("tags-->", partners.value);

// To prepare an object that each key has an array of tags based on their initial letters
const editInput = ref([]);

const isOpen = ref(false);

const add = async (form: any) => {
  const { data } = await useAuthLazyFetchPost(
    `${props.url}`,
    {
      body: {
        category: form.category,
        industry: form.industry,
        name: form.name,
        email: form.email,
        rating: 0,
        type: "Partner",
        address: {
          street: form.street,
          city: form.city,
          state: form.state,
          country: form.country,
          zip_code: form.code,
        },
        website: "www.google.com",
        status: 1,
        profile_id: 1,
      },
    }
    // Add the new tag to the tags
  );
  partners.value.unshift(data.value);
  getTags();
};
const emitData = (tag: Object) => {
  tag.value == "edit" ? (editInput.value = tag.tag) : deleteTag(tag);
  console.log("editIn23put", editInput);
};
// Delete tags
const deleteTag = async (tag: any) => {
  await useAuthLazyFetchDelete(`${props.url}${tag.tag.uid}`, {});
  // If the tag exists, delete it
  if (tag.index !== -1) {
    // To remove deleted tag
    partners.value.splice(tag.index, 1);
    getTags();
  }
};
// Edit tags
const edit = async (tag: any) => {
  await useAuthLazyFetchPut(`${props.url}${tag.uid}?name=${tag.tag}`, {
    body: {
      project_id: props.project_id,
      name: tag.tag,
      entity: props.entity,
    },
  });
};
// Split ids and name and mapping into single object
const transformTags = (tag: any) => {
  let tag_data = tag.name.split(",");
  let tag_ids = tag.uid.split(",");
  return tag_data.map((name, id) => {
    return { name: name, tag_id: tag_ids[id] };
  });
};
const getTags = async () => {
  // Get tags from appconfig
  const { data: partnersdata } = await useAuthLazyFetch(`${props.geturl}`, {});
  partners.value = partnersdata.value;
  editInput.value = tags.value;
};
</script>
