<script lang="coffeescript">
  import ProgressNav  from './components/ProgressNav.svelte'
  import ProseDown  from './components/ProseDown.svelte'

  fileInput = null
  openImagePicker = () ->
    fileInput.click()

  inputHeadline = null
  doAiHeadline = () ->
    mechanisms = [
      'Bedtime Ritual'
      'Ancient Technique'
      'Hack'
      'Secret Technique'
    ]
    benefits = [
      'Transform Your Health'
      'Increase Metabolism'
      'Lower Blood Sugar'
    ]

    pickArray = (a) ->
      a[Math.floor(Math.random() * a.length)]


    headlines = [
      'Potent Natural Body Reset Solution'
      'Weight Management Tips from 50 Successful People You Can Follow'
      'Lose Weight This Winter The Healthy Way Topic'
      'Lose Weight This Winter The Healthy Way'
      'Most Effective Weight Loss Strategy Revealed'
      'Increase Testosterone With This Easy Ritual'
      'My Morning Routine To Stay Lean Without **Dieting**'
      'The REAL Reason Women Struggle to Lose Weight'
      '9-Minute Morning Ritual Makes Day a Breeze'
      'Healthy Meals in 5 Minutes or Less!'
    ]


    newHeadlines = [
      "Discover How This **#{pickArray mechanisms}** Could #{pickArray benefits}"
      pickArray headlines
    ]

    inputHeadline.setValue(pickArray newHeadlines)

</script>

<template lang="pug">

  div.sidebar
    h1 Lander Wizard
    a(target='_blank' href='https://www.amazinghealthscience.com/lander/o1Wp')
      button View Lander
    div: :markdown-it(linkify langPrefix='highlight-')
      View your lander at this [link](https://www.amazinghealthscience.com/lander/o1Wp).
      Customize your lander using the form to the right.
    
    div.nav: ProgressNav
      ul
        li: a(href='#image') Image
        li: a(href='#headline') Headline
        li: a(href='#body') Body
        ul
          li: a(href='#expert') Expert & Problem
          li: a(href='#solution') Solution & Enemy
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
          img(src='img/adimage.jpg' alt='ad image' on:click='{openImagePicker}')
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

        Get more training on winning images [here](https://innercircle.ultimatefreedom.com/).
    fieldset#headline
      legend Headline
      ProseDown(bind:this='{inputHeadline}' hideToggle='{false}' mode='prosemirror' value='This **"7 Second Hack"** Could Transform Your Health')
      div.ai
        div
          button(on:click='{doAiHeadline}') AI Rewrite
          span &nbsp;This button will suggest a new headline based on the current headline.
      div.guide: :markdown-it(linkify langPrefix='highlight-')
        After the image, the headline is the second most important part of the lander.
        Viewers will try to find an answer to the question invoked by the image in the headline .
        The headline should hint at some solution that provides a major benefit.
        Don't close the loop! The viewer's curiosity should only get *stronger* after reading the headline.
        ### Template: 
        Discover How This \*\*[MECHANISM]\*\* Could [BENEFIT]
        ### Models:
         - This "7 Second Hack" Could Transform Your Health
         - This "7 Second Hack" Could Transform Your Health
         - This "7 Second Hack" Could Transform Your Health

    fieldset#body
      legend Body
      fieldset#expert
        legend Expert & Problem
        ProseDown(value='Whistle-blower Dr. Chen discovered a simple method to lose weight and keep it off (not exercise or diet).')
        div.ai: :markdown-it(linkify langPrefix='highlight-')
          ## AI Analysis
          TBD
      fieldset#solution
        legend Solution & Common Enemy
        ProseDown(value="Chen's new method addresses the root-cause of obesity so well, the weight loss industry is trying to keep him quiet.")
        div.ai: :markdown-it(linkify langPrefix='highlight-')
          ## AI Analysis
          TBD
      fieldset#cta
        legend Call to Action
        ProseDown(value='Take the quiz below')
        div.ai: :markdown-it(linkify langPrefix='highlight-')
          ## AI Analysis
          TBD
      div.guide: :markdown-it(linkify langPrefix='highlight-')
        ## Guide/Training
        TBD

    fieldset#quiz
      legend Quiz
      fieldset#q1
        legend Question 1
        div
          label Question
          ProseDown(value='Do you or anyone you know work at a diet/fitness company?')
        div.ai: :markdown-it(linkify langPrefix='highlight-')
          ## AI Analysis
          TBD
        div
          div.answer
            label Answer A
            ProseDown(value='Yes' mode='markdown' hideToggle='{true}')
          div.answer
            label Answer B
            ProseDown(value='No' mode='markdown' hideToggle='{true}')
      fieldset#q2
        legend Question 2
        div
          label Question
          ProseDown(value='Have you tried a diet that didn’t work in the last 12 months?')
        div.ai: :markdown-it(linkify langPrefix='highlight-')
          ## AI Analysis
          TBD
        div
          div.answer
            label Answer A
            ProseDown(value='Yes' mode='markdown' hideToggle='{true}')
          div.answer
            label Answer B
            ProseDown(value='No' mode='markdown' hideToggle='{true}')
      fieldset#q3
        legend Question 3
        div
          label Question
          ProseDown(value='Has your doctor diagnosed you with excess ghrelin?')
        div.ai: :markdown-it(linkify langPrefix='highlight-')
          ## AI Analysis
          TBD
        div
          div.answer
            label Answer A
            ProseDown(value='Yes' mode='markdown' hideToggle='{true}')
          div.answer
            label Answer B
            ProseDown(value='No' mode='markdown' hideToggle='{true}')
      fieldset#q4
        legend Question 4
        div
          label Question
          ProseDown(value='Are you over 40 years old?')
        div.ai: :markdown-it(linkify langPrefix='highlight-')
          ## AI Analysis
          TBD
        div
          div.answer
            label Answer A
            ProseDown(value='Yes' mode='markdown' hideToggle='{true}')
          div.answer
            label Answer B
            ProseDown(value='No' mode='markdown' hideToggle='{true}')
      div.guide: :markdown-it(linkify langPrefix='highlight-')
        ## Guide/Training
        TBD

    fieldset#congratulations
      legend Congratulations
      fieldset#congratulationsheader
        legend Congratulations Header
        ProseDown(value="Congratulations! Before you watch the presentation with Dr. Chen's discoveries, our lawyers have asked us to require that each person agrees to the following guidelines:")
        div.ai: :markdown-it(linkify langPrefix='highlight-')
          ## AI Analysis
          TBD
      fieldset#g1
        legend Guideline 1
        ProseDown(value='You must NOT talk about the details of this presentation with ANYONE due to the weight loss industry secrets contained within.')
        div.ai: :markdown-it(linkify langPrefix='highlight-')
          ## AI Analysis
          TBD
      fieldset#g2
        legend Guideline 2
        ProseDown(value="If you lose too much weight, too fast, consult a doctor. This powerful secret can help quickly shed pounds and must be used responsibly.")
        div.ai: :markdown-it(linkify langPrefix='highlight-')
          ## AI Analysis
          TBD
      fieldset#g3
        legend Guideline 3
        ProseDown(value='This presentation is ONLY being made available to a select group of people and will be REMOVED if Dr. Chen comes under too much pressure from the weight loss industry. If you do not want to discover these industry secrets, please CLOSE THIS WINDOW IMMEDIATELY to free up your slot for the next person in line.')
        div.ai: :markdown-it(linkify langPrefix='highlight-')
          ## AI Analysis
          TBD
      fieldset#agree
        legend Agree Button
        ProseDown(value='I Agree!')
      div.guide: :markdown-it(linkify langPrefix='highlight-')
        ## Guide/Training
        TBD
    footer
</template>

<style>
  .sidebar {
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
    /* text-transform: uppercase; */
  }

  fieldset fieldset legend {
    font-size: 150%;
  }

  .ai,
  .guide {
    padding: 4px;
  }

  .ai h2,
  .ai h3,
  .guide h2,
  .guide h3 {
    margin-top: 0;
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

  footer {
    height: 1200px;
  }
</style>
