<template>
  <section class="section">
    <div>slug: {{ msg }}</div>
    <div v-html="toHtmlString(posts.items[0].fields.body)" />
  </section>
</template>

<script>
import format from 'date-fns/format'
import { documentToHtmlString } from '@contentful/rich-text-html-renderer'
import client from '~/plugins/contentful'

export default {
  async asyncData (context) {
    let posts = []
    await client.getEntries({
      content_type: process.env.POST_TYPE_ID,
      'fields.slug': context.params.slug,
      limit: 1
    }).then(res => (posts = res))
    return {
      msg: context.params.slug,
      posts
    }
  },
  methods: {
    toHtmlString (obj) {
      return documentToHtmlString(obj)
    },
    dateToStr (str) {
      return format(str, 'YYYY/M/D')
    }
  }
}
</script>
