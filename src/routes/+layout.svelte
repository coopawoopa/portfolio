<script lang="ts">
	import { ModeWatcher } from 'mode-watcher';
	import '../app.css';
</script>

<svelte:head>
	<meta name="viewport" content="width=767px" />
</svelte:head>
<ModeWatcher defaultMode="dark" />
<slot />
