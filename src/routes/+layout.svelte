<script lang="ts">
	export const prerender = true;
</script>

<svelte:head>
	<title>karashiiro</title>
	<link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons" />
	<link
		rel="stylesheet"
		href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,600,700"
	/>
	<link rel="stylesheet" href="/smui.css" media="(prefers-color-scheme: light)" />
	<link rel="stylesheet" href="/smui-dark.css" media="screen and (prefers-color-scheme: dark)" />
</svelte:head>

<slot />

<style>
	:global(html) {
		font-family: 'Roboto', sans-serif;
	}
</style>
