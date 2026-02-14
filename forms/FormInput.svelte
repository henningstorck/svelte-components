<script lang="ts">
	import { getContext } from 'svelte';
	import type { FieldValuesContext } from './Form.svelte';

	interface Props {
		type?: string;
		name?: string;
		id?: string;
		value?: string | number;
		placeholder?: string;
		min?: number;
		max?: number;
		step?: number;
		required?: boolean;
		disabled?: boolean;
		readonly?: boolean;
	}

	let {
		type = 'text',
		name,
		id,
		value = $bindable(),
		placeholder,
		min,
		max,
		step,
		required = false,
		disabled = false,
		readonly = false
	}: Props = $props();

	let fieldValues = getContext<FieldValuesContext | undefined>('fieldValues');

	let fieldValue = $derived.by(() => {
		if (type === 'password') {
			return undefined;
		}

		if (name && fieldValues && fieldValues()[name] !== undefined) {
			return fieldValues()[name];
		}

		return value;
	});
</script>

<input
	class="form-input"
	{type}
	{name}
	{id}
	bind:value={fieldValue}
	{placeholder}
	{min}
	{max}
	{step}
	{required}
	{disabled}
	{readonly}
/>

<style>
	:where(:root) {
		--form-input-padding: var(--size-2);
		--form-input-bg: var(--surface-3);
		--form-input-border-color-focus: var(--text-1);
	}

	.form-input {
		padding: var(--form-input-padding);
		background-color: var(--form-input-bg);
		border: var(--border-size-2) solid var(--form-input-bg);
		transition: border-color 0.2s;
		width: 100%;

		&:focus-visible {
			outline: none;
			border-color: var(--form-input-border-color-focus);
		}
	}
</style>
