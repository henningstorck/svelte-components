<script lang="ts">
	interface Props {
		title?: string;
	}

	let { title }: Props = $props();
</script>

<div class="separator">{title}</div>

<style>
	:where(:root) {
		--separator-margin: var(--size-5);
		--separator-fg: var(--surface-4);
	}

	.separator {
		display: flex;
		flex-direction: row;
		align-items: center;
		gap: var(--size-3);
		margin-block: var(--separator-margin);
		text-align: center;
		color: var(--separator-fg);
		text-transform: uppercase;

		&:before,
		&:after {
			display: block;
			content: '';
			height: var(--border-size-2);
			background-color: var(--separator-fg);
			flex: 1 1 0;
		}
	}
</style>
