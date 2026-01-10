<script lang="ts">
	import { i18n } from '$lib/common/i18n/i18nService';
	import type { Snippet } from 'svelte';

	interface Props {
		children: Snippet;
		id: string;
		title?: string;
	}

	let { children, id, title }: Props = $props();
</script>

<dialog class="modal" {id}>
	{#if title}
		<div class="modal-title">
			{title}

			<button
				class="modal-close"
				command="request-close"
				commandfor={id}
				aria-label={i18n('common.close')}
			>
				<i class="ph ph-x"></i>
			</button>
		</div>
	{/if}

	<div class="modal-content">
		{@render children()}
	</div>
</dialog>

<style>
	:where(.modal) {
		--modal-margin: var(--size-5);
		--modal-padding: var(--size-5);
		--modal-bg: var(--surface-1);
		--modal-radius: var(--radius-2);
		--modal-max-width: 800px;
	}

	.modal {
		background-color: var(--modal-bg);
		border-radius: var(--modal-radius);
		padding: 0;
		width: 100%;
		max-width: var(--modal-max-width);

		&::backdrop {
			background-color: color-mix(in srgb, var(--body-bg) 80%, transparent 20%);
			backdrop-filter: blur(var(--size-1));
		}

		.modal-title {
			display: flex;
			flex-direction: row;
			align-items: center;
			justify-content: space-between;
			padding: var(--modal-padding);
			border-bottom: var(--border-size-2) solid var(--body-bg);
			font-weight: var(--font-weight-7);
			font-size: var(--font-size-3);

			.modal-close {
				background-color: transparent;
				padding: 0;
				font-size: var(--font-size-4);

				.ph {
					display: block;
				}
			}
		}

		.modal-content {
			padding: var(--modal-padding);
		}
	}
</style>
