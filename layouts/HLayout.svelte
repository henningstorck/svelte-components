<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children: Snippet;
		align?: 'start' | 'center' | 'end';
		justify?: 'start' | 'center' | 'end';
	}

	let { children, align = 'center', justify = 'start' }: Props = $props();
</script>

<div
	class="h-layout"
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
	:where(.h-layout) {
		--h-layout-gap: var(--size-3);
	}

	.h-layout {
		display: flex;
		flex-direction: row;
		gap: var(--h-layout-gap);
		flex-wrap: wrap;
		width: 100%;

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
