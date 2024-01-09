<!-- YOU CAN DELETE EVERYTHING IN THIS PAGE -->
<script lang="ts">
	import { dinero } from 'dinero.js';
	import { getModalStore } from '@skeletonlabs/skeleton';
	import type { ModalComponent, ModalSettings } from '@skeletonlabs/skeleton';
	import UserForm from '$lib/components/UserForm.svelte';
	interface User { name: string, incomePerAnnum: number };
	let users: User[] = []
			
	const modalStore = getModalStore();
	const modalComponent: ModalComponent = { ref: UserForm };
	const modal: ModalSettings = {
		type: 'component',
		component: modalComponent,
		response: (val: User) => {
			if (val) {
				users = [...users, val]
			}
		}
	}

	function onAddUser() {
		modalStore.trigger(modal);
	}
	modalStore.trigger(modal);
	
</script>
<div class="container h-full mx-auto flex justify-center items-center">
	{#each users as user}
		<div>
			<span>{user.name}</span>
		</div>
	{/each}
	<button class="btn variant-filled" on:click={onAddUser}>Add User</button>
</div>
