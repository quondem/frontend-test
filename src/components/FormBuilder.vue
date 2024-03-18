<template>
	<div class="form-builder">
		<!-- Должно собираться автоматически, а не руками как сейчас, согласно конфигу   -->
		<form
			v-for="(form, key) in config"
			:key="key"
			:ref="key"
			@submit.prevent="">
			<div>
				{{ form.name }}
				<component
					v-for="(item, index) in form.items"
					:key="index"
					:is="formMap[item?.type]"
					:name="`item?.name#${form.name}`"
					:label="item?.label"
					:type="item?.type"
					:error="validateErrors[key][item.name]"
					:options="item.additional?.options"
					:modelValue="formInfo[key][item.name]"
					@update:modelValue="formInfo[key][item.name] = $event" />

				<button
					@click="onSubmit(key)"
					type="submit">
					Отправить
				</button>
				<button
					@click="clearForm(key)"
					type="reset">
					Стереть
				</button>
			</div>
		</form>
	</div>
</template>

<script>
	import FormInput from "@/components/form-items/FormInput.vue";
	import FormSelect from "@/components/form-items/FormSelect.vue";
	import FormRadio from "@/components/form-items/FormRadio.vue";
	import FormPassword from "@/components/form-items/FormPassword.vue";

	export default {
		name: "FormBuilder",

		props: {
			config: {
				type: Object,
				required: true,
				default: {},
			},
		},

		data() {
			return {
				formInfo: {},
				validateErrors: {},
				formMap: {
					input: "FormInput",
					select: "FormSelect",
					radio: "FormRadio",
					password: "FormPassword",
				},
			};
		},

		methods: {
			createFormFields() {
				for (let key in this.config) {
					let form = this.config[key];
					this.formInfo[key] = {};
					this.validateErrors[key] = {};
					for (let item of form.items) {
						this.formInfo[key][item.name] = "";
						this.validateErrors[key][item.name] = "";
					}
					for (let item of form.items) {
						let options = item?.additional?.options;
						if (options) {
							options.forEach(option => {
								option.selected ? (this.formInfo[key][item.name] = option.value) : null;
							});
						}
					}
				}
			},
			validateForm(form) {
				let valid = true;

				for (let key in this.formInfo[form]) {
					let value = this.formInfo[form][key];
					if (!value.trim()) {
						valid = false;
						this.validateErrors[form][key] = "Это поле обязательно!";
					} else if (key == "repeat-pass" && value !== this.formInfo[form]["pass"]) {
						valid = false;
						this.validateErrors[form][key] = "Пароли не совпадают";
					} else {
						this.validateErrors[form][key] = "";
					}
				}
				return valid;
			},
			async onSubmit(form) {
				let valid = this.validateForm(form);
				if (valid) {
					for (let key in this.formInfo) {
						this.formInfo[key]["repeat-pass"] = undefined;
					}
					fetch("https://fetch123.com", {
						method: "POST",
						body: JSON.stringify(this.formInfo),
					}).catch(() => {});
					this.clearForm(form);
				}
			},
			clearForm(form) {
				for (let key in this.formInfo[form]) {
					this.formInfo[form][key] = "";
				}
				this.$refs[form][0].reset();
			},
		},

		created() {
			this.createFormFields();
		},
		components: { FormPassword, FormRadio, FormSelect, FormInput },
	};
</script>

<style>
	.error {
		color: red;
	}
</style>
