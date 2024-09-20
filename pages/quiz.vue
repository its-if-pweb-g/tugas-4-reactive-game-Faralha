<template>
  <div class="container">
    
    <Question class="mt-5" 
    v-for="(q, index) in questions"
    :key="index"
    :question="q.question"
    :answer="q.answer"
    :correctAnswer="q.correctAnswer"
    @answered="handleAnswered"/>
  </div>
</template>

<script>
  import questions from '~/questions.json';

  export default {
  setup() {
      const handleAnswered = (isCorrect) => {
      if(isCorrect) {
        console.log('Correct');
      } else {
        console.log('Incorrect');
      }
    }
      return {
        questions,
        handleAnswered
      }
    }
  }
</script>

<style scoped>

</style>