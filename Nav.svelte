<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children: Snippet;
	}

	let { children }: Props = $props();
</script>

<nav class="nav">
	{@render children()}
</nav>

<style>
	:where(.nav) {
		--nav-gap-y: var(--size-1);
		--nav-gap-x: var(--size-5);
	}

	.nav {
		display: flex;
		flex-direction: row;
		gap: var(--nav-gap-y) var(--nav-gap-x);

		:global(a) {
			color: var(--text-1);
			text-decoration-color: var(--text-1);
			font-weight: var(--font-weight-6);
			font-size: var(--font-size-2);
		}

		@media (max-width: 1000px) {
			flex-direction: column;
			align-items: center;
		}
	}
</style>
