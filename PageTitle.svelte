<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children?: Snippet;
		title: string;
		subtitle?: string;
	}

	let { children, title, subtitle }: Props = $props();
</script>

<div class="page-title">
	<h2 class="page-title-title">{title}</h2>

	{#if subtitle}
		<div class="page-title-subtitle">{subtitle}</div>
	{/if}

	{#if children}
		<div class="page-title-actions">{@render children()}</div>
	{/if}
</div>

<style>
	:where(:root) {
		--page-title-margin: var(--size-9);
		--page-title-gap: var(--size-5);
	}

	.page-title {
		margin-block: var(--page-title-margin);
		display: grid;
		grid-template-areas:
			'title actions'
			'subtitle actions';
		grid-template-columns: 1fr auto;
		grid-template-rows: auto auto;
		column-gap: var(--page-title-gap);
		align-items: end;

		.page-title-title {
			grid-area: title;
			font-size: var(--font-size-6);
			font-weight: var(--font-weight-8);
		}

		.page-title-subtitle {
			grid-area: subtitle;
			font-size: var(--font-size-4);
			font-weight: var(--font-weight-6);
		}

		.page-title-actions {
			grid-area: actions;
		}
	}
</style>
