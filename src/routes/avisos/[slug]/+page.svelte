<script lang="ts">
	import { formatDate } from '$lib/utils';

	interface Props {
		data: any;
	}

	let { data }: Props = $props();
</script>

<!-- SEO -->
<svelte:head>
	<title>{data.meta.title}</title>
	<meta property="og:type" content="article" />
	<meta property="og:title" content={data.meta.title} />
	<meta property="og:description" content={data.meta.description} />
</svelte:head>

<section class="pico container">
	<article>
		<!-- Title -->
		<hgroup>
			<h1>{data.meta.title}</h1>
			<p>Published at {formatDate(data.meta.date)}</p>
		</hgroup>

		<figure class="container text-center items-center my-auto">
			<img src={data.meta.thumbnail} alt={data.meta.title} class="aspect-video object-cover" />
		</figure>
		<!-- Tags -->
		<div class="tags">
			{#each data.meta.categories as category}
				<span class="surface-4">&num;{category}</span>
			{/each}
		</div>

		<!-- Post -->
		<div class="prose">
			<svelte:component this={data.content} />
		</div>
	</article>
</section>

<style>
	article {
		max-inline-size: var(--size-content-3);
		margin-inline: auto;
	}

	h1 {
		text-transform: capitalize;
	}

	h1 + p {
		margin-top: var(--size-2);
		color: var(--text-2);
	}

	.tags {
		display: flex;
		gap: var(--size-3);
		margin-top: var(--size-7);
	}

	.tags > * {
		padding: var(--size-2) var(--size-3);
		border-radius: var(--radius-round);
	}
</style>
