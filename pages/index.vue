<template>
	<div class="outer">
		<div class="container vh-100 d-flex flex-column">
			<div
				class="flex-grow-1 d-flex flex-column justify-content-center align-items-start">
				<h1><span style="font-size: 2rem;">Quiz:</span><br>Tes Pengetahuan Nawasena 2024</h1>

				<label for="username">Masukkan Username</label>
				<input
					type="text"
					name="username"
					id="username"
					v-model="username"
					class="form-control" />
				<p v-if="errorMessage" class="text-danger">{{ errorMessage }}</p>
				<NuxtLink
					to="/quiz"
					class="btn btn-info mt-3 p-2 px-4"
					@click="handleRegister">
					Mulai Quiz
				</NuxtLink>
			</div>
			<Footer />
		</div>
	</div>
</template>

<script lang="ts">
import { ref, onMounted } from "vue";
import { useRouter } from "vue-router";

export default {
	setup() {
		const username = ref<string>("");
		const errorMessage = ref<string>("");
		const router = useRouter();

		const handleRegister = () => {
			if (!username.value.trim()) {
				errorMessage.value = "Username is required";
			} else {
				sessionStorage.setItem("username", username.value);
				sessionStorage.setItem("questions", JSON.stringify([]));
				errorMessage.value = "";
				router.push("/quiz"); // Navigate to quiz page
			}
		};

		onMounted(() => {
			username.value = sessionStorage.getItem("username") || "";
		});

		return {
			username,
			errorMessage,
			handleRegister,
		};
	},
};
</script>

<style scoped>
.outer{
	background-color: var(--primary);
	color: var(--secondary);
}
.container {
	min-height: 100vh;
	display: flex;
	flex-direction: column;
}
.flex-grow-1 {
	flex-grow: 1;
}
</style>
