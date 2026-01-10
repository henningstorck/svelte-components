<script lang="ts">
	import { getContext } from 'svelte';
	import type { FieldValuesContext } from './Form.svelte';

	interface Props {
		type: string;
		name?: string;
		id?: string;
		value?: string | number;
		options?: { [key: string]: string };
		placeholder?: string;
		min?: number;
		max?: number;
		step?: number;
		required?: boolean;
		disabled?: boolean;
		readonly?: boolean;
		checked?: boolean;
	}

	let {
		type,
		name,
		id,
		value = $bindable(),
		options = {},
		placeholder,
		min,
		max,
		step,
		required = false,
		disabled = false,
		readonly = false,
		checked = $bindable(false)
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

{#if type === 'textarea'}
	<textarea class="form-control" {name} {id} {placeholder} {required} {disabled} {readonly}>
		{fieldValue}
	</textarea>
{:else if type === 'select'}
	<select class="form-control" {name} {id} {placeholder} {required} {disabled}>
		{#each Object.entries(options) as option (option[0])}
			<option value={option[0]} selected={option[0] === fieldValue}>{option[1]}</option>
		{/each}
	</select>
{:else if type === 'checkbox'}
	<input
		class="form-control"
		type="checkbox"
		{name}
		{id}
		value={fieldValue}
		{required}
		{disabled}
		{readonly}
		bind:checked
	/>
{:else}
	<input
		class="form-control"
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
		{checked}
	/>
{/if}

<style>
	:where(.form-control) {
		--form-control-padding: var(--size-2);
		--form-control-bg: var(--surface-3);
		--form-control-border-color-focus: var(--text-1);
	}

	.form-control {
		padding: var(--form-control-padding);
		width: 100%;
		background-color: var(--form-control-bg);
		border: var(--border-size-2) solid var(--form-control-bg);
		transition: border-color 0.2s;

		&:focus-visible {
			outline: none;
			border-color: var(--form-control-border-color-focus);
		}
	}
</style>
