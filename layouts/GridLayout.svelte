<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children: Snippet;
	}

	let { children }: Props = $props();
</script>

<div class="grid-layout">
	{@render children()}
</div>

<style>
	:where(.grid-layout) {
		--grid-layout-gap: var(--size-3);
		--grid-layout-min-width: 400px;
	}

	.grid-layout {
		display: grid;
		gap: var(--grid-layout-gap);
		grid-template-columns: repeat(
			auto-fit,
			minmax(min(var(--grid-layout-min-width), 100%), 1fr)
		);
	}
</style>
