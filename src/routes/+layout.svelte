<script lang="ts">
	import { enhance } from '$app/forms';
	import { page } from '$app/stores';

	import type { SubmitFunction } from './$types';

	import '../app.postcss';
	import { themes } from './themes';

	const submitUpdateTheme: SubmitFunction = ({ action }) => {
		const theme = action.searchParams.get('theme');

		if (theme) {
			document.documentElement.setAttribute('data-theme', theme);
		}
	};

</script>

<div class="bg-base-300 min-h-full">
	<div class="navbar bg-base-100 px-6">
		<div class="flex-1">
			<a href="/" class="font-bold text-xl">SvelteKit Theme Switching</a>
		</div>
		<div class="flex-none">
			<ul class="menu menu-horizontal px-1 z-50">
				<li>
					<button> Set Theme 🎨 </button>
					<ul class="p-2 bg-base-100 w-full max-h-96 overflow-y-scroll">
						<form method="POST" use:enhance={submitUpdateTheme}>
							{#each themes as theme}
								<li>
									<button formaction="/?/setTheme&theme={theme}&redirectTo={$page.url.pathname}"
										>{theme}</button
									>
								</li>
							{/each}
						</form>
					</ul>
				</li>
			</ul>
		</div>
	</div>
	<slot />
</div>
