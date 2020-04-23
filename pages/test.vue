<template>
  <section class="section">
    <ul v-for="(post, i) in posts.items" :key="i">
      <li>{{ post.fields.title }}</li>
      <ul>
        <li v-html="toHtmlString(post.fields.body)" />
        <li> {{ post.fields.entryDate }} </li>
      </ul>
    </ul>
  </section>
</template>

<script>
import format from 'date-fns/format'
import { documentToHtmlString } from '@contentful/rich-text-html-renderer'
import client from '~/plugins/contentful'

export default {
  async asyncData ({ env }) {
    let posts = []
    await client.getEntries({
      content_type: process.env.POST_TYPE_ID,
      order: '-fields.entryDate'
    }).then(res => (posts = res))
    return {
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
