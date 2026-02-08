<script lang="ts">
	import { getContext } from 'svelte';
	import type { FieldValuesContext } from './Form.svelte';

	interface Props {
		name?: string;
		id?: string;
		required?: boolean;
		disabled?: boolean;
		readonly?: boolean;
		checked?: boolean;
	}

	let {
		name,
		id,
		required = false,
		disabled = false,
		readonly = false,
		checked = $bindable(false)
	}: Props = $props();

	let fieldValues = getContext<FieldValuesContext | undefined>('fieldValues');

	let fieldChecked = $derived.by(() => {
		if (name && fieldValues && fieldValues()[name] !== undefined) {
			return !!fieldValues()[name];
		}

		return checked;
	});
</script>

<input
	class="form-checkbox"
	type="checkbox"
	{name}
	{id}
	value="on"
	{required}
	{disabled}
	{readonly}
	bind:checked={fieldChecked}
/>
