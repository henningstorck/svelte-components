<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children?: Snippet;
		title: string;
		subtitle?: string;
		align?: 'start' | 'center' | 'end';
	}

	let { children, title, subtitle, align = 'start' }: Props = $props();
</script>

<div
	class="page-title"
	class:align-start={align === 'start'}
	class:align-center={align === 'center'}
	class:align-end={align === 'end'}
>
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

		&.align-start {
			text-align: start;
		}

		&.align-center {
			text-align: center;
		}

		&.align-end {
			text-align: end;
		}

		.page-title-title {
			grid-area: title;
			font-size: var(--font-size-6);
			font-weight: var(--font-weight-8);
			margin: 0;
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
