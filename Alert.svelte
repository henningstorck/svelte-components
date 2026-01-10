<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children: Snippet;
		level: 'success' | 'danger' | 'warning' | 'info';
		noIcon?: boolean;
	}

	let { children, level, noIcon = false }: Props = $props();

	const icon = {
		success: 'ph-check-circle',
		danger: 'ph-warning-circle',
		warning: 'ph-warning',
		info: 'ph-info'
	};
</script>

<div class="alert {level}">
	{#if !noIcon}
		<div class="alert-icon">
			<i class="ph {icon[level]}"></i>
		</div>
	{/if}

	<div class="alert-message">
		{@render children()}
	</div>
</div>

<style>
	:where(.alert) {
		--alert-margin: var(--size-5);
		--alert-padding: var(--size-3);
		--alert-gap: var(--size-3);
		--alert-radius: var(--radius-2);
	}

	.alert {
		margin-block: var(--alert-margin);
		display: flex;
		flex-direction: row;
		align-items: center;
		gap: var(--alert-gap);
		padding: var(--alert-padding);
		border-radius: var(--alert-radius);
		font-weight: var(--font-weight-5);

		&.success {
			background-color: var(--success-bg);
			color: var(--success-fg);
		}

		&.danger {
			background-color: var(--danger-bg);
			color: var(--danger-fg);
		}

		&.warning {
			background-color: var(--warning-bg);
			color: var(--warning-fg);
		}

		&.info {
			background-color: var(--info-bg);
			color: var(--info-fg);
		}

		.alert-icon {
			font-size: var(--font-size-5);

			.ph {
				display: block;
			}
		}
	}
</style>
