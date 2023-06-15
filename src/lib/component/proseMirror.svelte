<script>
	import * as Y from 'yjs'
	// import { WebsocketProvider } from 'y-websocket'
	import { ySyncPlugin, yCursorPlugin, yUndoPlugin, undo, redo } from 'y-prosemirror'
	// import { EditorState } from 'prosemirror-state'
	import { schema } from './schema'
	// import { EditorView } from 'prosemirror-view'
	// @ts-ignore
	import { exampleSetup } from 'prosemirror-example-setup'
	// @ts-ignore
	// import { keymap } from 'prosemirror-keymap'
    import { onMount } from 'svelte';
	import "$lib/component/style.css"


let EditorState
let EditorView
let keymap

	onMount(async() => {
		// const {WebsocketProvider} = ((await import('y-websocket'))) ;
		const {WebrtcProvider} = ((await import('y-webrtc'))) ;
		var p1 = ((await import('prosemirror-keymap'))) ;
		keymap = p1.keymap;
		// console.log(key);
		var p2 = ((await import('prosemirror-state'))) ;
		EditorState = p2.EditorState
		var p3 = ((await import('prosemirror-view'))) ;
		EditorView = p3.EditorView

		const ydoc = new Y.Doc()
		// const provider = new WebsocketProvider('wss://demos.yjs.dev', 'prosemirror', ydoc)
		const provider = new WebrtcProvider('prosemirror', ydoc)
		console.log(provider);
		const type = ydoc.getXmlFragment('prosemirror')
	
		const editor = document.querySelector('#editor')
	
		const prosemirrorView = new EditorView(editor, {
		state: EditorState.create({
			schema,
			plugins: [
			ySyncPlugin(type),
			yCursorPlugin(provider.awareness),
			yUndoPlugin(),
			keymap({
				'Mod-z': undo,
				'Mod-y': redo,
				'Mod-Shift-z': redo
			})
			].concat(exampleSetup({ schema }))
		})
		})
	
		// @ts-ignore
		window.example = { provider, ydoc, type, prosemirrorView }

	})



</script>


<div id="editor"></div>