<template>
  <div>
    <h2 style="text-align: center; padding: 0 20px 0 20px;">{{ question }}</h2>
    <div class="answer d-flex justify-content-around mt-4">
      <Answer
        v-for="(ans, index) in answer"
        :answer="ans"
        :key="index"
        :isSelected="selectedAnswer === ans"
        @answered="handleAnswer(ans)"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';


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
    selectedAnswer: {
      type: String,
      default: null,
    }
  },
  setup(props, { emit }) {
    const selectedAnswer = ref<string | null>(props.selectedAnswer);

    const handleAnswer = (selectedAnswerValue: string) => {
      if (selectedAnswer.value === selectedAnswerValue) {
        return;
      }

      selectedAnswer.value = selectedAnswerValue;
      const isCorrect = selectedAnswerValue === props.correctAnswer;
      emit('answered', { isCorrect, answer: selectedAnswerValue });
    };

    return {
      selectedAnswer,
      handleAnswer
    };
  }
});
</script>

<style scoped>
.answer {
  flex-direction: row;
  padding: 0 15px 0 15px;

  @media only screen and (max-width: 900px){
    flex-direction: column;
  }
}
</style>