<script>
	import { onMount } from 'svelte'
	/* eslint-env browser */

	// @ts-ignore
	import * as Y from 'yjs'
	// import CodeMirror from 'codemirror'
	// import { WebrtcProvider } from 'y-webrtc'
	// import { CodemirrorBinding } from 'y-codemirror'
	import 'codemirror/mode/javascript/javascript.js'
	
	
	var CodeMirror
	var CodemirrorBinding
	onMount(async() =>{
		var c1 = ((await import('codemirror')));
		CodeMirror = c1.default;
		const {WebrtcProvider} = ((await import('y-webrtc'))) ;
		var c2 = ((await import('y-codemirror'))) ;
		CodemirrorBinding = c2.default;
		
		const ydoc = new Y.Doc()
		const provider = new WebrtcProvider('quill-demo-room', ydoc)
	
		const yText = ydoc.getText('codemirror')
		const editorContainer = document.querySelector('#editor')
	
		const editor = CodeMirror(editorContainer, {
			mode: 'javascript',
			lineNumbers: true
		})
	
		const binding = new CodemirrorBinding(yText, editor, provider.awareness)
	})



</script>