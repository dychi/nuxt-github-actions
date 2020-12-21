<template>
  <div class="bg-teal-900">
    <p>Input</p>
    <input v-model="query" type="search" autocomplete="on" />

    <ul v-if="articles.length">
      <li v-for="article of articles" :key="article.slug">
        <NuxtLink :to="{ name: 'blog-slug', params: { slug: article.slug } }">{{ article.title }}</NuxtLink>
      </li>
    </ul>
  </div>
</template>
<script lang="ts">
import Vue from 'vue'
import { Context } from '@nuxt/types'


export default Vue.extend({
  data () {
    return {
      query: '',
      articles: []
    }
  },
  watch: {
    async query (query: string) {
      if (!query) {
        this.articles = []
        return
      }

      this.articles = await this.$content('items')
        .only(['title', 'slug'])
        .sortBy('createdAt', 'asc')
        .limit(12)
        .search(query)
        .fetch()
    }
  }
})
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
</style>
