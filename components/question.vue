<template>
  <div>
    <h2>{{ question }}</h2>

    <div class="d-flex flex-column">
      <Answer v-for="ans in answer" :answer="ans" :key="ans" @answered="handleAnswer"/>
    </div>
  </div>
</template>

<script lang="ts">
  export default defineComponent({
    props: {
      question: {
        type: String,
        required: true,
      },
      answer: {
        type: Array as () => string[],
        required: true,
      },
      correctAnswer: {
        type: String,
        required: true,
      },
    },
    methods: {
      handleAnswer(selectedAnswer: string) {
        const isCorrect = selectedAnswer === this.correctAnswer;
        this.$emit('answered', isCorrect);
      }
    },
  },
  );
</script>

<style scoped>

</style>