<script setup lang="ts">
import { defineProps, withDefaults } from 'vue'

const props = withDefaults(
  defineProps<{
    resource?: string
  }>(),
  {
    resource: 'page'
  }
)
</script>

<template>
  <div class="not-found">
    <h1>Oops!</h1>
    <h3>The {{ resource }} you're looking for is not here.</h3>
    <RouterLink :to="{ name: 'event-list-view' }">Back to the home page</RouterLink>
  </div>
</template>

<style scoped>
.not-found {
  text-align: center;
  padding: 50px;
}

.not-found h1 {
  color: #ff6b6b;
  font-size: 3rem;
  margin-bottom: 20px;
}

.not-found h3 {
  color: #666;
  margin-bottom: 30px;
}

.not-found a {
  color: #42b983;
  text-decoration: none;
  font-weight: bold;
}

.not-found a:hover {
  text-decoration: underline;
}
</style>
