<template>
    <ProjectsMain :url="url" :geturl="geturl"></ProjectsMain>
</template>
<script setup lang="ts">
const url='https://v1-orm-gharpe.mercury.infinity-api.net/api/projects/'
const geturl='https://v1-orm-gharpe.mercury.infinity-api.net/api/projects/?offset=0&limit=100&sort_column=id&sort_direction=desc'
</script>