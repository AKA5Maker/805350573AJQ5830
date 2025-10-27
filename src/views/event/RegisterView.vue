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

const register = () => {
  messageStore.updateMessage('You are successfully registered for ' + props.event.title)
  setTimeout(() => {
    messageStore.resetMessage()
  }, 3000)
  router.push({ name: 'event-detail-view' })
}
</script>

<template>
  <div class="register-container">
    <h2>Register for {{ event.title }}</h2>
    <p>Fill out the form below to register for this event:</p>

    <div class="form-group">
      <label>Name:</label>
      <input type="text" placeholder="Enter your name" />
    </div>

    <div class="form-group">
      <label>Email:</label>
      <input type="email" placeholder="Enter your email" />
    </div>

    <button @click="register" class="register-btn">Register Me!</button>
  </div>
</template>

<style scoped>
.register-container {
  max-width: 400px;
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

.form-group input {
  width: 100%;
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.register-btn {
  background-color: #42b983;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
  margin-top: 10px;
}

.register-btn:hover {
  background-color: #369c6f;
}
</style>
