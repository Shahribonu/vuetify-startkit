<script>
import { RouterLink, RouterView } from "vue-router";
import MainLayout from "./layout/MainLayout.vue";

export default {
  components: {
    MainLayout,
  },
};
</script>

<template>
  <MainLayout>
    <RouterView />
  </MainLayout>

  <RouterView />
</template>
