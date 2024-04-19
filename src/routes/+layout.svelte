<script>
	import { page } from '$app/stores';
	import { fade, fly } from 'svelte/transition';
	import '../app.pcss';
	let pages = ['Login', 'Sign Up', 'Create Quiz', 'My Quizes', 'Dashboard', 'Quizes'];
	let open = false;
	function show() {
		open = !open;
	}
</script>

<nav>
	<div class="flex h-24 items-center justify-between px-4 py-2">
		<a href="/" class="flex items-center">
			<img src="/logo.png" alt="Logo" class=" h-24 pr-2" />
			<span class="  pb-1 text-4xl font-bold">The Web</span>
		</a>
		<div>
			<ul class="flex flex-row-reverse gap-x-4 max-xl:hidden">
				{#each pages as pageName}
					<li>
						<a
							href={'/' + pageName.toLowerCase().replaceAll(' ', '')}
							class={'pb-1 text-3xl font-semibold hover:text-violet-700 ' +
								($page.url.pathname == '/' + pageName.toLowerCase().replaceAll(' ', '')
									? 'text-violet-700'
									: '')}>{pageName}</a
						>
					</li>
				{/each}
			</ul>
		</div>
		<button on:click={show} class="pr-2 xl:hidden">
			<div class=" mb-1 h-1 w-6 rounded-full bg-white"></div>
			<div class="h-1 w-6 rounded-full bg-white"></div>
			<div class="mt-1 h-1 w-6 rounded-full bg-white"></div>
		</button>
		{#if open}
			<dialog
				transition:fly={{ y: -500, duration: 1000, x: 500 }}
				{open}
				class={' z-20 mt-96 rounded-lg border-4 border-sky-950  bg-slate-700 px-8  text-white xl:hidden'}
			>
				<ul class="flex flex-col-reverse gap-y-4 py-4 text-xl font-semibold">
					{#each pages as pageName}
						<li>
							<a
								on:click={show}
								href={pageName.toLowerCase().replaceAll(' ', '') == 'quizes'
									? '/'
									: '/' + pageName.toLowerCase().replaceAll(' ', '')}
								class={'hover:text-violet-700 ' +
									($page.url.pathname == '/' + pageName.toLowerCase().replaceAll(' ', '') ||
									(pageName.toLowerCase().replaceAll(' ', '') == 'quizes' &&
										$page.url.pathname == '/')
										? 'text-violet-700'
										: '')}>{pageName}</a
							>
						</li>
					{/each}
				</ul>
			</dialog>
		{/if}
	</div>
</nav>

<slot></slot>
