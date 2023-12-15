<template>
  <div>
    <h1>Blog</h1>
    <ul>
      <li v-for="{ _path: slug, title } in blogPosts" :key="slug">
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
const { data: blogPosts } = await useAsyncData("blogPosts", () =>
  queryContent("/articles").find()
);
</script>
