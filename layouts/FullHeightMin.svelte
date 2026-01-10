<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children: Snippet;
	}

	let { children }: Props = $props();
</script>

<div class="full-height-min">
	{@render children()}
</div>

<style>
	.full-height-min {
		flex: 0 0 auto;
		width: 100%;
	}
</style>
