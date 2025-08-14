<script lang="ts">
	import { SliceZone } from '@prismicio/svelte';
	import type { PageProps } from './$types';

	import { components } from '$lib/slices';

	const { data }: PageProps = $props();
</script>

<SliceZone slices={data.slices} {components} />
<!-- Render the slices of the page 
Match the slices with the components defined in $lib/slices -->
