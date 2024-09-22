<template>
	<NuxtLink :to="to"
		><div class="back-button">
			<svg
				xmlns="http://www.w3.org/2000/svg"
				height="24px"
				viewBox="0 -960 960 960"
				width="24px"
				fill="currentColor">
				<path
					d="m313-440 224 224-57 56-320-320 320-320 57 56-224 224h487v80H313Z" />
			</svg>
			{{text}}
		</div></NuxtLink
	>
</template>

<script>
export default {
  props: {
    to: {
      type: String,
      required: true,
    },
    text: {
      type: String,
      default: "Kembali",
    }
  },
};
</script>

<style scoped></style>
