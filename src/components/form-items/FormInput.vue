<template>
	<div>
		<p>{{ label }}</p>
		<input
			v-bind="$attrs"
			@input="$emit('update:modelValue', $event.target.value)"
			:type="type"
			:name="name" />
		<div
			v-if="error"
			class="error">
			{{ error }}
		</div>
	</div>
</template>

<script>
	export default {
		name: "FormInput",

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
	};
</script>

<style scoped></style>
