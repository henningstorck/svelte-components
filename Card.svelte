<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children: Snippet;
		title?: string;
	}

	let { children, title }: Props = $props();
</script>

<div class="card">
	{#if title}
		<div class="card-title">{title}</div>
	{/if}

	<div class="card-content">
		{@render children()}
	</div>
</div>

<style>
	:where(:root) {
		--card-margin: var(--size-5);
		--card-padding: var(--size-5);
		--card-bg: var(--surface-1);
		--card-radius: var(--radius-2);
	}

	.card {
		background-color: var(--card-bg);
		border-radius: var(--card-radius);
		margin-block: var(--card-margin);

		.card-title {
			padding: var(--card-padding);
			border-bottom: var(--border-size-2) solid var(--body-bg);
			font-weight: var(--font-weight-7);
			font-size: var(--font-size-3);
		}

		.card-content {
			padding: var(--card-padding);
		}
	}
</style>
