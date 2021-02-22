<script lang="coffeescript">
  import {onMount} from 'Svelte'
  import ProgressNav  from './components/ProgressNav.svelte'

  import { EditorView } from 'prosemirror-view'
  import { EditorState } from 'prosemirror-state'
  import { schema, defaultMarkdownParser, defaultMarkdownSerializer } from 'prosemirror-markdown'
  import { exampleSetup } from 'prosemirror-example-setup'

  fileInput = null

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
      @view = new EditorView(target, {
        state: EditorState.create({
          doc: defaultMarkdownParser.parse(content),
          plugins: exampleSetup({schema})
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
  content = null

  
  onMount () ->
    view = new ProseMirrorView(place, content.value)

    ```
    document.querySelectorAll("input[type=radio]").forEach(button => {
      console.log('button')
      button.addEventListener("change", () => {
        console.log('change');
        if (!button.checked) return
        let View = button.value == "markdown" ? MarkdownView : ProseMirrorView
        if (view instanceof View) return
        let content = view.content
        view.destroy()
        view = new View(place, content)
        view.focus()
      })
    })
    ```

  toggleEditor = (e) ->
    console.log 'CHANGE'
    if not @.checked then return
    View = if @.value is 'markdown' then MarkdownView else ProseMirrorView
    if view instanceof View then return
    content = view.content
    view.destroy()
    view = new View(place, content)
    view.focus() 


  openImagePicker = () ->
    fileInput.click()
</script>

<template lang="pug">
  div.nav: ProgressNav
    ul
      li: a(href='#image') Image
      li: a(href='#headline') Headline
      li: a(href='#body') Body
      ul
	      li: a(href='#expert') Expert and Problem
        li: a(href='#solution') Solution and Common Enemy
      li: a(href='#quiz') Quiz
      ul
        li: a(href='#q1') Question 1
        li: a(href='#q2') Question 2
        li: a(href='#q3') Question 3
        li: a(href='#q4') Question 4
      li: a(href='#congratulations') Congratulations
      ul
        li: a(href='#g1') Guideline 1
        li: a(href='#g2') Guideline 2
        li: a(href='#g3') Guideline 3
        li: a(href='#agree') Agree Button
  main
    fieldset#image
      legend Image
      div
          img(src='img/ad-image.jpg' alt='ad image' on:click='{openImagePicker}')
          button(on:click='{openImagePicker}') Upload Image
          input(type='file' bind:this='{fileInput}' style='display:none')

      div.ai: :markdown-it(linkify langPrefix='highlight-')
        ## AI Analysis
         - **Too much text.** Facebook rejects ad images with too much text.
           Even if not rejected, the ad will be given fewer impressions.
           Limit text to 25% of image.
         - **Negative sentiment.** Facebook prefers images of happy people.
         - **Lone person.** Facebook prefers images with two or more people together.
      div.guide: :markdown-it(linkify langPrefix='highlight-')
        ## Does your ad image satisfy these properties of winning images?
        - **Good images get the user to stop scrolling.** People scan the images in their newsfeed,
          only reading the few things that catch their attention. 
          If you have a poor ad image, the rest of your ad doesn't matter because it won't even be read.
          Good images stand out from other content in the Facebook newsfeed (think: photos and cartoons).
          So vector-style images tend to stand out. Also experiment with colors: black and white,
          grayscale, or super-colorful.

        - **Good images get the user to ask a question in their head.**
           The image should invoke a burning question in the user's mind that 
          *must* be answered. When the viewer sees your ad image, they should be thinking something like:         
          - What the heck is that?
          - Where do I squeeze to lose weight?

        - **Good images tell a story, but only *half* the story.** This is called opening a "loop." 
        One common mistake is placing a product in the image (like a bottle). This closes the loop and
        makes people think they're being sold something. Make sure the story is simple and easy to follow.

        Get more training on winning images here.
    fieldset#headline
      legend Headline
      div.editor(bind:this='{place}')
      div(style='text-align:center')
        label.toggle(style='border-right: 1px solid silver')
          span Rich Text&nbsp;
          input(type='radio' name='inputformat' on:change='{toggleEditor}' value='prosemirror' checked) 
          span &nbsp; 
        label.toggle
          span &nbsp;
          input(type='radio' name='inputformat' on:change='{toggleEditor}' value='markdown')
          span &nbsp;Markdown 

      div
        textarea(bind:this='{content}' style='display:none;') This **"7 Second Hack"** Could Transform Your Health
      div
        b Template: 
        span Discover How This **[MECHANISM]** Could [BENEFIT]
      div
        b Models: 
        ul 
          li This "7 Second Hack" Could Transform Your Health
          li This "7 Second Hack" Could Transform Your Health
          li This "7 Second Hack" Could Transform Your Health

    fieldset#body
      legend Body
      fieldset#expert
        legend Expert and Problem
        div Whistle-blower Dr. Chen discovered a simple method to lose weight and keep it off (not exercise or diet).
      fieldset#solution
        legend Solution and Common Enemy
        div Whistle-blower Dr. Chen discovered a simple method to lose weight and keep it off (not exercise or diet).
      fieldset#cta
        legend Call to Action
        input(value='Take the quiz below')

    fieldset#quiz
      legend Quiz
      fieldset#q1
        legend Question 1
        div
          label Question
          input(value='Do you or anyone you know work at a diet/fitness company?')
        div
          div.answer
            label Answer A
            input(value='Yes')
          div.answer
            label Answer B
            input(value='No')
      fieldset#q2
        legend Question 2
        div
          label Question
          input(value='Do you or anyone you know work at a diet/fitness company?')
        div
          div.answer
            label Answer A
            input(value='Yes')
          div.answer
            label Answer B
            input(value='No')
      fieldset#q3
        legend Question 3
        div
          label Question
          input(value='Do you or anyone you know work at a diet/fitness company?')
        div
          div.answer
            label Answer A
            input(value='Yes')
          div.answer
            label Answer B
            input(value='No')
      fieldset#q4
        legend Question 4
        div
          label Question
          input(value='Do you or anyone you know work at a diet/fitness company?')
        div
          div.answer
            label Answer A
            input(value='Yes')
          div.answer
            label Answer B
            input(value='No')

    fieldset#congratulations
      legend Congratulations
      fieldset#congratulationsheader
        legend Congratulations Header
        span Congratulations! Before you watch the presentation with Dr. Chen's discoveries, 
        | our lawyers have asked us to require that each person agrees to the following guidelines:
      fieldset#g1
        legend Guideline 1
        span You must NOT talk about the details of this presentation with ANYONE due to the weight loss 
        | industry secrets contained within.
      fieldset#g2
        legend Guideline 2
        span If you lose too much weight, too fast, consult a doctor. This powerful secret can help quickly 
        | shed pounds and must be used responsibly.
      fieldset#g3
        legend Guideline 3
        span This presentation is ONLY being made available to a select group of people and will be 
        | REMOVED if Dr. Chen comes under too much pressure from the weight loss industry. If you do not 
        | want to discover these industry secrets, please CLOSE THIS WINDOW IMMEDIATELY to free up your 
        | slot for the next person in line.
      fieldset#agree
        legend Agree Button
        input(value='I Agree!')
    footer
</template>

<style>
  :global(.nav) {
    position: fixed;
    left: 1em;
    top: 1em;
    width: 14em;
    line-height: 2;
  }
  main {
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
    margin-left: 20em;
  }

  fieldset {
    margin-bottom: 2em;
  }
  legend {
    font-size: 300%;
    text-transform: uppercase;
  }

  fieldset fieldset legend {
    font-size: 150%;
  }

  .ai {
    background-color: aliceblue;
  }

  .guide {
    background-color: lightyellow;
  }

  div.answer {
    width: 50%;
    display: inline-block;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }

  img {
    width: 400px;
  }

  label {
    font-weight: bold;
  }

  label.toggle {
    display: inline;
  }

  input.wide {
    width: 100%;
  }

  footer {
    height: 1200px;
  }

  .editor {
    padding: 0;
    margin: 0;
    height: 80px;
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
</style>
