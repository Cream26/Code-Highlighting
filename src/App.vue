<template>
  <div class="flex flex-col h-screen">
    <!-- Top Navigation -->
    <Top_navigation />
    <Central_region />
    <Bottom_mark />
  </div>
</template>

<script setup lang="ts">
import Top_navigation from './components/top_navigation.vue'
import Bottom_mark from './components/bottom_mark.vue'
import Central_region from './components/central_region.vue'
</script>
