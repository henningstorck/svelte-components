<script lang="ts">
	import Button from './Button.svelte';
	import HLayout from './layouts/HLayout.svelte';
	import VLayout from './layouts/VLayout.svelte';
	import Modal from './Modal.svelte';

	interface Props {
		id: string;
		href: string;
		closeMessage: string;
		confirmationTitle: string;
		confirmationMessage: string;
		continueMessage: string;
		cancelMessage: string;
	}

	let {
		id,
		href,
		closeMessage,
		confirmationTitle,
		confirmationMessage,
		continueMessage,
		cancelMessage
	}: Props = $props();
</script>

<Modal {id} title={confirmationTitle} {closeMessage}>
	<VLayout>
		{confirmationMessage}

		<HLayout>
			<Button {href} color="danger" lazy>{continueMessage}</Button>

			<Button command="request-close" commandfor={id}>
				{cancelMessage}
			</Button>
		</HLayout>
	</VLayout>
</Modal>
