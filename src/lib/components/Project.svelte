<script lang="ts">
	import Card, { Content, Actions } from '@smui/card';
	import { Label } from '@smui/common';
	import Button from '@smui/button';

	export let title: string;
	export let description: string;
	export let url: string;
</script>

<Card variant="outlined" padded>
	<div class="project">
		<div class="project-content">
			<Content>
				<h2 class="title" style="margin: 0;">{title}</h2>
				<div class="gap" />
				<span>{description}</span>
			</Content>
		</div>
		<div class="project-gap" />
		<div class="project-actions">
			<Actions fullBleed>
				<a href={url}>
					<Button>
						<Label>Go to project</Label>
						<i class="material-icons" aria-hidden="true">arrow_forward</i>
					</Button>
				</a>
			</Actions>
		</div>
	</div>
</Card>

<style>
	.gap {
		height: 12px;
	}

	.title {
		font-weight: 400;
	}

	.project {
		display: grid;
		height: 300px;
		grid-template-rows: 1fr 1fr auto;
	}

	.project-content {
		grid-row: 1;
		word-break: break-word;
		max-height: 220px;
	}

	.project-gap {
		grid-row: auto;
	}

	.project-actions {
		grid-row: 3;
	}
</style>
