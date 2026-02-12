<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children: Snippet;
		color?: 'primary' | 'secondary' | 'success' | 'danger' | 'warning' | 'info';
	}

	let { children, color }: Props = $props();
</script>

<span class="badge {color}">
	{@render children()}
</span>

<style>
	.badge {
		background-color: var(--badge-bg);
		color: var(--badge-fg);
		padding: var(--size-1) var(--size-3);
		font-size: var(--font-size-0);
		text-transform: uppercase;
		border-radius: var(--radius-round);

		&.primary {
			--badge-bg: var(--primary-bg);
			--badge-fg: var(--primary-fg);
		}

		&.secondary {
			--badge-bg: var(--secondary-bg);
			--badge-fg: var(--secondary-fg);
		}

		&.success {
			--badge-bg: var(--success-bg);
			--badge-fg: var(--success-fg);
		}

		&.danger {
			--badge-bg: var(--danger-bg);
			--badge-fg: var(--danger-fg);
		}

		&.warning {
			--badge-bg: var(--warning-bg);
			--badge-fg: var(--warning-fg);
		}

		&.info {
			--badge-bg: var(--info-bg);
			--badge-fg: var(--info-fg);
		}
	}
</style>
