<script lang="ts">
	import { resolve } from '$app/paths';
	import type { Snippet } from 'svelte';

	interface Props {
		start?: Snippet;
		end?: Snippet;
		children?: Snippet;
		title?: string;
		logo?: string;
		toggleNavigationMessage: string;
	}

	let { start, end, children, title, logo, toggleNavigationMessage }: Props = $props();
	let expanded = $state(false);

	const toggle = () => {
		expanded = !expanded;
	};
</script>

<header class="header" class:align-baseline={!logo} class:align-center={!!logo}>
	{#if logo}
		<h1 class="header-logo">
			<a href={resolve('/')}>
				<img src={logo} alt={title} />
			</a>
		</h1>
	{:else}
		<h1 class="header-title"><a href={resolve('/')}>{title}</a></h1>
	{/if}

	<button class="header-toggle" title={toggleNavigationMessage} onclick={toggle}>
		{#if expanded}
			<i class="ph ph-x"></i>
		{:else}
			<i class="ph ph-list"></i>
		{/if}
	</button>

	{#if start}
		<div class="header-start" aria-expanded={expanded}>
			{@render start()}
		</div>
	{/if}

	{#if end}
		<div class="header-end" aria-expanded={expanded}>
			{@render end()}
		</div>
	{:else if children}
		<div class="header-end" aria-expanded={expanded}>
			{@render children()}
		</div>
	{/if}
</header>

<style>
	:where(.header) {
		--header-padding: var(--size-5);
		--header-gap: var(--size-7);
		--header-logo-height: var(--size-10);
	}

	.header {
		padding: var(--header-padding);
		display: grid;
		gap: 0 var(--header-gap);
		grid-template-areas: 'title start end';
		grid-template-columns: auto 1fr auto;

		&.align-baseline {
			align-items: baseline;
		}

		&.align-center {
			align-items: center;
		}

		.header-title {
			grid-area: title;
			font-weight: var(--font-weight-9);
			font-size: var(--font-size-4);
			text-align: left;

			a {
				color: var(--text-1);
				text-decoration: none;
			}
		}

		.header-toggle {
			display: none;
			grid-area: toggle;
			background-color: transparent;
			padding: 0;
			font-size: var(--font-size-4);

			.ph {
				display: block;
			}
		}

		.header-logo {
			img {
				display: block;
				height: var(--header-logo-height);
			}
		}

		.header-start {
			grid-area: start;
		}

		.header-end {
			grid-area: end;
		}

		@media (max-width: 1000px) {
			grid-template-areas:
				'title toggle'
				'start start'
				'end end';
			grid-template-columns: 1fr auto;
			text-align: center;

			.header-toggle {
				display: block;
			}

			.header-start,
			.header-end {
				display: none;
				margin-top: var(--header-gap);

				&[aria-expanded='true'] {
					display: block;
				}
			}
		}
	}
</style>
