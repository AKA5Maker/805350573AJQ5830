<script setup lang="ts">
import type { Event } from '@/types'

defineProps<{
  event: Event
}>()
</script>

<template>
  <div class="event-info">
    <div class="info-item">{{ event.category }}</div>
    <div class="info-item">{{ event.organizer }}</div>
  </div>
</template>

<style scoped>
.event-info {
  font-size: 14px;
  text-align: right;
}

.info-item {
  margin-bottom: 4px;
}
</style>
