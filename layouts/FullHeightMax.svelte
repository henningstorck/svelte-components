<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children: Snippet;
	}

	let { children }: Props = $props();
</script>

<div class="full-height-max">
	{@render children()}
</div>

<style>
	.full-height-max {
		flex: 1 1 0;
		width: 100%;
	}
</style>
