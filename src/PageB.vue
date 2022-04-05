<template>
  <div class="card p-20 d-flex justify-content-center align-items-center">
    <h1>La page B</h1>
    <div v-if="state.user">
      <h2>{{ user.name }}</h2>
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive, watchEffect } from 'vue';
import { useRoute } from 'vue-router';

const state = reactive<{ user: any; users: any[] }>({
  user: null,
  users: null,
});

const route = useRoute();

watchEffect(async () => {
  state.users = await fetch('https://restapi.fr/api/usertest/').json();
  console.log(state.users);
  if (route.params.userId) {
    state.user = await fetch(
      `https://restapi.fr/api/usertest/${route.params.userId}`
    ).json();
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
