<script lang="ts">
	import Bounded from '$lib/components/Bounded.svelte';
	import Heading2 from '$lib/components/Heading2.svelte';
	import type { Content } from '@prismicio/client';
	import {
		PrismicImage,
		PrismicLink,
		PrismicRichText,
		PrismicText,
		type SliceComponentProps
	} from '@prismicio/svelte';
	import clsx from 'clsx';

	type Props = SliceComponentProps<Content.CaseStudiesSlice>;

	const { slice }: Props = $props();
	/** @type {import("@prismicio/client").Content.CaseStudyDocument[]}
	 */
	const caseStudies: import('@prismicio/client').Content.CaseStudyDocument[] = [];
</script>

<Bounded data-slice-type={slice.slice_type} data-slice-variation={slice.variation}>
	<Heading2>
		<PrismicText field={slice.primary.heading} />
	</Heading2>
	<div class="mx-auto mt-6 max-w-md text-center text-balance text-gray-300">
		<PrismicRichText field={slice.primary.body} />
	</div>
	<div class="mt-20 grid gap-16">
		{#each slice.primary.repeatable_zone as item, index}
			<div
				class="group relative grid gap-4 opacity-85 transition-opacity duration-300 hover:cursor-pointer hover:opacity-100 md:grid-cols-2 md:gap-8 lg:grid-cols-3"
			>
				<div class="col-span-1 flex flex-col justify-center gap-4">
					<h3 class="text-4xl">
						<PrismicText field={item.case_study.data.company} />
					</h3>
					<div class="max-w-md">
						<PrismicRichText field={item.case_study.data.description} />
					</div>
					<PrismicLink
						field={item.case_study}
						class="z-10 after:absolute after:inset-0 hover:underline"
						>Read <PrismicText field={item.case_study.data.company} /> case study
					</PrismicLink>
				</div>
				<div class={clsx('relative lg:col-span-2', index % 2 && 'md:-order-1')}>
					<div class="image-glow -bottom-8 -left-4 bg-orange-500"></div>
					<div class="image-glow -top-8 -right-4 bg-violet-500"></div>

					<PrismicImage
						field={item.case_study.data.image}
						sizes="(max-width: 768px) 100vw, 50vw"
						class="z-20 scale-[.98] rounded-xl transition-transform duration-300 group-hover:scale-100"
					/>
				</div>
			</div>
		{/each}
	</div>
</Bounded>

<style>
	.image-glow {
		@apply absolute h-1/2 w-1/2 rounded-full opacity-0 mix-blend-screen transition-opacity duration-500 group-hover:opacity-30;
		filter: blur(64px);
	}
</style>
