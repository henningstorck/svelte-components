<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children: Snippet;
		minWidth?: number;
		stretch?: boolean;
	}

	let { children, minWidth = 400, stretch = false }: Props = $props();
</script>

<div class="grid-layout" style="--grid-layout-min-width: {minWidth}px" class:stretch>
	{@render children()}
</div>

<style>
	:where(:root) {
		--grid-layout-gap: var(--size-3);
	}

	.grid-layout {
		display: grid;
		gap: var(--grid-layout-gap);
		grid-template-columns: repeat(
			auto-fill,
			minmax(min(var(--grid-layout-min-width), 100%), 1fr)
		);

		&.stretch {
			grid-template-columns: repeat(
				auto-fit,
				minmax(min(var(--grid-layout-min-width), 100%), 1fr)
			);
		}
	}
</style>
