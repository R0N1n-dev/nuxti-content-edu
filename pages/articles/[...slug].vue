<template>
  <div>
    <button @click="router.go(-1)">Back</button>
    <ContentRenderer :value="blogPost" />
  </div>
</template>

<script setup>
const router = useRouter();
const route = useRoute();
const { data: blogPost } = await useAsyncData("blogPost", () =>
  queryContent("/articles").where({ _path: route.path }).findOne()
);
</script>
