<template>
	<div>
		<p>{{ label }}</p>
		<input
			v-bind="$attrs"
			:value="value"
			@input="$emit('input', $event.target.value)"
			:type="type"
			:name="name"
			required />
	</div>
</template>

<script>
	export default {
		name: "FormInput",

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
	};
</script>

<style scoped></style>
