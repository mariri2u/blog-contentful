<template>
  <section class="section">
    <div class="columns is-mobile" v-for="(post, i) in posts.items" :key="i">
      <nuxt-link v-bind:to="{ name: 'slug', params: { slug: post.fields.slug }}">
        <card
          v-bind:title='post.fields.title'
          icon="cellphone-link"
        >
          slug: {{ post.fields.slug }}<br/>
          id: {{ post.sys.id }}<br/>
          entry: {{ post.fields.entryDate }}<br/>
        </card>
      </nuxt-link>
    </div>
  </section>
</template>

<script>
import format from 'date-fns/format'
import { documentToHtmlString } from '@contentful/rich-text-html-renderer'
import client from '~/plugins/contentful'
import Card from '~/components/Card'

export default {
  components: {
    Card
  },
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
