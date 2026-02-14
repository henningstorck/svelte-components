<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children?: Snippet;
		icon: string;
		title: string;
		subtitle?: string;
	}

	let { children, icon, title, subtitle }: Props = $props();
</script>

<div class="status-message">
	<div class="status-message-icon">
		<i class="ph {icon}"></i>
	</div>

	<h3 class="status-message-title">
		{title}
	</h3>

	{#if subtitle}
		<div class="status-message-subtitle">
			{subtitle}
		</div>
	{/if}

	{#if children}
		<div class="status-message-actions">
			{@render children()}
		</div>
	{/if}
</div>

<style>
	:where(:root) {
		--whoopsie-margin: var(--size-9);
		--whoopsie-gap: var(--size-7);
	}

	.status-message {
		text-align: center;
		margin-block: var(--whoopsie-margin);

		.status-message-icon {
			margin-bottom: var(--whoopsie-gap);

			.ph {
				display: block;
				font-size: var(--size-11);
			}
		}

		.status-message-title {
			font-size: var(--font-size-6);
			font-weight: var(--font-weight-6);
		}

		.status-message-subtitle {
			font-size: var(--font-size-4);
			font-weight: var(--font-weight-4);
		}

		.status-message-actions {
			margin-top: var(--whoopsie-gap);
		}
	}
</style>
