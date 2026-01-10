<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children: Snippet;
	}

	let { children }: Props = $props();
</script>

<div class="form-actions">
	{@render children()}
</div>

<style>
	:where(.form-actions) {
		--form-actions-margin: var(--size-5);
	}

	.form-actions {
		margin-top: var(--form-actions-margin);
	}
</style>
