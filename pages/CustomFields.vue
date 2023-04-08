<template>
    <CustomFieldsMain :url="url" :geturl="geturl"></CustomFieldsMain>
</template>
<script setup lang="ts">
const url='https://v1-orm-lib.mars.hipso.cc/api/custom-fields/'
const geturl='https://v1-orm-lib.mars.hipso.cc/api/custom-fields/CONTACTS?offset=0&limit=100&sort_column=id&sort_direction=desc'
</script>