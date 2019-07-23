<template>
  <Wrap :page="page">
    <div class="home">
      <!-- <h1 class="site-title" v-if="$siteConfig.title">{{ $siteConfig.title }}</h1>
      <p class="site-description" v-if="$siteConfig.description">{{ $siteConfig.description }}</p>
      -->
      <slot name="default"></slot>

      <h2
        class="post-list-heading"
        v-if="page.posts && page.posts.length > 0 && page.attributes.listTitle"
      >{{ page.attributes.listTitle }}</h2>

      <ul class="post-list" v-if="page.posts && page.posts.length > 0">
        <li class="post" v-for="post in page.posts" :key="post.attributes.permalink">
          <span class="post-meta">
            <span class="date">{{ formatDate(post.attributes.createdAt) }}</span>
            <span
              class="categories"
              v-for="category in post.attributes.categories"
              :key="category.toString()"
            >, {{category}}</span>
          </span>
          <h3>
            <saber-link
              class="post-link"
              :to="post.attributes.permalink"
            >{{ post.attributes.title }}</saber-link>
          </h3>
        </li>
      </ul>

      <div
        class="pagination"
        v-if="page.pagination && (page.pagination.hasNext || page.pagination.hasPrev)"
      >
        <router-link
          class="prev-link"
          :to="page.pagination.prevLink"
          v-if="page.pagination.hasPrev"
        >{{ $siteConfig.pagination && $siteConfig.pagination.nextPage || '更多文章'}}</router-link>
        <router-link
          class="next-link"
          :to="page.pagination.nextLink"
          v-if="page.pagination.hasNext"
        >{{ $siteConfig.pagination && $siteConfig.pagination.prevPage || '返回'}}</router-link>
      </div>
    </div>
  </Wrap>
</template>

<style lang="scss" scoped>
@import '../styles/variables.scss';

.post-list-heading {
  color: $gray;
  font-weight: lighter;
  margin-bottom: 50px;
}
.post-list {
  list-style: none;
  margin: 0;
  padding: 0;
}
.post {
  margin-bottom: 2em;
}

.post-meta {
  @extend %post-meta
}

.post-link {
  position: relative;
  text-decoration: none;
  color: $headline-color;
  font-size: 20px;
}


@media screen and (min-width: 600px) {
  .post-link {
    &:hover {
      // background: rgba(98, 146, 241, 0.3);
      color: $headline-color;
      &::before {
        width: 10px;
        left: -30px;
      }
    }

    &::before {
      content: ' ';
      position: absolute;
      top: 10px;
      left: -20px;
      width: 4px;
      height: 4px;
      border-radius: 2px;
      background: $headline-color;
      transition: all 200ms cubic-bezier(0.4, 0, 1, 1);
    }
  }
}
</style>


<script>
import variables from 'saber/variables'
import formatDate from '../utils/formatDate'
import Wrap from '../components/Wrap.vue'
import getSvg from '../utils/getSvg'

export default {
  components: {
    Wrap
  },

  props: ['page'],

  data() {
    return {
      feedLink: variables.feedLink
    }
  },

  methods: {
    formatDate,
    getSvg
  }
}
</script>
