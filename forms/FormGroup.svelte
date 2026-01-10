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
	<label class="label" for={labelFor}>{label}</label>
	{@render children()}

	{#each relevantFieldErrors as fieldError (fieldError)}
		<div class="errors">{fieldError}</div>
	{/each}
</div>

<style>
	:where(.form-group) {
		--form-group-gap: var(--size-1);
	}

	.form-group {
		display: flex;
		flex-direction: column;
		gap: var(--form-group-gap);
		width: 100%;

		.label {
			font-weight: var(--font-weight-5);
		}

		.errors {
			color: var(--danger-bg);
		}
	}
</style>
