<template>
	<div class="generator">
		<Generator />
	</div>
</template>

<script lang="ts">
	import { Vue, Component } from 'vue-property-decorator';
	import Generator from '../components/generator.vue';
	@Component({
		components: { Generator },
	})
	export default class MainLayout extends Vue {}
</script>

<style lang="scss" scoped></style>
