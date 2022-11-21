<template>
	<div class="center">
		<div class="container q-my-lg q-pa-lg">
			<Display :password="finalPassword" />
			<Slider v-model="size" />

			<div>
				<div class="checkContainer">
					<q-checkbox
						v-model="upper"
						label="Upper Case"
						color="teal"
					/>
					<q-checkbox
						v-model="lower"
						label="Lower Case"
						color="cyan"
					/>
					<q-checkbox
						v-model="numbers"
						label="Number"
						color="orange"
					/>
					<q-checkbox
						v-model="special"
						label="Special Characters"
						color="red"
					/>
				</div>
			</div>

			<div class="strenghtDisplay q-px-md">
				<span>Strength</span>
				<Strength :password="finalPassword" />
			</div>

			<q-btn color="secondary" class="button" @click="generate()"
				>Generate</q-btn
			>
		</div>
	</div>
</template>

<script lang="ts">
	import { Vue, Component } from 'vue-property-decorator';

	import Strength from './strength.vue';
	import Display from './passwordDisplay.vue';
	import Slider from './slider.vue';

	@Component({
		components: { Strength, Display, Slider },
	})
	export default class Generator extends Vue {
		numberChars = '0123456789';
		lowerChars = 'abcdefghijklmnopqrstuvwxyz';
		upperChars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
		specialChars = '!@#$%^&*()';

		size = 5;
		upper = true;
		lower = true;
		numbers = true;
		special = true;

		finalPassword = 'Password';

		get options() {
			let char = '';
			if (this.upper == true) {
				char = char + this.upperChars;
			}

			if (this.lower == true) {
				char = char + this.lowerChars;
			}

			if (this.numbers == true) {
				char = char + this.numberChars;
			}

			if (this.special == true) {
				char = char + this.specialChars;
			}

			return char;
		}

		generate() {
			let password = '';
			const chars = this.options;
			for (let i = 0; i < this.size; i++) {
				const randomNumber = Math.floor(Math.random() * chars.length);
				password += chars.substring(randomNumber, randomNumber + 1);
			}
			this.finalPassword = password;
			return password;
		}

		setSize(ev: number) {
			console.log('set size');
			this.size = ev;
		}
	}
</script>

<style lang="scss" scoped>
	.container {
		width: 50%;
		background-color: rgb(27, 27, 27);
		color: white;
		height: 500px;
		border-radius: 7px;
		display: flex;
		flex-direction: column;
		flex-wrap: nowrap;
		justify-content: space-between;
	}
	.center {
		display: flex;
		justify-content: space-around;
	}
	.checkContainer {
		display: flex;
		flex-direction: column;
	}

	.button {
		width: 100%;
	}
	.passwordDisplay {
		font-size: 2em;
	}

	.strenghtDisplay {
		background-color: rgb(15, 15, 15);
		font-size: 2em;
		color: #666;
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
</style>
