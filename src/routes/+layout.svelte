<script lang="ts">
	import favicon from "$lib/assets/favicon.svg";
	import { page } from "$app/state";

	let { children } = $props();

	const breadcrumbs = $derived(
		page.url.pathname
			.slice(1)
			.split("/")
			.map((segment, index, array) => {
				const name = segment;
				const href = "/" + array.slice(0, index + 1).join("/") || "/";
				return { name, href };
			}),
	);
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<header>
	<div class="breadcrumbs">
		<a href="/">~</a>
		{#each breadcrumbs as crumb}
			<span>/</span>
			<a href={crumb.href}>{crumb.name}</a>
		{/each}
	</div>

	<nav>
		<a href="/">Home</a>
		<a href="/projects">Projects</a>
		<a href="/posts">Posts</a>
	</nav>
</header>

<main>	
	{@render children()}
</main>

<footer></footer>

<style lang="scss" global>
	@use "$lib/styles/styles.scss";
	@use "$lib/styles/pallet.scss" as *;

	header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin: 1rem 0;

		.breadcrumbs {
			display: flex;
			gap: 0.5rem;

			a {
				text-decoration: none;
				color: $breadcrumb-color;

				&:hover {
					text-decoration: underline;
				}
			}
		}

		nav {
			display: flex;
			gap: 1.5rem;

			a {
				text-decoration: none;
				color: inherit;
			}
		}
	}

	footer {
		margin: 2rem 0;
	}
</style>
