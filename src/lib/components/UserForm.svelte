<script lang="ts">
    import type { SvelteComponent } from 'svelte';
    import { getModalStore, RadioGroup, RadioItem } from '@skeletonlabs/skeleton';
    export let parent: SvelteComponent;

    const formData = {
        name: '',
        incomeValue: 0,
        incomeType: 'annum'
    }

    const modalStore = getModalStore();

    function onFormSubmit(): void {
		if ($modalStore[0].response) {
            const incomePerAnnum = formData.incomeType === 'annum' ? formData.incomeValue : formData.incomeValue * 12
            $modalStore[0].response({ name: formData.name, incomePerAnnum });
        }
		modalStore.close();
	}
</script>
<div class="card p-4 w-modal shadow-xl space-y-4">
    <form class="modal-form p-4 space-y-4 rounded-container-token">
        <label class="label">
            <span>Name</span>
            <input class="input p-2" bind:value={formData.name} />
        </label>
        <RadioGroup>
            <RadioItem bind:group={formData.incomeType} name="incomeType" value="annum">Per Annum</RadioItem>
            <RadioItem bind:group={formData.incomeType} name="incomeType" value="monthly">Per Month</RadioItem>
        </RadioGroup>
        <label class="label">
            <span>Income</span>
            <input class="input p-2" type="number" bind:value={formData.incomeValue} />
        </label>
    </form>
    <footer class="modal-footer {parent.regionFooter}">
        <button class="btn {parent.buttonNeutral}" on:click={parent.onClose}>{parent.buttonTextCancel}</button>
        <button class="btn {parent.buttonPositive}" on:click={onFormSubmit}>Submit Form</button>
    </footer>
</div>