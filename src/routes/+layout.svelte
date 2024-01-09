<script lang="ts">
	import '../app.postcss';
	import { AppShell, initializeStores, Modal } from '@skeletonlabs/skeleton';
	initializeStores();
</script>

<Modal />
<AppShell>
	<slot />
</AppShell>