<template>
	<div class="p-2 button" @click="selectAnswer" :class="{ selected: isSelected}">
		<p class="answer-text">{{ answer }}</p>
	</div>
</template>

<script>
export default {
	props: {
		answer: {
			type: String,
			required: true,
		},
		isSelected: {
			type: Boolean,
			default: false,
		},
	},

	methods: {
		selectAnswer() {
			this.$emit("answered", this.answer);
		},
	},
};
</script>

<style scoped>
.button {
	border: 1px solid black;
	border-radius: 3px;
	margin: 2px;
	transition: all 0.3s ease-in;
}
.button:hover {
	background-color: #c5c4c4;
	cursor: pointer;
}

.selected {
	background-color: #c5c4c4;
}

.answer-text {
	margin: 0;
	padding: 0;
	text-align: center;
	font-weight: 400;
	font-size: large;
}
</style>
