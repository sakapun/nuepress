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
          if (script.src.indexOf('https://gist.github.com/') !== -1) {
            console.log(1)
          }
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
    }
  }
</script>

<style scoped>

</style>
