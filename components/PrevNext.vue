<script setup>
// import icons
// define prev and next props
defineProps(["prev", "next"]);
</script>
<template>
  <ul class="prev-next-cont">
    <li class="link-item prev">
      <NuxtLink v-if="prev" :to="prev._path">
        <span> {{ prev.title }} </span>
      </NuxtLink>
    </li>
    <li class="link-item next">
      <NuxtLink v-if="next" :to="next._path">
        <span> {{ next.title }} </span>
      </NuxtLink>
    </li>
  </ul>
</template>
<style scoped>
/* ... */
</style>
