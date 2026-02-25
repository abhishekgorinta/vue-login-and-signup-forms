<script>
import Navbar from "./components/Navbar.vue";


export default {
  components: { Navbar }
}
</script>

<template>
  <Navbar />
  <main class="main-content">
    <router-view></router-view>
  </main>
</template>

<style>
.main-content {
  margin-top: 60px;
}
</style>
