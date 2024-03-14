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
				:id="option.value"
				:value="option.value"
				:checked="option.selected" />
			<label :for="option.value">{{ option.text }}</label>
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
		},
	};
</script>

<style scoped></style>
