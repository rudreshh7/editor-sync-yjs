<svelte:head>
	<link href="https://cdn.quilljs.com/1.3.6/quill.snow.css" rel="stylesheet">
</svelte:head>

<script>
	import * as Y from 'yjs'
	// import { WebrtcProvider } from 'y-webrtc'
	// import { QuillBinding } from 'y-quill'
	// import Quill from 'quill'
	// import QuillCursors from 'quill-cursors'
    import { onMount } from 'svelte';

	

	let QuillCursors
	let Quill

	var quill;
	onMount(async () => {
		const {WebrtcProvider} = ((await import('y-webrtc'))) ;
		const {QuillBinding} = (await import('y-quill')) ;
		var q2 = (await import('quill-cursors'));
		QuillCursors = q2.default;
		var q = (await import ('quill'));
		Quill = q.default;
		console.log(Quill);
		Quill.register('modules/cursors', QuillCursors)
	

		quill = new Quill(document.querySelector('#editor'), {
		modules: {
			cursors: true,
			toolbar: [
			// adding some basic Quill content features
			[{ header: [1, 2, false] }],
			['bold', 'italic', 'underline'],
			['image', 'code-block']
			],
			history: {
			// Local undo shouldn't undo changes
			// from remote users
			userOnly: true
			}
		},
		placeholder: 'Start collaborating...',
		theme: 'snow' // 'bubble' is also great
		})
		const ydoc = new Y.Doc()
	
		const provider = new WebrtcProvider('quill-demo-room', ydoc)
		provider.connect()
		// Define a shared text type on the document
		const ytext = ydoc.getText('quill')
	
		// "Bind" the quill editor to a Yjs text type.
		const binding = new QuillBinding(ytext, quill, provider.awareness)
	});

	// A Yjs document holds the shared data

	// Remove the selection when the iframe is blurred

</script>

<div id="editor"></div>