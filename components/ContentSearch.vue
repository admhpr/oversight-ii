<script setup lang="ts">
import type { ParsedContent } from '@nuxt/content/dist/runtime/types';

const props = defineProps({
  path: {
    type: String,
    required: true,
  },
});

const search = ref('')
const content = ref([]) as Ref<Pick<ParsedContent, string>[]>
onMounted(async () => {
  content.value = await getSearchContent(props.path)
})

async function getSearchContent(path: string) {
  const result = await queryContent(path).only(["title", "description", "tags", "body"]).find()
  return result
}
</script>
<template>
  <input v-model="search">
  {{JSON.stringify(content)}}
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
