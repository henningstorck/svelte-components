<script lang="ts">
	import { setContext, type Snippet } from 'svelte';

	export type FieldValues = { [key: string]: unknown };
	export type FieldErrors = { [key: string]: string[] };

	export type FieldValuesContext = () => FieldValues;
	export type FieldErrorsContext = () => FieldErrors;

	interface Props {
		children: Snippet;
		method: 'post' | 'get';
		action?: string;
		fieldValues?: FieldValues;
		fieldErrors?: FieldErrors;
	}

	let { children, method, action, fieldValues, fieldErrors }: Props = $props();

	setContext<FieldValuesContext>('fieldValues', () => fieldValues || {});
	setContext<FieldErrorsContext>('fieldErrors', () => fieldErrors || {});
</script>

<form {method} {action}>
	{@render children()}
</form>
