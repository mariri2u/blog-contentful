<template>
  <section class="section">
    <ul v-for="(post, i) in posts.items" :key="i">
      <li>{{ post.fields.title }}</li>
      <ul>
        <li>{{ post.fields.content }}</li>
        <li>{{ post.fields.updateDate }}</li>
      </ul>
    </ul>
    <div>json: {{ posts }}</div>
  </section>
</template>

<script>
import client from '~/plugins/contentful'

export default {
  async asyncData ({ env }) {
    let posts = []
    await client.getEntries({
      content_type: process.env.POST_TYPE_ID,
      order: '-fields.updateDate'
    }).then(res => (posts = res))
    return {
      posts
    }
  }
}
</script>
