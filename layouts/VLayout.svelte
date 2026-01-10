<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children: Snippet;
		align?: 'start' | 'center' | 'end';
		justify?: 'start' | 'center' | 'end';
	}

	let { children, align = 'start', justify = 'start' }: Props = $props();
</script>

<div
	class="v-layout"
	class:align-start={align === 'start'}
	class:align-center={align === 'center'}
	class:align-end={align === 'end'}
	class:justify-start={justify === 'start'}
	class:justify-center={justify === 'center'}
	class:justify-end={justify === 'end'}
>
	{@render children()}
</div>

<style>
	:where(.v-layout) {
		--v-layout-gap: var(--size-3);
	}

	.v-layout {
		display: flex;
		flex-direction: column;
		gap: var(--v-layout-gap);

		&.align-start {
			align-items: start;
		}

		&.align-center {
			align-items: center;
		}

		&.align-end {
			align-items: end;
		}

		&.justify-start {
			justify-content: start;
		}

		&.justify-center {
			justify-content: center;
		}

		&.justify-end {
			justify-content: end;
		}
	}
</style>
