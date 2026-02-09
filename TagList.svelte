<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children: Snippet;
	}

	let { children }: Props = $props();
</script>

<div class="tag-list">
	{@render children()}
</div>

<style>
	.tag-list {
		display: flex;
		flex-wrap: wrap;
		gap: var(--size-2) var(--size-4);
	}
</style>
