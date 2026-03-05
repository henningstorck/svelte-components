<script lang="ts">
	interface Props {
		title: string;
		delay?: string;
		takesLongerTitle: string;
		takesLongerDelay?: string;
	}

	let { title, delay = '0.5s', takesLongerTitle, takesLongerDelay = '8s' }: Props = $props();
</script>

<div class="loading-indicator" style:--delay={delay} style:--takes-longer-delay={takesLongerDelay}>
	<div class="spinner"></div>
	<div class="title">{title}</div>
	<div class="takes-longer">{takesLongerTitle}</div>
</div>

<style>
	@keyframes fade-in {
		0% {
			opacity: 0;
		}
		100% {
			opacity: 1;
		}
	}

	@keyframes spinner {
		33% {
			border-radius: 0;
			clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
		}
		66% {
			border-radius: 0;
			clip-path: polygon(50% 0, 50% 0, 100% 100%, 0 100%);
		}
	}

	.loading-indicator {
		text-align: center;
		margin-block: var(--size-5);
		opacity: 0;
		animation-name: fade-in;
		animation-duration: 0.2s;
		animation-delay: var(--delay);
		animation-fill-mode: forwards;
	}

	.spinner {
		width: var(--size-8);
		aspect-ratio: 1;
		border-radius: 50%;
		background: var(--text-1);
		clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
		animation-name: spinner;
		animation-duration: 2s;
		animation-timing-function: cubic-bezier(0.3, 1, 0, 1);
		animation-iteration-count: infinite;
		margin-inline: auto;
		margin-bottom: var(--size-3);
	}

	.title {
		font-size: var(--font-size-5);
		font-weight: var(--font-weight-7);
	}

	.takes-longer {
		font-size: var(--font-size-3);
		font-weight: var(--font-weight-2);
		opacity: 0;
		animation-name: fade-in;
		animation-duration: 0.2s;
		animation-delay: var(--takes-longer-delay);
		animation-fill-mode: forwards;
	}
</style>
