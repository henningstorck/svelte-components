<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children: Snippet;
	}

	let { children }: Props = $props();
</script>

<table class="table">
	{@render children()}
</table>

<style>
	:where(.table) {
		--table-padding: var(--size-3) var(--size-5);
		--table-radius: var(--radius-2);
		--table-margin: var(--size-7);
		--table-bg: var(--surface-1);
	}

	.table {
		--nice-inner-radius: 0;

		width: 100%;
		border-radius: var(--table-radius);
		border-collapse: collapse;
		border: none;
		overflow: hidden;
		box-shadow: var(--shadow-3);
		margin-block: var(--table-margin);

		:global(th),
		:global(td) {
			padding: var(--table-padding);
			background-color: var(--table-bg);

			&:not([align]) {
				text-align: start;
			}
		}

		:global(th) {
			font-weight: var(--font-weight-8);
		}

		:global(td) {
			border-top: var(--border-size-2) solid var(--body-bg);
		}
	}
</style>
