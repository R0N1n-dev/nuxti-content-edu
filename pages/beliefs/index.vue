<template>
  <div>
    <h1>Beliefs</h1>
    <ul>
      <li v-for="{ _path: fad, title } in beliefs" :key="fad">
        <NuxtLink :to="fad">{{ title }}</NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script setup>
/*const blogPosts = await queryContent("/articles")
    .sort({ date: -1 }) // show latest articles first
    .where({ _partial: false }) // exclude the Partial files
    .find();*/
const { data: beliefs } = await useAsyncData("beliefs", () =>
  queryContent("/beliefs").find()
);
</script>
