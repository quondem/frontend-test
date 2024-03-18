<template>
	<FormInput
		:label="label"
		:type="type"
		:name="name"
		:error="error" />
</template>

<script>
	import FormInput from "@/components/form-items/FormInput.vue";

	export default {
		name: "FormPassword",
		props: {
			label: {
				type: String,
				default: "",
			},
			type: {
				type: String,
				default: "text",
			},
			name: {
				type: String,
				default: "",
			},
			error: {
				type: String,
				default: "",
			},
		},
		components: {
			FormInput,
		},
	};
</script>

<style lang="scss" scoped></style>
