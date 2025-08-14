<script lang="ts">
	import type { Content } from '@prismicio/client';
	import { PrismicRichText, PrismicText, type SliceComponentProps } from '@prismicio/svelte';
	import clsx from 'clsx';

	import IconNpm from '~icons/fa6-brands/npm';
	import IconGithub from '~icons/fa6-brands/github';
	import IconFigma from '~icons/fa6-brands/figma';
	import IconFly from '~icons/fa6-brands/fly';
	import IconCloudflare from '~icons/fa6-brands/cloudflare';
	import IconDigitalOcean from '~icons/fa6-brands/digital-ocean';

	import background from './background.jpg';
	import Bounded from '$lib/components/Bounded.svelte';
	import LogoBackground from './LogoBackground.svelte';
	import StylizedLogoMark from './StylizedLogoMark.svelte';
	import Heading2 from '$lib/components/Heading2.svelte';

	const icons = {
		npm: IconNpm,
		github: IconGithub,
		figma: IconFigma,
		fly: IconFly,
		cloudflare: IconCloudflare,
		digitalocean: IconDigitalOcean
	};

	type Props = SliceComponentProps<Content.IntegrationsSlice>;

	const { slice }: Props = $props();
</script>

<Bounded
	data-slice-type={slice.slice_type}
	data-slice-variation={slice.variation}
	class="relative overflow-hidden"
>
	<img src={background} alt="" class="absolute inset-0 h-full w-full object-cover" />
	<LogoBackground />
	<div class="relative">
		<Heading2
			class="mx-auto mt-8 bg-gradient-to-b from-violet-50 to-violet-300 bg-clip-text py-2 text-transparent"
		>
			<PrismicText field={slice.primary.heading} />
		</Heading2>
		<div class="mx-auto mt-6 max-w-md text-center text-balance text-gray-300">
			<PrismicRichText field={slice.primary.body} />
		</div>

		<div class="mt-20 flex flex-col items-center md:flex-row">
			{#each slice.primary.items as item, index}
				{#if index === Math.floor(slice.primary.items.length / 2)}
					<StylizedLogoMark />
					<div class="signal-line rotate-180"></div>
				{/if}
				<div
					class="pulsing-icon flex aspect-square size-24 shrink-0 items-center justify-center rounded-full border border-violet-50/30 bg-violet-50/25 p-3 text-3xl text-violet-100 opacity-40 md:text-3xl lg:text-5xl"
				>
					{#if item.icon && icons[item.icon]}
						<!-- svelte-ignore svelte_component_deprecated -->
						<svelte:component this={icons[item.icon]} />
					{/if}
				</div>
				{#if index !== slice.primary.items.length - 1}
					<div
						class={clsx(
							'signal-line',
							index >= Math.floor(slice.primary.items.length / 2) ? 'rotate-180' : 'rotate-0'
						)}
					></div>
				{/if}
			{/each}
		</div>
	</div>
</Bounded>
