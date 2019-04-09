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
      runScript () {
        const scripts = this.$el.querySelectorAll('script')
        scripts.forEach(script => {
          const parentNode = script.parentNode
          let alternativeNode
          // todo: ホワイトリスト方式にする
          if (script.src.indexOf('https://gist.github.com/') !== -1) {
            alternativeNode = document.createElement('iframe')
            alternativeNode.src = URL.createObjectURL(new Blob(['<!DOCTYPE html><title></title>' + script.outerHTML], {type: 'text/html'}))
            alternativeNode.onload = () => {
              alternativeNode.height = alternativeNode.contentDocument.body.scrollHeight + 50
            }
          } else {
            alternativeNode = document.createElement('script')
            alternativeNode.src = script.src
          }
          parentNode.replaceChild(alternativeNode, script)
        })
      }
    },
    mounted () {
      this.runScript()
    },
    updated () {
      this.runScript()
    }
  }
</script>

<style scoped>
.content >>> iframe {
  width: 100%;
  border: none;
  overflow: hidden;
}
</style>
