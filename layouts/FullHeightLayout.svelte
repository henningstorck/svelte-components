<script lang="ts">
	import type { Snippet } from 'svelte';

	interface Props {
		children: Snippet;
		justify?: 'space-between' | 'start' | 'center' | 'end';
		backgroundImage?: string;
	}

	let { children, justify = 'space-between', backgroundImage }: Props = $props();
</script>

<div
	class="full-height-layout"
	class:justify-space-between={justify === 'space-between'}
	class:justify-start={justify === 'start'}
	class:justify-center={justify === 'center'}
	class:justify-end={justify === 'end'}
	style={backgroundImage ? `background-image: url('${backgroundImage}');` : undefined}
>
	{@render children()}
</div>

<style>
	.full-height-layout {
		min-height: 100dvh;
		display: flex;
		flex-direction: column;
		background-repeat: no-repeat;
		background-position: center center;
		background-size: cover;

		&.justify-space-between {
			justify-content: space-between;
		}

		&.justify-start {
			justify-content: start;
		}

		&.justify-center {
			justify-content: center;
		}

		&.justify-end {
			justify-content: end;
		}
	}
</style>
