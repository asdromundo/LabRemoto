<script lang="ts">
	import { description } from '$lib/config';
	import { pb } from '$lib/pb/pocketbase.svelte';
	import { LogIn } from 'lucide-svelte';
	let loggedIn = $derived(pb.authStoreIsValid());
</script>

<div class="pico container">
	<div class="container">
		<article class="grid">
			<div class="container">
				<hgroup>
					<h4>Facultad de Ingeniería, UNAM</h4>
					<h2>{description}</h2>
					<h3>Bienvenidos</h3>
				</hgroup>
				{#if !loggedIn}
					<p>Inicia sesión para ingresar a las prácticas.</p>
					<a href="/login" class="inline-flex items-center">
						Inicia sesión
						<LogIn class="w-4 h-4 ms-2" />
					</a>
				{:else if !pb.isRole('students')}
					<p></p>
					<p>Accede al panel de administrador para modificar a los usuarios</p>
					<p>O revisa la página de prácticas</p>

					<div class="text-center items-center">
						<a href="/practicas" class="secondary no-underline rounded-lg text-sm px-4 py-2"
							>Prácticas</a
						>
						<a href="/administrar" class="button no-underline rounded-lg text-sm px-4 py-2"
							>Admin Panel</a
						>
					</div>
				{:else}
					<p>Puedes reservar un horario o, si ya tienes uno, ingresar a la práctica.</p>

					<div class="text-center items-center">
						<a
							href="/practicas"
							class="text-white no-underline bg-red-700 hover:bg-red-800 focus:ring-4 focus:ring-red-300 font-medium rounded-lg text-sm px-5 py-2.5 dark:bg-red-600 dark:hover:bg-red-700 focus:outline-none dark:focus:ring-red-800"
							>Prácticas</a
						>
					</div>
				{/if}
			</div>

			<figure class="container text-center items-center my-auto">
				<enhanced:img
					src="$lib/assets/cover.jpg"
					alt="Laboratorio de Análisis de Sistemas y Señales. Imagen generada por IA."
					class="aspect-video object-cover"
				></enhanced:img>

				<figcaption>Imagen de Bing Image Generator.</figcaption>
			</figure>
		</article>
	</div>
</div>

<!-- svelte-ignore css_unused_selector -->
<style>
	article {
		border-radius: 1.5rem;
		background-image: '$lib/assets/cover.jpg';
	}

	img {
		display: inline;
	}

	article figure {
		margin: auto;
	}

	.button {
		background-color: var(--pico-primary-background);
		color: var(--pico-primary-inverse);
		display: inline-flex;
		align-items: center;
	}
	.button:hover {
		background-color: var(--pico-primary-hover-background);
		text-decoration: none;
	}

	.secondary {
		background-color: var(--pico-secondary-background);
		color: var(--pico-secondary-inverse);
		display: inline-flex;
		align-items: center;
	}

	.secondary:hover {
		background-color: var(--pico-primary-hover-background);
		text-decoration: none;
	}
</style>
