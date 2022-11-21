<template>
	<div class="displayContainer">
		<div class="passwordDisplay">
			{{ password }}
		</div>
		<q-btn @click="copy(password)">Copy</q-btn>
	</div>
</template>

<script lang="ts">
	import { Vue, Component, Prop } from 'vue-property-decorator';
	import { copyToClipboard } from 'quasar';

	@Component({
		components: {},
	})
	export default class DisplayPassword extends Vue {
		@Prop()
		password!: string;

		copy(password: string) {
			copyToClipboard(password)
				.then(() => {
					this.$q.notify({
						type: 'positive',
						position: 'top',
						message: 'Copiado com sucesso',
					});
				})
				.catch(() => {
					this.$q.notify({
						type: 'negative',
						position: 'top',
						message: 'Nao copiado',
					});
				});
		}
	}
</script>

<style lang="scss" scoped>
	.passwordDisplay {
		font-size: 2em;
	}
	.displayContainer {
		display: flex;
		justify-content: space-between;
	}
</style>
