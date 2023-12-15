<!--<template>
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
</script>-->

<template>
  <div>
    <button @click="router.go(-1)">Back</button>
    <PrevNext :prev="prev" :next="next" />
    <ContentRenderer :value="data">
      <ContentRendererMarkdown :value="data" />
    </ContentRenderer>
  </div>
</template>

<script setup>
const router = useRouter();
const route = useRoute();
const { data } = await useAsyncData(`content-${route.path}`, async () => {
  // fetch document where the document path matches with the cuurent route
  let article = queryContent().where({ _path: route.path }).findOne();
  // get the surround information,
  // which is an array of documeents that come before and after the current document
  let surround = queryContent()
    .only(["_path", "title", "description"])
    .sort({ date: 1 })
    .findSurround(route.fullPath);

  return {
    article: await article,
    surround: await surround,
  };
});

// destrucure `prev` and `next` value from data
const [prev, next] = data.value.surround;
</script>
