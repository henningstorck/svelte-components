<script lang="ts">
	interface Props {
		value: number;
		min?: number;
		max?: number;
		showPercentage?: boolean;
	}

	let { value, min = 0, max = 100, showPercentage = false }: Props = $props();
</script>

<div class="progress-wrapper">
	<div class="progress">
		<div
			class="progress-bar"
			style="width: {(Math.min(Math.max(value, min), max) / max) * 100}%"
		></div>
	</div>

	{#if showPercentage}
		<div class="progress-percentage">
			{Math.round((Math.min(Math.max(value, min), max) / max) * 100)}%
		</div>
	{/if}
</div>

<style>
	:where(.progress) {
		--progress-bg: var(--surface-3);
		--progress-bar-bg: var(--primary-bg);
	}

	.progress-wrapper {
		display: flex;
		flex-direction: row;
		align-items: center;
		gap: var(--size-3);
	}

	.progress {
		background-color: var(--progress-bg);
		border-radius: var(--radius-round);
		width: 100%;
		height: var(--size-3);
		overflow: hidden;
	}

	.progress-bar {
		background-color: var(--progress-bar-bg);
		height: 100%;
	}

	.progress-percentage {
		width: var(--size-8);
		text-align: right;
	}
</style>
