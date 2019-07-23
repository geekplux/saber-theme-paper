<template>
  <Wrap :page="page">
    <article class="post typo" itemscope itemtype="http://schema.org/BlogPosting">
      <header class="post-header">
        <h1 class="post-title" itemprop="name headline">{{ page.attributes.title }}</h1>
        <div class="post-meta">
          <time
            class="dt-published"
            :datetime="page.attributes.createdAt"
            itemprop="datePublished"
          >{{ formatDate(page.attributes.createdAt) }}</time>
        </div>
      </header>

      <div class="post-content" itemprop="articleBody">
        <slot name="default"/>
      </div>
      <a class="u-url" :href="page.attributes.permalink" hidden></a>
      <div class="post-meta">
        <div class="category">
          <span class="label">Category:</span>
          <span
            class="categories"
            v-for="category in page.attributes.categories"
            :key="category.toString()"
          >, {{category}}</span>
        </div>
        <div class="tag">
          <span class="label">Tags:</span>
          <span class="tags" v-for="tag in page.attributes.tags" :key="tag.toString()">, {{tag}}</span>
        </div>
      </div>
      <div class="pagination">
        <router-link class="prev" v-if="page.prevPost" :to="page.prevPost.permalink">
          <strong>{{ $siteConfig.pagination && $siteConfig.pagination.prevPost || '上一篇' }}</strong>
          <p>{{ page.prevPost.title }}</p>
        </router-link>
        <router-link class="next" v-if="page.nextPost" :to="page.nextPost.permalink">
          <strong>{{ $siteConfig.pagination && $siteConfig.pagination.nextPost || '下一篇' }}</strong>
          <p>{{ page.nextPost.title }}</p>
        </router-link>
      </div>
    </article>
    <Disqus
      v-if="page.attributes.comments !== false && $themeConfig.disqus"
      :url="$siteConfig.url"
      :permalink="page.attributes.permalink"
      :shortname="$themeConfig.disqus"
    />
  </Wrap>
</template>

<style lang="scss">
@import '../styles/variables.scss';

article.typo {
  position: relative;
  font-size: 16px;

  a {
    word-break: break-all;
  }

  .pagination {
    display: flex;
    font-size: 14px;
    justify-content: space-between;

    a {
      border-bottom: 0;
      flex: 1;

      &.prev {
        text-align: right;
        padding-right: 10px;
      }
      &.next {
        text-align: left;
        padding-left: 10px;
      }
    }
  }

  code {
    font-size: 14px;
  }

  .post-meta {
    @extend %post-meta;
    margin-bottom: 20px;
  }

  .label {
    color: $gray;
  }

  @media screen and (min-width: 600px) {
    .post-meta {
      margin-bottom: 30px;
    }
  }
}
</style>


<script>
import formatDate from '../utils/formatDate'
import Wrap from '../components/Wrap.vue'
import Disqus from '../components/Disqus.vue'

export default {
  components: {
    Wrap,
    Disqus
  },

  props: ['page'],

  methods: {
    formatDate
  }
}
</script>
