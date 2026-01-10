<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children: Snippet;
	}

	let { children }: Props = $props();
</script>

<section class="section">
	{@render children()}
</section>

<style>
	:where(.section) {
		--section-margin: var(--size-9);
	}

	.section {
		margin-block: var(--section-margin);
	}
</style>
