<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children: Snippet;
		color: string;
	}

	let { children, color }: Props = $props();
</script>

<div class="tag" style="--tag-color: {color}">
	{@render children()}
</div>

<style>
	.tag {
		display: flex;
		align-items: center;
		gap: var(--size-2);
		font-size: var(--font-size-0);
		text-transform: uppercase;

		&::before {
			content: '';
			display: inline-block;
			width: var(--size-3);
			height: var(--size-2);
			background-color: var(--tag-color);
			border-radius: var(--radius-round);
		}
	}
</style>
