<template>
  <article class="container mx-auto">
    <div class="text-3xl rounded-md bg-green-600 text-white">
      <h1>Display All Content</h1>
      <nuxt-link to="/develop">develop</nuxt-link>
    </div>
    <nuxt-content
      class="prose prose-sm sm:prose lg:prose-lg xl:prose-2xl mx-auto"
      :document="page" />
  </article>
</template>

<script lang="ts">
import Vue from 'vue'
import { Context } from '@nuxt/types'

export default Vue.extend({
  async asyncData ({ $content, params, error }: Context) {
    const page = await $content('hello').fetch()
    return {
      page
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
