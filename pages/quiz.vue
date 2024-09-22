<template>
	<div class="outer">
		<div class="container p-2">
			<Question
				class="questions"
				v-for="(q, index) in questions"
				:key="index"
				:question="q.question"
				:answer="q.answer"
				:correctAnswer="q.correctAnswer"
				@answered="handleAnswered(q, $event)" />

			<NuxtLink to="/scores" class="btn btn-primary w-100 mb-5"
				>Lihat Skor</NuxtLink
			>
		</div>
	</div>
</template>

<script>
import { ref } from "vue";
import questionsData from "~/questions.json";

export default {
	setup() {
		const questions = ref(
			questionsData.map((q) => ({ ...q, isCorrect: false }))
		);
		const score = ref(0);

		const handleAnswered = (question, answer) => {
			const isCorrect = answer.isCorrect;

			if (isCorrect && !question.isCorrect) {
				score.value++;
			} else if (!isCorrect && question.isCorrect) {
				score.value--;
			}

			// Update the question's isCorrect state
			question.isCorrect = isCorrect;
		};

		return {
			questions,
			handleAnswered,
			score,
		};
	},
};
</script>

<style scoped>
.outer {
  background-color: white;
}
.questions {
  display: flex;
  flex-direction: column;
  align-items: around;
  justify-content: center;
	padding: 3rem 1rem;
  border-radius: 13px;
  border: 1px solid gray;
  margin: 15px 0 15px 0;
}
</style>
