<template>
  <div>
    <MainHeader/>
    <OffersHeader/>
    <AboutHeader/>
  </div>
</template>

<script setup>
const props = defineProps({
    data: {
      type: Object,
      default: () => ({}),
    },
  });

  const date = computed(() => {
    try {
      const date = new Date(props.data.date);
      return `${date.toLocaleDateString()} | начало ${date.toLocaleTimeString(
        "ru-RU",
        {
          hour: "2-digit",
          minute: "2-digit",
        },
      )}`;
    } catch {
      return null;
    }
  });
</script>

<style lang="less"></style>