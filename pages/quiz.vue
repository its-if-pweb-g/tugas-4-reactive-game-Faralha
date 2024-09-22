<template>
	<div class="container">
		<Question
			class="mt-5"
			v-for="(q, index) in questions"
			:key="index"
			:question="q.question"
			:answer="q.answer"
			:correctAnswer="q.correctAnswer"
			@answered="handleAnswered" />
	</div>
</template>

<script>
import questions from "~/questions.json";

export default {
  setup() {
    const score = ref(0);
    
		const handleAnswered = (answer) => {
      if (answer.isCorrect) {
        score.value++;
				console.log("Correct");
			} else {
				console.log("Incorrect");
      }

    };

    
		return {
			questions,
      handleAnswered,
      score,
		};
	},
};
</script>

<style scoped></style>
