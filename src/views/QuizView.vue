<script setup>
import { ref, watch, computed } from "vue";
import { useRoute } from "vue-router";
import Question from "../components/Question.vue";
import QuizHeader from "../components/QuizHeader.vue";
import quizzes from "../data/data.json";
import Result from "../components/Result.vue";

const route = useRoute();
const quizId = parseInt(route.params.id);
const currentQuestionIndex = ref(0);
const quiz = quizzes.find((q) => q.id === quizId);
const numberOfCorrectAnswers = ref(0);
const showResults = ref(false);

// We can do the same thing using computed like below

// const questionStatus = ref(`${currentQuestionIndex.value}/${quiz.questions.length}`);

// watch(() => currentQuestionIndex.value, () => {
//   questionStatus.value = `${currentQuestionIndex.value}/${quiz.questions.length}`
// });

const questionStatus = computed(
  () => `${currentQuestionIndex.value}/${quiz.questions.length}`
);

const barPercentage = computed(
  () => `${(currentQuestionIndex.value / quiz.questions.length) * 100}%`
);

const onOptionSelected = (isCorrect) => {
  if (isCorrect) {
    numberOfCorrectAnswers.value++;
  }

  if (quiz.questions.length - 1 === currentQuestionIndex.value) {
    showResults.value = true;
  }

  currentQuestionIndex.value++;
};
</script>

<template>
  <div>
    <QuizHeader
      :questionStatus="questionStatus"
      :barPercentage="barPercentage"
    />
    <div>
      <Question
        v-if="!showResults"
        :question="quiz.questions[currentQuestionIndex]"
        @selectOption="onOptionSelected"
      />

      <Result
        v-else
        :quizQuestionLength="quiz.questions.length"
        :numberOfCorrectAnswers="numberOfCorrectAnswers"
      />
    </div>
  </div>
</template>
