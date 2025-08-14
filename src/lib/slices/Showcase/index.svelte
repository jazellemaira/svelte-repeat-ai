<script lang="ts">
	import Bounded from '$lib/components/Bounded.svelte';
	import ButtonLink from '$lib/components/ButtonLink.svelte';
	import Heading2 from '$lib/components/Heading2.svelte';
	import type { Content } from '@prismicio/client';
	import {
		PrismicImage,
		PrismicRichText,
		PrismicText,
		type SliceComponentProps
	} from '@prismicio/svelte';
	import clsx from 'clsx';
	import IconGear from '~icons/ph/gear';
	import IconCycle from '~icons/ph/arrows-clockwise';

	type Props = SliceComponentProps<Content.ShowcaseSlice>;

	const { slice }: Props = $props();

	const icons = {
		gear: IconGear,
		cycle: IconCycle
	};
</script>

<Bounded data-slice-type={slice.slice_type} data-slice-variation={slice.variation} class="relative">
	<div
		class="absolute -z-10 aspect-video w-full max-w-2xl rounded-full bg-violet-500/40 mix-blend-screen blur-[120px] filter"
	></div>
	{#if slice.primary.heading}
		<Heading2>
			<PrismicText field={slice.primary.heading} />
		</Heading2>
	{/if}
	<div
		class="relative mt-16 grid items-center gap-8 rounded-xl border border-violet-50/20 bg-gradient-to-b from-gray-50/15 to-gray-50/5 p-8 backdrop-blur-sm lg:grid-cols-3 lg:gap-0 lg:py-12"
	>
		<div class="grid-background"></div>
		<div>
			{#if slice.primary.icon}
				<div class="w-fit rounded-lg bg-violet-800 p-4 text-3xl">
					<svelte:component this={icons[slice.primary.icon]} />
				</div>
			{/if}
			{#if slice.primary.subheading}
				<h3 class="mt-6 text-2xl font-normal">
					<PrismicText field={slice.primary.subheading} />
				</h3>
			{/if}
			{#if slice.primary.body}
				<div class="prose prose-invert mt-4 max-w-xl">
					<PrismicRichText field={slice.primary.body} />
				</div>
			{/if}
			{#if slice.primary.button_link}
				<ButtonLink field={slice.primary.button_link} class="mt-6">
					{slice.primary.button_text || 'Learn more'}
				</ButtonLink>
			{/if}
		</div>
		{#if slice.primary.image}
			<PrismicImage
				field={slice.primary.image}
				class={clsx(
					'opacity-90 shadow-2xl lg:col-span-2 lg:pt-0',
					slice.variation === 'reverse'
						? 'lg:order-1 lg:translate-x-[15%]'
						: 'lg:-order-1 lg:translate-x-[-15%]'
				)}
				sizes="(max-width: 768px) 100vw, 50vw"
			/>
		{/if}
	</div>
</Bounded>

<style>
	.grid-background {
		background-image: url('/assets/grid-pattern.png');
		position: absolute;
		inset: 0;
		background-repeat: repeat;
		background-position: center;
		mask-image: radial-gradient(circle at 60% 50%, black 10%, transparent 40%);
		opacity: 0.15;
		z-index: -1;
	}
</style>
