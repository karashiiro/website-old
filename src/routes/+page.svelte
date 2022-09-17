<script lang="ts">
	import Project from '$lib/components/Project.svelte';
	import LayoutGrid, { Cell } from '@smui/layout-grid';
	import { onMount } from 'svelte';

	const socials = {
		github: 'https://github.com/karashiiro',
		twitter: 'https://twitter.com/karashiiro1',
		kofi: 'https://ko-fi.com/karashiiro'
	};

	let projects: { title: string; description: string; url: string }[] = [];

	const projectRegex = /\[(?<title>[^\]]+)\]\((?<url>[^\)]+)\)\|(?<description>[^\|]+)/;
	const linkRegex = /\[(?<text>[^\]]+)\]\((?<url>[^\)]+)\)/;

	function stripLinks(text: string): string {
		const m = text.match(linkRegex);
		if (m?.groups != null) {
			text = text.replace(`[${m.groups['text']}](${m.groups['url']})`, m.groups['text']);

			return stripLinks(text);
		}

		return text;
	}

	async function getProjects() {
		return fetch('https://raw.githubusercontent.com/karashiiro/karashiiro/master/README.md')
			.then((res) => res.text())
			.then((data) => {
				const lines = data.split('\n');
				const projects: { title: string; description: string; url: string }[] = [];
				for (const line of lines) {
					if (!line.startsWith('[')) {
						continue;
					}

					const matches = line.match(projectRegex);
					if (matches?.groups != null) {
						projects.push({
							title: matches.groups['title'],
							description: stripLinks(matches.groups['description']),
							url: matches.groups['url']
						});
					}
				}

				return projects;
			});
	}

	onMount(async () => {
		projects = await getProjects();
	});
</script>

<main>
	<LayoutGrid>
		<Cell span={3}>
			<img
				alt="Avatar"
				class="pfp"
				src="https://avatars.githubusercontent.com/u/49822414?v=4"
			/></Cell
		>
		<Cell span={9}>
			<div class="cell">
				<div>
					<h6 class="title">karashiiro</h6>
					<div class="socials">
						<span><a href={socials.github}>GitHub</a></span>
						<span><a href={socials.twitter}>Twitter</a></span>
						<span><a href={socials.kofi}>Ko-fi</a></span>
					</div>
				</div>
			</div>
		</Cell>
		{#each projects as project}
			<Cell span={3}>
				<Project {...project} />
			</Cell>
		{/each}
	</LayoutGrid>
</main>

<style>
	.title {
		font-size: 24pt;
		font-weight: 100;
	}

	.socials span {
		margin-right: 30px;
	}

	.cell {
		height: 60px;
		display: flex;
		align-items: center;
	}

	.pfp {
		height: 200px;
		width: 200px;
		border: 6px solid var(--mdc-theme-primary, #ff3e00);
		border-radius: 100%;
	}

	main {
		width: 74%;
		margin: auto;
	}
</style>
