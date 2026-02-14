<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children: Snippet;
		title?: string;
		type?: 'submit' | 'reset';
		onclick?: () => void;
		href?: string;
		target?: string;
		download?: string;
		command?: string;
		commandfor?: string;
		color?:
			| 'primary'
			| 'secondary'
			| 'success'
			| 'danger'
			| 'warning'
			| 'info'
			| 'surface'
			| 'link';
		outline?: boolean;
		pill?: boolean;
		icon?: boolean;
		disabled?: boolean;
		block?: boolean;
		lazy?: boolean;
	}

	let {
		children,
		title,
		type,
		onclick,
		href,
		target,
		download,
		command,
		commandfor,
		color = 'secondary',
		outline = false,
		pill = false,
		icon = false,
		disabled = false,
		block = false,
		lazy = false
	}: Props = $props();
</script>

{#if href && !disabled}
	<!-- eslint-disable svelte/no-navigation-without-resolve -->
	<a
		class="button {color}"
		{href}
		{target}
		{download}
		{title}
		class:outline
		class:pill
		class:icon
		class:disabled
		class:block
		data-sveltekit-preload-data={lazy ? 'off' : undefined}
	>
		{@render children()}
	</a>
{:else}
	<button
		class="button {color}"
		{type}
		{onclick}
		{command}
		{commandfor}
		{title}
		class:outline
		class:pill
		class:icon
		{disabled}
		class:block
	>
		{@render children()}
	</button>
{/if}

<style>
	:where(:root) {
		--button-padding: var(--size-2) var(--size-4);
		--button-padding-link: var(--size-2);
		--button-padding-icon: var(--size-2);
		--button-gap: var(--size-2);
		--button-radius: var(--radius-2);
	}

	.button {
		display: inline-flex;
		flex-direction: row;
		gap: var(--button-gap);
		align-items: center;
		padding: var(--button-padding);
		border: var(--border-size-2) solid var(--button-bg);
		background-color: var(--button-bg);
		color: var(--button-color);
		border-radius: var(--button-radius);
		font-weight: var(--font-weight-6);
		cursor: pointer;
		text-decoration: none;
		width: max-content;
		transition:
			background-color 0.2s,
			border-color 0.2s,
			color 0.2s,
			transform 0.2s;

		&:hover:not(:disabled, .disabled) {
			background-color: color-mix(in srgb, var(--button-bg) 80%, Canvas 20%);
			border-color: color-mix(in srgb, var(--button-bg) 80%, Canvas 20%);
		}

		&:active:not(:disabled, .disabled) {
			transform: scale(0.97);
		}

		&.primary {
			--button-bg: var(--primary-bg);
			--button-color: var(--primary-fg);
		}

		&.secondary {
			--button-bg: var(--secondary-bg);
			--button-color: var(--secondary-fg);
		}

		&.success {
			--button-bg: var(--success-bg);
			--button-color: var(--success-fg);
		}

		&.danger {
			--button-bg: var(--danger-bg);
			--button-color: var(--danger-fg);
		}

		&.warning {
			--button-bg: var(--warning-bg);
			--button-color: var(--warning-fg);
		}

		&.info {
			--button-bg: var(--info-bg);
			--button-color: var(--info-fg);
		}

		&.surface {
			--button-bg: var(--surface-1);
			--button-color: var(--text-1);
		}

		&.link {
			--button-bg: transparent;
			--button-color: var(--primary-bg);
			padding: var(--button-padding-link);

			&:hover {
				background-color: transparent;
				text-decoration: underline;
			}
		}

		&.outline {
			background-color: transparent;
			color: var(--button-bg);

			&:hover:not(:disabled, .disabled) {
				background-color: var(--button-bg);
				border-color: var(--button-bg);
				color: var(--button-color);
			}
		}

		&.pill {
			border-radius: var(--radius-round);
		}

		&.icon {
			padding: var(--button-padding-icon);
		}

		&:disabled,
		&.disabled {
			opacity: 0.5;
			cursor: not-allowed;
		}

		&.block {
			display: block;
			width: 100%;
		}

		:global(.ph) {
			font-size: var(--font-size-4);
			display: block;
		}
	}
</style>
