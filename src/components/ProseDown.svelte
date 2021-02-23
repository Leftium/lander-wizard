<svelte:options accessors={true} />

<script type="text/coffeescript">
  import {onMount} from 'svelte'

  import { EditorView } from 'prosemirror-view'
  import { EditorState } from 'prosemirror-state'
  import { schema, defaultMarkdownParser, defaultMarkdownSerializer } from 'prosemirror-markdown'
  import { exampleSetup, buildMenuItems } from 'prosemirror-example-setup'

  class MarkdownView
    constructor: (target, content) ->
      @textarea = target.appendChild(document.createElement('textarea'))
      @textarea.value = content

    focus: ()-> @textarea.focus()
    destroy: ()-> @textarea.remove()

    ```
    get content() { return this.textarea.value }
    ```
  class ProseMirrorView
    constructor: (target, content) ->
      menuItems = buildMenuItems(schema)
      menuContent = [
        [
          menuItems.toggleStrong          
          menuItems.toggleEm
          menuItems.toggleLink
        ]
        menuItems.fullMenu[2]
        menuItems.blockMenu[0]
      ]
      plugins = exampleSetup({
        schema
        floatingMenu: true
        menuBar: true
        menuContent
        })

      @view = new EditorView(target, {
        state: EditorState.create({
          doc: defaultMarkdownParser.parse(content),
          plugins
        })
      })
  
    focus: ()-> @view.focus()
    destroy: ()-> @view.destroy()

    ```
    get content() {
      return defaultMarkdownSerializer.serialize(this.view.state.doc)
    }
    ```
  
  
  place = null
  view = null
  export value = ''
  export hideToggle = true
  export mode = 'markdown' 

  f = () ->
    view.content
  `export const getValue = f`
  

  f = (value) ->
    view.destroy()
    View = if @.value is 'markdown' then MarkdownView else ProseMirrorView
    view = new View(place, value)
  `export const setValue = f`

  toggleEditor = (e) ->
    if not @.checked then return
    View = if mode is 'markdown' then MarkdownView else ProseMirrorView
    if view instanceof View then return
    content = view.content
    view.destroy()
    view = new View(place, content)
    view.focus()  

  onMount () ->
    View = if mode is 'markdown' then MarkdownView else ProseMirrorView
    view = new View(place, value)
</script>

<template lang="pug">
  div.editor(bind:this='{place}')
  div(style='text-align: right' class:hideToggle)
    label.toggle(style='border-right: 1px solid silver')
      span Rich Text&nbsp;
      input(type='radio' bind:group='{mode}' on:change='{toggleEditor}' value='prosemirror') 
      span &nbsp; 
    label.toggle
      span &nbsp;
      input(type='radio' bind:group='{mode}' on:change='{toggleEditor}' value='markdown')
      span &nbsp;Markdown 

</template>

<style>
  .editor {
    padding: 0;
    margin: 0;
    min-height: 80px;
  }

  :global(.editor p),
  :global(.editor blockquote),
  :global(.editor li),
  :global(.editor ol),
  :global(.editor ul) {
    margin-top: 0.2em !important;
    margin-bottom: 0.2em;
  }

  :global(.editor textarea) {
    width: 100%;
    height: 100%;
    border: none;
    margin: 0;
  }

  :global(.editor textarea:focus) {
    outline: none !important;
  }

  label.toggle {
    display: inline;
    color: gray;
    font-size: 80%;
  }

  .hideToggle {
    display: none;
  }
</style>
