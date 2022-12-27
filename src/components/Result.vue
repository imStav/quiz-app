<script setup>
import { RouterLink } from "vue-router";
import { defineProps } from "vue";

const { numberOfCorrectAnswers, quizQuestionLength } = defineProps([
  "quizQuestionLength",
  "numberOfCorrectAnswers"
]);
</script>

<template>
  <div class="results">
    <p>Your results...</p>

    <h1>{{ numberOfCorrectAnswers }} / {{ quizQuestionLength }}</h1>

    <RouterLink to="/">Go back</RouterLink>
  </div>
</template>

<style scoped>
h1 {
  font-size: 80px;
}

p {
  font-size: 25px;
}

.results {
  text-align: center;
  padding: 100px;
}
</style>
