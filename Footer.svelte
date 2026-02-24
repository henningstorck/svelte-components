<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children?: Snippet;
		copyright?: string;
	}

	let { children, copyright }: Props = $props();
</script>

<footer class="footer" class:justify-center={!children}>
	<div class="footer-copyright">{copyright}</div>

	{#if children}
		<div class="footer-content">
			{@render children()}
		</div>
	{/if}
</footer>

<style>
	:where(:root) {
		--footer-padding: var(--size-5);
		--footer-gap: var(--size-5);
	}

	.footer {
		padding: var(--footer-padding);
		display: flex;
		flex-direction: row;
		gap: var(--footer-gap);
		align-items: center;
		justify-content: space-between;
		font-weight: var(--font-weight-6);

		&.justify-center {
			justify-content: center;
		}

		@media (max-width: 1000px) {
			flex-direction: column;
		}
	}
</style>
