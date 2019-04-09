<template>
  <div class="content" id="article-content" v-html="content"></div>
</template>

<script>
  export default {
    name: 'ArticleContent',
    props: {
      content: String
    },
    methods: {
      replaceGistIframe () {
        const scripts = this.$el.querySelectorAll('script')
        scripts.forEach(script => {
          const parentNode = script.parentNode
          let alternativeNode
          if (script.src.indexOf('https://gist.github.com/') !== -1) {
            console.log(1)
          } else {
            alternativeNode = document.createElement('script')
            alternativeNode.src = script.src
          }
          parentNode.replaceChild(alternativeNode, script)
        })
        // if (script) {
        //   const parent = script.parentNode
        //   const iframe = document.createElement('iframe')
        //   iframe.width = '100%'
        //   iframe.src = URL.createObjectURL(new Blob(['<!DOCTYPE html><title></title>' + script.outerHTML], {type: 'text/html'}))
        //   parent.replaceChild(iframe, script)
        //   iframe.onload = function () {
        //     console.log(iframe.innerHeight)
        //   }
        // }
      }
    },
    mounted () {
      this.replaceGistIframe()
    },
    updated () {
      this.replaceGistIframe()
    }
  }
</script>

<style scoped>

</style>
