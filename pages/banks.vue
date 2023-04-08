<template>
    <QuestionMain :url="url" :geturl="geturl"></QuestionMain>
</template>
<script setup lang="ts">
const url='https://v7-stark-db-orm.mercury.infinity-api.net/api/question-bank/bulk'
const geturl='https://v7-stark-db-orm.mercury.infinity-api.net/api/question-bank/?offset=0&limit=100&sort_column=id&sort_direction=desc'
</script>
