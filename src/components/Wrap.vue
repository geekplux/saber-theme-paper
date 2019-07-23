<template>
  <div class="container">
    <Header :siteTitle="siteTitle"/>
    <main class="content" aria-label="Content">
      <slot></slot>
    </main>
    <Footer :siteTitle="siteTitle"/>
  </div>
</template>

<style lang="scss" scoped>
.content {
  position: relative;
  padding: 25px;
  width: 80vw;
  max-width: 750px;
  margin: 50px auto 0 auto;
  background: #fff;
  box-shadow: 0px 10px 20px 0px rgba(236, 236, 236, 0.86);
}

@media screen and (min-width: 600px) {
  .content {
    padding: 50px;
  }
}
</style>


<script>
import variables from 'saber/variables'
import Header from './Header.vue'
import Footer from './Footer.vue'

export default {
  components: {
    Header,
    Footer
  },

  props: ['page'],

  head() {
    const { title, layout, excerpt } = this.page.attributes
    let { description } = this.$siteConfig
    if (layout === 'page' || layout === 'post') {
      if (excerpt) {
        description = excerpt.replace(/<(?:.|\n)*?>/gm, '')
      }
    }
    return {
      title: title ? `${title} - ${this.siteTitle}` : this.siteTitle,
      meta: [
        description && {
          name: 'description',
          content: description
        }
      ].filter(Boolean),
      link: variables.feedLink
        ? [
            {
              rel: 'alternate',
              title: `${this.siteTitle} - Feed`,
              type: `application/${
                variables.feedLinkType === 'atom'
                  ? 'atom+xml'
                  : variables.feedLinkType === 'rss'
                  ? 'rss+xml'
                  : 'json'
              }`,
              href: variables.feedLink
            }
          ].filter(Boolean)
        : []
    }
  },

  computed: {
    siteTitle() {
      return this.$siteConfig.title || 'Your Awesome Title'
    }
  }
}
</script>
