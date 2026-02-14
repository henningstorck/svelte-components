<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children: Snippet;
	}

	let { children }: Props = $props();
</script>

<nav class="button-group">
	{@render children()}
</nav>

<style>
	:where(:root) {
		--button-group-radius: var(--radius-2);
	}

	.button-group {
		display: inline-flex;
		flex-direction: row;
		flex-wrap: nowrap;
		border-radius: var(--button-group-radius);
		overflow: hidden;

		:global(.button) {
			border-radius: 0;

			&:active {
				transform: scale(1);
			}
		}
	}
</style>
