<script>
    import ProseMirror from "../lib/component/proseMirror.svelte";
	import Quill from "../lib/component/quillEditor.svelte";
    // import CodeMirror from '../lib/component/codeMirror.svelte';
	import { onMount } from 'svelte';
    // import Slate from '../lib/component/slate.svelte';
	
	
	// const sleep = ms => new Promise(f => setTimeout(f, ms));
	
	onMount(async () => {
		// await sleep(1000); // simulate network delay
		// Quill = (await import('../lib/component/quillEditor.svelte'));
	});
</script>

<!-- <Quill /> -->

<ProseMirror />

<!-- <CodeMirror /> -->

<!-- <svelte:component this={Quill} /> -->

<!-- <Slate /> -->