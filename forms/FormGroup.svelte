<script lang="ts">
	import { getContext, type Snippet } from 'svelte';
	import type { FieldErrorsContext } from './Form.svelte';

	interface Props {
		children: Snippet;
		label: string;
		labelFor: string;
		name: string;
	}

	let { children, label, labelFor, name }: Props = $props();

	let fieldErrors = getContext<FieldErrorsContext | undefined>('fieldErrors');

	let relevantFieldErrors = $derived.by(() => {
		if (!fieldErrors) {
			return [];
		}

		return fieldErrors()[name];
	});
</script>

<div class="form-group">
	<label class="form-group-label" for={labelFor}>{label}</label>
	{@render children()}

	{#each relevantFieldErrors as fieldError (fieldError)}
		<div class="form-group-errors">{fieldError}</div>
	{/each}
</div>

<style>
	:where(:root) {
		--form-group-gap: var(--size-1);
	}

	.form-group {
		display: flex;
		flex-direction: column;
		gap: var(--form-group-gap);
		width: 100%;

		.form-group-label {
			font-weight: var(--font-weight-5);
		}

		.form-group-errors {
			color: var(--danger-bg);
		}
	}
</style>
