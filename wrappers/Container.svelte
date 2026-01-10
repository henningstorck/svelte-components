<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children: Snippet;
		size?: 'fluid' | 'narrow' | undefined;
	}

	let { children, size = undefined }: Props = $props();
</script>

<div class="container" class:fluid={size === 'fluid'} class:narrow={size === 'narrow'}>
	{@render children()}
</div>

<style>
	:where(.container) {
		--container-width: 1200px;
		--container-width-narrow: 800px;
		--container-width-fluid: 100%;
		--container-padding: var(--size-5);
	}

	.container {
		width: 100%;
		max-width: var(--container-width);
		margin-inline: auto;
		padding-inline: var(--container-padding);

		&.fluid {
			max-width: var(--container-width-fluid);
		}

		&.narrow {
			max-width: var(--container-width-narrow);
		}
	}
</style>
