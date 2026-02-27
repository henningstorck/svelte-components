<script lang="ts">
	import { getContext } from 'svelte';
	import type { FieldValuesContext } from './Form.svelte';

	interface Props {
		name?: string;
		id?: string;
		value?: string | number;
		placeholder?: string;
		required?: boolean;
		disabled?: boolean;
		readonly?: boolean;
	}

	let {
		name,
		id,
		value = $bindable(),
		placeholder,
		required = false,
		disabled = false,
		readonly = false
	}: Props = $props();

	let fieldValues = getContext<FieldValuesContext | undefined>('fieldValues');

	let fieldValue = $derived.by(() => {
		if (name && fieldValues && fieldValues()[name] !== undefined) {
			return fieldValues()[name];
		}

		return value;
	});
</script>

<!-- prettier-ignore -->
<textarea class="form-textarea" {name} {id} {placeholder} {required} {disabled} {readonly}>{fieldValue}</textarea>

<style>
	:where(:root) {
		--form-textarea-padding: var(--size-2);
		--form-textarea-bg: var(--surface-3);
		--form-textarea-border-color-focus: var(--text-1);
	}

	.form-textarea {
		padding: var(--form-textarea-padding);
		background-color: var(--form-textarea-bg);
		border: var(--border-size-2) solid var(--form-textarea-bg);
		transition: border-color 0.2s;
		width: 100%;
		min-height: var(--size-11);

		&:focus-visible {
			outline: none;
			border-color: var(--form-textarea-border-color-focus);
		}
	}
</style>
