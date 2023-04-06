<template>
  <PartnersMain :geturl=getUrl :url=url ></PartnersMain>
</template>
<script setup lang="ts">
const getUrl =
  "https://v1-orm-gharpe.mercury.infinity-api.net/api/partners/?offset=0&limit=100&sort_column=id&sort_direction=desc";

const url = "https://v1-orm-gharpe.mercury.infinity-api.net/api/partners/";
</script>
