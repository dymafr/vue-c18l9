<template>
  <div
    class="
      card
      p-20
      d-flex
      flex-column
      justify-content-center
      align-items-center
    "
  >
    <h1>La page B</h1>
    <div v-if="state.user">
      <h2>{{ state.user.name }}</h2>
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive, watchEffect } from 'vue';
import { useRoute } from 'vue-router';

const state = reactive<{ user: any }>({
  user: null,
});

const route = useRoute();

watchEffect(async () => {
  if (route.params.userId) {
    const response = await fetch(
      `https://restapi.fr/api/usertest/${route.params.userId}`
    );
    state.user = await response.json();
  } else {
    state.user = null;
  }
});
</script>

<style scoped lang="scss">
.card {
  width: 100%;
  height: 300px;
}
</style>
