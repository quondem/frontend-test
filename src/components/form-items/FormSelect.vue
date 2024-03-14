<template>
	<div>
		<p>{{ label }}</p>
		<select :name="name">
			<option
				v-for="option in options"
				:key="option.value"
				:selected="option.selected">
				{{ option.text }}
			</option>
		</select>
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
		},
	};
</script>

<style scoped></style>
