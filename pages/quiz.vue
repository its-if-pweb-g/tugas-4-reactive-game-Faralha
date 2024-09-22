<template>
	<div class="outer p-2">
		<div class="container" style="margin-top: 10rem">
			<Kembali to="/" />

			<p>Bermain sebagai: {{ username }}</p>
			<Question
				class="questions"
				v-for="(q, index) in questions"
				:key="index"
				:question="q.question"
				:answer="q.answer"
				:correctAnswer="q.correctAnswer"
				:selectedAnswer="q.selectedAnswer"
				@answered="handleAnswered(q, $event)" />
			<NuxtLink
				to="/scores"
				class="btn btn-primary w-100 mb-5"
				@click="handleSaved"
				>Lihat Skor</NuxtLink
			>
		</div>
	</div>
</template>

<script>
import { ref, onMounted } from "vue";
import questionsData from "~/questions.json";

export default {
	setup() {
		const questions = ref([]);
		const score = ref(0);
		const username = ref("");

		const loadQuestions = () => {
			const storedQuestions = JSON.parse(sessionStorage.getItem("questions"));
			if (storedQuestions && storedQuestions.length > 0) {
				questions.value = storedQuestions;

				// Recalculate score
				score.value = storedQuestions.reduce((acc, question) => {
					return acc + (question.isCorrect ? 1 : 0);
				}, 0);
			} else {
				questions.value = questionsData.map((q) => ({
					...q,
					isCorrect: false,
					selectedAnswer: null,
				}));
			}
		};

		const handleAnswered = (question, answer) => {
			const isCorrect = answer.isCorrect;

			if (isCorrect && !question.isCorrect) {
				score.value++;
			} else if (!isCorrect && question.isCorrect) {
				score.value--;
			}

			question.isCorrect = isCorrect;
			question.selectedAnswer = answer.answer;

			// cache to session storage
			sessionStorage.setItem("questions", JSON.stringify(questions.value));
		};

		// store leaderboard to local storage
		const handleSaved = () => {
			const leaderboard = JSON.parse(localStorage.getItem("leaderboard")) || [];
			leaderboard.push({
				username: username.value,
				score: score.value,
			});
			localStorage.setItem("leaderboard", JSON.stringify(leaderboard));
		};

		onMounted(() => {
			username.value = sessionStorage.getItem("username");
			loadQuestions();
		});

		return {
			questions,
			handleAnswered,
			handleSaved,
			score,
			username,
		};
	},
};
</script>

<style scoped>

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
