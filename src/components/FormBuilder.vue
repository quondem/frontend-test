<template>
	<div class="form-builder">
		<!-- Должно собираться автоматически, а не руками как сейчас, согласно конфигу   -->
		<form @submit.prevent="onSubmit">
			<div
				v-for="item in form.items"
				:key="item.name">
				<div v-if="item.type == 'input'">
					<form-input
						v-model="info"
						:label="item.label"
						:type="item.type"
						:name="item.name" />
				</div>
				<div v-if="item.type == 'select'">
					<form-select
						:label="item.label"
						:name="item.name"
						:options="item.additional.options" />
				</div>
				<div v-if="item.type == 'radio'">
					<form-radio
						:label="item.label"
						:type="item.type"
						:name="item.name"
						:options="item.additional.options" />
				</div>
				<div v-if="item.type == 'password'">
					<form-password
						:name="item.name"
						:label="item.label"
						:type="item.type" />
				</div>
			</div>

			<button type="submit">Отправить</button>
			<button type="reset">Стереть</button>
		</form>
	</div>
</template>

<script>
	import FormInput from "@/components/form-items/FormInput.vue";
	import FormSelect from "@/components/form-items/FormSelect.vue";
	import FormRadio from "@/components/form-items/FormRadio.vue";
	import FormPassword from "@/components/form-items/FormPassword.vue";
	import config from "@/json/form-config.json";

	export default {
		name: "FormBuilder",

		data() {
			return {
				form: config.parent,
				info: "123",
			};
		},

		methods: {
			onSubmit() {
				alert("Submit");
			},
		},

		created: () => {},
		components: { FormPassword, FormRadio, FormSelect, FormInput },
	};
</script>

<style scoped></style>
