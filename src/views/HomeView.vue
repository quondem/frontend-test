<template>
	<main>
		<FormBuilder :config="config" />
	</main>
</template>

<script setup>
	import FormBuilder from "../components/FormBuilder.vue";
	import config from "@/json/form-config.json";
</script>
