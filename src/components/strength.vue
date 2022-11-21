<template>
	<div class="displayStrength">
		{{ force }}
		<div class="barContainer" :class="cForce">
			<div class="firstBar bar"></div>
			<div class="secondBar bar"></div>
			<div class="thirdBar bar"></div>
			<div class="fourthBar bar"></div>
		</div>
	</div>
</template>

<script lang="ts">
	import { Vue, Component, Prop, Watch } from 'vue-property-decorator';

	@Component({
		components: {},
	})
	export default class Strength extends Vue {
		@Prop({ default: '' })
		password!: string;

		force = 'force';

		pointsForce = 0;

		cForce = '';

		strongPassword = new RegExp(
			'(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9])(?=.*[^A-Za-z0-9])(?=.{8,})'
		);
		mediumPassword = new RegExp(
			'((?=.*[a-z])(?=.*[A-Z])(?=.*[0-9])(?=.*[^A-Za-z0-9])(?=.{6,}))|((?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])(?=.{8,}))'
		);

		@Watch('password')
		handleStrength(pass: string) {
			if (this.strongPassword.test(pass)) {
				this.force = 'Strong';
				this.cForce = 'strong';
				this.pointsForce = 4;
			} else if (this.mediumPassword.test(pass)) {
				this.force = 'Medium';
				this.cForce = 'medium';
				this.pointsForce = 3;
			} else {
				this.force = 'Weak';
				this.cForce = 'weak';
				this.pointsForce = 2;
			}
		}
	}
</script>

<style lang="scss" scoped>
	.displayStrength {
		display: flex;
		gap: 5px;
		align-items: center;
	}
	.bar {
		border: 1px solid rgb(39, 39, 39);
		width: 14px;
		height: 28px;
	}
	.barContainer {
		display: flex;
		gap: 4px;
	}

	.strong {
		.firstBar {
			background-color: red;
		}
		.secondBar {
			background-color: orange;
		}
		.thirdBar {
			background-color: greenyellow;
		}
		.fourthBar {
			background-color: green;
		}
	}

	.medium {
		.firstBar {
			background-color: red;
		}
		.secondBar {
			background-color: orange;
		}
		.thirdBar {
			background-color: greenyellow;
		}
	}

	.weak {
		.firstBar {
			background-color: red;
		}
		.secondBar {
			background-color: orange;
		}
	}
</style>
