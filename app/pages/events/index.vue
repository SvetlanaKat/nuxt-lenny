<template>
  <div class="events">
    <div class="events__container">
    <AppListing title="Мероприятия" class="events__listing">
      <EventCard
        v-for="(card, index) in list"
        :key="index"
        :data="card"
        class="app-listing__card"
      />
    </AppListing>
    </div>
  </div>

  <TableEvents/>
  <OffersMain/>
  <InformationEvents/>

</template>

<script setup>
  const list = ref([]);

  const URL = "http://localhost:3000/json/events.json";

  const { data } = await useAsyncData(`events`, () => {
    return $fetch(URL);
  });
  if (data?.value) list.value = data.value;


  
  
</script>

<style lang="less">
  .events {
  padding: 110px 0 100px;

  @media @bw1340 {
    padding: 100px 0 100px;
  }

  @media @bw768 {
    padding: 50px 0 35px;
  }

  &__container {
  .container();

  &__listing {
    display: block;
    margin-bottom: 100px;
  }

  &__services {
    margin-top: 100%;
    margin-bottom: 50px;
  }

  &__span {
    display: flex;
    align-items: center;
    grid-area: span;
    font-family: @font1;
    font-weight: 600;
    font-size: 16px;
    background-color: @black;
    text-decoration: none;
    transition: color 0.2s;
  }
}
}


</style>