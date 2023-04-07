<template>
  <div>
    <div v-if="isEdit">
      <PartnersEdit :partner="editInput" @edit="edit" />
    </div>
    <PartnersList
      :partners="partners"
      @edit="editData"
      @delete="deleteData()"
    ></PartnersList>

    <div v-if="addPartner" class="block justify-end">
      <PartnersAdd @add="add"></PartnersAdd>
    </div>

    <button
      type="button"
      class="block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
      @click="addPartner = true"
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
partners.value = formData.value;

// To prepare an object that each key has an array of tags based on their initial letters
const editInput = ref({});
const isEdit = ref(false);

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
  getPartners();
};
const editData = (partner: Object) => {
  editInput.value = partner;
  isEdit.value=true
};
// Delete tags
const deleteData = async (partner: any) => {
  await useAuthLazyFetchDelete(`${props.url}${partner.uid}`, {});
  // If the tag exists, delete it
  if (partner.index !== -1) {
    // To remove deleted tag
    partners.value.splice(partner.index, 1);
    getPartners();
  }
};
// Edit tags
const edit = async (partner: any) => {
  await useAuthLazyFetchPut(`${props.url}${partner.uid}?name=${partner}`, {
    body: {
      category: partner.category,
      industry: partner.industry,
      name: partner.name,
      email: partner.email,
      rating: 0,
      type: "Partner",
      address: {
        street: partner.street,
        city: partner.city,
        state: partner.state,
        country: partner.country,
        zip_code: partner.code,
      },
      website: "www.google.com",
      status: 1,
      profile_id: 1,
    },
  });
  isEdit.value=false
};

const getPartners = async () => {
  // Get tags from appconfig
  const { data: partnersdata } = await useAuthLazyFetch(`${props.geturl}`, {});
  partners.value = partnersdata.value;
};
</script>
