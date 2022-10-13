<template>
  <div class=" flex flex-col items-center justify-center">
    <no-ssr>
      <DynamicRenderer :content="newHTMLObject" />

    </no-ssr>
  </div>
</template>

<script>

export default {
  name: 'IndexPage',
  data() {
    return {
      htmlObject: '<div class="article-content mb-7"><p class="paragraph"> Lorem ipsum dolor sit amet consectetur, adipisicing elit. Quisquam facilis perspiciatis quo numquam? Nihil ut, vero voluptatibus quos repudiandae unde asperiores officia similique libero omnis doloribus modi accusantium, officiis temporibus?</p><p class="paragraph"> Lorem ipsum dolor sit amet consectetur, adipisicing elit. Quisquam facilis perspiciatis quo numquam? Nihil ut, vero voluptatibus quos repudiandae unde asperiores officia similique libero omnis doloribus modi accusantium, officiis temporibus?</p><p class="paragraph"> Lorem ipsum dolor sit amet consectetur, adipisicing elit. Quisquam facilis perspiciatis quo numquam? Nihil ut, vero voluptatibus quos repudiandae unde asperiores officia similique libero omnis doloribus modi accusantium, officiis temporibus?</p><p class="paragraph"> Lorem ipsum dolor sit amet consectetur, adipisicing elit. Quisquam facilis perspiciatis quo numquam? Nihil ut, vero voluptatibus quos repudiandae unde asperiores officia similique libero omnis doloribus modi accusantium, officiis temporibus?</p><p class="paragraph"> Lorem ipsum dolor sit amet consectetur, adipisicing elit. Quisquam facilis perspiciatis quo numquam? Nihil ut, vero voluptatibus quos repudiandae unde asperiores officia similique libero omnis doloribus modi accusantium, officiis temporibus?</p></div>',
      newHTMLObject: null,
    }
  },
  methods: {
    // strip html and append a div before the last paragraph
    stripHTML(html) {
      if (process.client) {
        const div = document.createElement('div')
        div.innerHTML = html
        const paragraphs = div.querySelectorAll('p')
        const lastParagraph = paragraphs[paragraphs.length - 1]
        const newDiv = document.createElement('div')
        newDiv.innerHTML = lastParagraph.innerHTML
        lastParagraph.innerHTML = '<div><logo></logo></div>'
        lastParagraph.appendChild(newDiv)
        return div.innerHTML
      }
    }
  },
  mounted() {
    this.newHTMLObject = this.stripHTML(this.htmlObject);
  },
}
</script>
