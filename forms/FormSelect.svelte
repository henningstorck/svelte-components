<script lang="ts">
	import { getContext } from 'svelte';
	import type { FieldValuesContext } from './Form.svelte';

	interface Props {
		name?: string;
		id?: string;
		value?: string | number;
		options?: { [key: string]: string };
		placeholder?: string;
		required?: boolean;
		disabled?: boolean;
	}

	let {
		name,
		id,
		value = $bindable(),
		options = {},
		placeholder,
		required = false,
		disabled = false
	}: Props = $props();

	let fieldValues = getContext<FieldValuesContext | undefined>('fieldValues');

	let fieldValue = $derived.by(() => {
		if (name && fieldValues && fieldValues()[name] !== undefined) {
			return fieldValues()[name];
		}

		return value;
	});
</script>

<select class="form-select" {name} {id} {placeholder} {required} {disabled}>
	{#each Object.entries(options) as option (option[0])}
		<option value={option[0]} selected={option[0] === fieldValue}>{option[1]}</option>
	{/each}
</select>

<style>
	:where(.form-select) {
		--form-select-padding: var(--size-2);
		--form-select-bg: var(--surface-3);
		--form-select-border-color-focus: var(--text-1);
	}

	.form-select {
		padding: var(--form-select-padding);
		background-color: var(--form-select-bg);
		border: var(--border-size-2) solid var(--form-select-bg);
		transition: border-color 0.2s;
		width: 100%;

		&:focus-visible {
			outline: none;
			border-color: var(--form-select-border-color-focus);
		}
	}
</style>
