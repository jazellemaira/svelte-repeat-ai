<script>
	import clsx from 'clsx';

	/** @type {string | undefined} */
	let className = undefined;
	export { className as class };
</script>

<h2 class={clsx('max-w-3xl text-center text-5xl font-medium text-balance md:text-7xl', className)}>
	<slot />
</h2>
