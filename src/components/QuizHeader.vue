<script setup>
import { defineProps } from "vue";

const { questionStatus, barPercentage } = defineProps([
  "questionStatus",
  "barPercentage",
]);
</script>

<template>
  <header>
    <h3>Question {{ questionStatus }}</h3>
    <div class="bar">
      <div class="completion" :style="{ width: barPercentage }"></div>
    </div>
  </header>
</template>

<style scoped>
header {
  margin-top: 20px;
}

.bar {
  width: 300px;
  height: 50px;
  border: 3px solid coral;
}

.completion {
  width: 0%;
  height: 100%;
  background-color: coral;
}
</style>
