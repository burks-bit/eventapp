<template>
  <Profile />
</template>

<script setup>
  import { ref } from 'vue';
  import Profile from '@/components/Profile.vue';

  const current_profile = ref(2);
</script>
