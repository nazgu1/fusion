<script lang="ts">
	import { invalidateAll } from '$app/navigation';
	import type { Item } from '$lib/api/model';
	import { t } from '$lib/i18n';
	import { toast } from 'svelte-sonner';
	let tooltip = t('common.reload');
	import { RefreshCcw } from 'lucide-svelte';
	import { shortcut, shortcuts } from './ShortcutHelpModal.svelte';

	type Props =
		| {
				disabled: true;
		  }
		| {
				disabled?: false;
		  };

	let props: Props = $props();

	async function handleClick() {
		if (props.disabled) {
			console.error('unreachable code');
			return;
		}

		toast.success(t('state.success'));
		invalidateAll();
	}
</script>

<div class="tooltip tooltip-bottom" data-tip={tooltip}>
	<button
		onclick={handleClick}
		use:shortcut={shortcuts.reloadAll.keys}
		class="btn btn-ghost btn-square"
	>
		<RefreshCcw class="size-4" />
	</button>
</div>
