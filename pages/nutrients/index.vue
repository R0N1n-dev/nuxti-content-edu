<template>
  <div>
    <h1>Nutrients</h1>
    <ul>
      <li v-for="{ _path: slug, title } in nutrients" :key="slug">
        <NuxtLink :to="slug">{{ title }}</NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script setup>
/*const blogPosts = await queryContent("/articles")
  .sort({ date: -1 }) // show latest articles first
  .where({ _partial: false }) // exclude the Partial files
  .find();*/
const { data: nutrients } = await useAsyncData("nutrients", () =>
  queryContent("/nutrients").find()
);
</script>
