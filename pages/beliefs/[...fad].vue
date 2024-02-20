<template>
  <div>
    <button @click="router.go(-1)">Back</button>
    <button @click="router.push('/beliefs')">Beliefs</button>
    <PrevNext :prev="prev" :next="next" />
    <ContentRenderer :value="data.belief">
      <h1>{{ data.belief.title }}</h1>
      <ContentRendererMarkdown :value="data.belief" />
    </ContentRenderer>
  </div>
</template>

<script setup>
const router = useRouter();
const route = useRoute();
const { data } = await useAsyncData(`content-${route.path}`, async () => {
  // fetch document where the document path matches with the cuurent route
  let belief = queryContent().where({ _path: route.path }).findOne();
  // get the surround information,
  // which is an array of documeents that come before and after the current document
  let surround = queryContent()
    .only(["_path", "title", "description"])
    .sort({ date: 1 })
    .findSurround(route.fullPath);

  return {
    belief: await belief,
    surround: await surround,
  };
});

// destrucure `prev` and `next` value from data
const [prev, next] = data.value.surround;
console.log(prev, next);
</script>
