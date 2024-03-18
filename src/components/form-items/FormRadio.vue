<template>
	<fieldset>
		<legend>{{ label }}</legend>

		<div
			v-for="option in options"
			:key="option.value">
			<input
				required
				:type="type"
				:name="name"
				:value="option.value"
				:checked="option.selected"
				@input="$emit('update:modelValue', $event.target.value)" />
			<label :for="option.value">{{ option.text }}</label>
		</div>
		<div
			v-if="error"
			class="error">
			{{ error }}
		</div>
	</fieldset>
</template>

<script>
	export default {
		name: "FormRadio",

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

			options: {
				type: Object,
				required: true,
			},
			error: {
				type: String,
				default: "",
			},
		},
	};
</script>

<style scoped></style>
