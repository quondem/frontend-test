<template>
	<div>
		<p>{{ label }}</p>
		<select
			@input="$emit('update:modelValue', $event.target.value)"
			:name="name">
			<option
				v-for="option in options"
				:key="option.value"
				:selected="option.selected">
				{{ option.text }}
			</option>
		</select>
		<div
			v-if="error"
			class="error">
			{{ error }}
		</div>
	</div>
</template>

<script>
	export default {
		name: "FormSelect",

		props: {
			label: {
				type: String,
				default: "",
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
