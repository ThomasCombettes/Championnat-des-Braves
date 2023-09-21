<script lang="ts">
	import '../app.postcss';
	import { AppShell, AppBar } from '@skeletonlabs/skeleton';
</script>

<!-- App Shell -->
<AppShell>
	<svelte:fragment slot="header">
		<!-- App Bar -->
		<AppBar>
			<svelte:fragment slot="lead">
				<strong class="text-xl uppercase">Championnat des Braves</strong>
			</svelte:fragment>

			
			<svelte:fragment slot="trail">
				<a
					class="btn btn-sm variant-ghost-surface"
					href="https://discord.gg/EXqV7W8MtY"
					target="_blank"
					rel="noreferrer"
				>
					Discord M2
				</a>
				<a
					class="btn btn-sm variant-ghost-surface"
					href="https://github.com/ThomasCombettes/Championnat-des-Braves"
					target="_blank"
					rel="noreferrer"
				>
					GitHub
				</a>
			</svelte:fragment>
		</AppBar>
	</svelte:fragment>

	<svelte:fragment slot="sidebarLeft">
		<div id="tab">

			<nav class="list-nav">
				<!-- (optionally you can provide a label here) -->
				<ul>
					<li>
						<a href="/elements/lists">
							<span class="badge bg-primary-500">💀</span>
							<span class="flex-auto">guerre d'homme</span>
						</a>
					</li>
					<li>
						<a href="/elements/lists">
							<span class="badge bg-primary-500">~</span>
							<span class="flex-auto">à venir</span>
						</a>
					</li>
				</ul>
			</nav>
		</div>
	</svelte:fragment>
	
	<slot />
</AppShell>



<style>
	#tab{
		border-color: red;
		border-width: 5px;
		padding: 40;
	}
</style>