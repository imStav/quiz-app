<script setup>
import q from "../data/data.json";
import { ref, watch } from "vue";
import Card from "../components/Card.vue";
import gsap from "gsap";

const quizzes = ref(q);
const search = ref("");

watch(search, () => {
  quizzes.value = q.filter((quiz) =>
    quiz.name.toLocaleLowerCase().includes(search.value.toLocaleLowerCase())
  );
});

// Card animations
// Before-enter hook equivalent of card-enter-from CSS rule
const beforeEnter = (el) => {
  console.log("before enter");
  el.style.opacity = 0;
  el.style.transform = "translateY(-60px)";
};

const enter = (el) => {
  console.log("enter");
  gsap.to(el, {
    y: 0,
    opacity: 1,
    duration: 0.5,
    delay: el.dataset.index * 0.3
  })
}
</script>

<template>
  <div>
    <header>
      <h1>Quizes</h1>
      <input v-model.trim="search" type="text" placeholder="Search..." />
    </header>

    <div class="options-container">
      <TransitionGroup 
        appear
        @before-enter="beforeEnter"
        @enter="enter"
      >
        <Card 
          v-for="(quiz, index) in quizzes" 
          :key="quiz.id" 
          :quiz="quiz" 
          :data-index="index"
        />
      </TransitionGroup>
    </div>
  </div>
</template>

<style scoped>
header {
  margin-bottom: 10px;
  margin-top: 30px;
  display: flex;
  align-items: center;
}

header h1 {
  font-weight: bold;
  margin-right: 30px;
}

header input {
  border: none;
  background-color: rgba(128, 128, 128, 0.1);
  padding: 10px;
  border-radius: 5px;
}

.options-container {
  display: flex;
  flex-wrap: wrap;
  margin-top: 40px;
}
</style>
