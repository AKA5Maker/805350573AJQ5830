<script setup lang="ts">
import EventCard from '../components/EventCard.vue'
import EventInfo from '../components/EventInfo.vue'
import type { Event } from '@/types'
import { ref, onMounted, computed, watchEffect } from 'vue'
import EventService from '../services/EventService'
import { useRouter } from 'vue-router'

const events = ref<Event[] | null>(null)
const totalEvents = ref(0)

const props = defineProps({
  page: {
    type: Number,
    required: true
  }
})

const currentPage = computed(() => props.page)

const hasNextPage = computed(() => {
  const totalPages = Math.ceil(totalEvents.value / 3) // 改为每页3个
  return currentPage.value < totalPages
})

const router = useRouter()

onMounted(() => {
  watchEffect(() => {
    // 移除 events.value = null 避免闪烁
    EventService.getEvents(3, currentPage.value) // 改为每页3个
      .then((response) => {
        events.value = response.data
        totalEvents.value = response.headers['x-total-count']
      })
      .catch(() => {
        router.push({ name: 'network-error-view' })
      })
  })
})
</script>

<template>
  <h1>Events For Good</h1>
  <div class="events">
    <div v-for="event in events" :key="event.id" class="event-container">
      <EventCard :event="event" />
      <EventInfo :event="event" />
    </div>
  </div>

  <div class="pagination">
    <RouterLink
      id="page-prev"
      :to="{ name: 'event-list-view', query: { page: currentPage - 1 } }"
      rel="prev"
      v-if="currentPage != 1"
    >&lt; Prev Page</RouterLink>

    <RouterLink
      id="page-next"
      :to="{ name: 'event-list-view', query: { page: currentPage + 1 } }"
      rel="next"
      v-if="hasNextPage"
    >Next Page &gt;</RouterLink>
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.event-container {
  margin-bottom: 20px;
}

.pagination {
  display: flex;
  width: 290px;
}

.pagination a {
  flex: 1;
  text-decoration: none;
  color: #2c3e50;
}

#page-prev {
  text-align: left;
}

#page-next {
  text-align: right;
}
</style>
