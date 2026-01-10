<script lang="ts">
	import { i18n } from '$lib/common/i18n/i18nService';
	import Button from './Button.svelte';
	import HLayout from './layouts/HLayout.svelte';
	import VLayout from './layouts/VLayout.svelte';
	import Modal from './Modal.svelte';

	interface Props {
		id: string;
		href: string;
		confirmationTitle: string;
		confirmationMessage: string;
		continueMessage: string;
		cancelMessage?: string;
	}

	let {
		id,
		href,
		confirmationTitle,
		confirmationMessage,
		continueMessage = i18n('common.continue'),
		cancelMessage = i18n('common.cancel')
	}: Props = $props();
</script>

<Modal {id} title={confirmationTitle}>
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
