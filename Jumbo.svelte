<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		title?: string;
		subtitle?: string;
		children?: Snippet;
		align?: 'start' | 'center' | 'end';
	}

	let { title, subtitle, children, align = 'start' }: Props = $props();
</script>

<div
	class="jumbo"
	class:align-start={align === 'start'}
	class:align-center={align === 'center'}
	class:align-end={align === 'end'}
>
	{#if title}
		<h2 class="title">{title}</h2>
	{/if}

	{#if subtitle}
		<div class="subtitle">{subtitle}</div>
	{/if}

	{#if children}
		<div class="content">
			{@render children()}
		</div>
	{/if}
</div>

<style>
	.jumbo {
		margin-block: var(--size-9);

		&.align-start {
			text-align: start;
		}

		&.align-center {
			text-align: center;
		}

		&.align-end {
			text-align: end;
		}

		.title {
			font-size: var(--font-size-8);
			font-weight: var(--font-weight-8);
		}

		.subtitle {
			font-size: var(--font-size-4);
			font-weight: var(--font-weight-6);
		}

		.content {
			margin-top: var(--size-5);
		}
	}
</style>
