<template>
  <div class="card p-20 d-flex justify-content-center align-items-center">
    <h1>La page B</h1>
    <div></div>
  </div>
</template>

<script setup lang="ts">
import { reactive, watchEffect } from 'vue';
import { useRoute, onBeforeRouteUpdate } from 'vue-router';

const state = reactive<{ user: any }>({ user: null });

const route = useRoute();

watchEffect(async () => {
  if (route.params.userId) {
    state.user = await fetch(
      `https://restapi.fr/api/usertest/${route.params.userId}`
    ).json();
  }
});
</script>

<style scoped lang="scss">
.card {
  width: 100%;
  height: 300px;
}
</style>
