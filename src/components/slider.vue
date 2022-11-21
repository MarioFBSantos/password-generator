<template>
	<div class="sliderContainer">
		<q-slider
			v-model="size"
			:min="5"
			:max="15"
			color="secondary"
			@input="$emit('input', $event)"
		/>
		<div class="size">
			{{ size }}
		</div>
	</div>
</template>

<script lang="ts">
	import { Vue, Component } from 'vue-property-decorator';

	@Component({
		components: {},
	})
	export default class Slider extends Vue {
		size = 5;
	}
</script>

<style lang="scss" scoped>
	.sliderContainer {
		display: flex;
		gap: 15px;
		align-items: center;
	}

	.size {
		font-size: 2em;
		color: #26a69a;
	}
</style>
