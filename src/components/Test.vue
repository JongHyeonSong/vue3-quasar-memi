<script setup lang="ts">
import { ref } from 'vue';
import AuthBtn from './auth/AuthBtn.vue';
const num = ref<number>(1);
</script>

<template>
  <AuthBtn />
  <q-btn @click="num += 1">
    <q-icon name="font_download" class="text-primary" style="font-size: 32px" />
    <span>{{ num }}</span>
  </q-btn>
</template>
