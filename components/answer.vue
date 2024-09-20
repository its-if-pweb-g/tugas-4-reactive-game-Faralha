<template>
	<div style="border: 1px solid black" class="p-2" @click="selectAnswer">
		<h3>{{ answer }}</h3>
	</div>
</template>

<script>
export default {
	props: {
		answer: {
			type: String,
			required: true,
		},
	},
	methods: {
		selectAnswer() {
			this.$emit('answered', this.answer);
		},
	},
};
</script>

<style scoped></style>
