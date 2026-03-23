<template>
  <div>
    <SloganMain/>
    <OffersMain/>
    <AboutMain/>
    <UpcomingMain/>
    <BlogMain/>
    <ContactsMain/>
   
  </div>
</template>

<script setup>
 const list = ref([]);

  const URL = "http://localhost:3000/json/blog.json";

  const { data } = await useAsyncData(`blog`, () => {
    return $fetch(URL);
  });
  if (data?.value) list.value = data.value;
</script>

<style lang="less">

</style>