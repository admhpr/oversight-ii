<script setup lang="ts">
const props = defineProps({
  path: {
    type: String,
    required: true,
  },
});
function onInput({target: {value}}){
    console.log('onInput', value)
}
</script>
<template>
  <input @input="onInput">
  <ContentQuery :path="props.path">
    <template #default="{ data }">
      <ul>
        {{JSON.stringify(data)}}
        <!-- <li v-for="author of data" :key="author.name">
          {{ author.name }}
        </li> -->
      </ul>
    </template>
    <template #not-found>
      <p>No authors found.</p>
    </template>
  </ContentQuery>
</template>

<style scoped></style>
