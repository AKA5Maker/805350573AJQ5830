<template>
  <div class="networkError">
    <h1>Uh-Oh!</h1>
    <h3>
      It looks like you're experiencing some network issues, please take a breath and
      <a href="#" @click="$router.go(-1)">click here</a> to try again.
    </h3>
    <p>Error details: Failed to load event data from server.</p>
  </div>
</template>

<style scoped>
.networkError {
  text-align: center;
  padding: 50px;
}

.networkError h1 {
  color: #ff6b6b;
  font-size: 3rem;
  margin-bottom: 20px;
}

.networkError h3 {
  color: #666;
  line-height: 1.6;
}

.networkError a {
  color: #42b983;
  text-decoration: none;
  font-weight: bold;
}

.networkError a:hover {
  text-decoration: underline;
}
</style>
