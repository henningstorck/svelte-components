<script lang="ts">
	import Button from './Button.svelte';

	interface Props {
		value: string;
		textCopy: string;
		textCopied: string;
		iconCopy?: string;
		iconCopied?: string;
		resetTimeout?: number;
	}

	let {
		value,
		textCopy,
		textCopied,
		iconCopy = 'ph ph-clipboard',
		iconCopied = 'ph ph-check',
		resetTimeout = 2000
	}: Props = $props();
	let copied = $state(false);

	const handleClick = () => {
		navigator.clipboard.writeText(value);
		copied = true;

		setTimeout(() => {
			copied = false;
		}, resetTimeout);
	};
</script>

<Button onclick={handleClick}>
	{#if copied}
		{#if iconCopied}
			<i class={iconCopied}></i>
		{/if}

		{textCopied}
	{:else}
		{#if iconCopy}
			<i class={iconCopy}></i>
		{/if}

		{textCopy}
	{/if}
</Button>
