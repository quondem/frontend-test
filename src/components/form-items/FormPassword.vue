<template>
	<FormInput
		:label="label"
		:type="type"
		:name="name"
		:value="value"
		@input="$emit('input', $event.target.value)" />
</template>

<script>
	import FormInput from "@/components/form-items/FormInput.vue";

	export default {
		name: "FormPassword",
		props: {
			value: {
				type: String,
			},
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
		},
		components: {
			FormInput,
		},
	};
</script>

<style lang="scss" scoped></style>
