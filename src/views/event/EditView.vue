<script setup lang="ts">
import { toRefs } from 'vue'
import { useRouter } from 'vue-router'
import { useMessageStore } from '@/stores/message'
import type { Event } from '@/types'

const props = defineProps<{
  event: Event
  id: String
}>()

const { event } = toRefs(props)
const router = useRouter()
const messageStore = useMessageStore()

const saveEdit = () => {
  messageStore.updateMessage('The data has been updated successfully!')
  setTimeout(() => {
    messageStore.resetMessage()
  }, 3000)
  router.push({ name: 'event-detail-view' })
}
</script>

<template>
  <div class="edit-container">
    <h2>Edit Event: {{ event.title }}</h2>

    <div class="form-group">
      <label>Title:</label>
      <input type="text" :value="event.title" />
    </div>

    <div class="form-group">
      <label>Description:</label>
      <textarea :value="event.description" rows="4"></textarea>
    </div>

    <button @click="saveEdit" class="save-btn">Save Changes</button>
  </div>
</template>

<style scoped>
.edit-container {
  max-width: 500px;
  margin: 20px auto;
  padding: 20px;
  text-align: left;
}

.form-group {
  margin: 15px 0;
}

.form-group label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.save-btn {
  background-color: #42b983;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
  margin-top: 10px;
}

.save-btn:hover {
  background-color: #369c6f;
}
</style>
