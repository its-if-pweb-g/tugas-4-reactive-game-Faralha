<template>
	<div class="outer">
		<div
			class="container d-flex flex-column justify-content-center align-items-start w-100 vh-100">
			<Kembali to="/" text="Main Lagi" class="mb-3" />
			<div v-if="leaderboard.length">
				<h1>Leaderboard</h1>
				<div
					v-for="(entry, index) in leaderboard"
					:key="index"
					class="leaderboard-entry">
					<p>
						<strong>{{ entry.username || entry.name }}</strong
						>: {{ entry.score }}
					</p>
				</div>
			</div>
			<div v-else>
				<p>No scores available.</p>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			leaderboard: JSON.parse(localStorage.getItem("leaderboard")) || [],
		};
	},
};
</script>

<style scoped>
.leaderboard-entry {
	padding: 5px;
}
p {
	margin: 0;
}
</style>
