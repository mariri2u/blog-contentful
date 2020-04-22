<template>
  <section class="section">
    <div>{{ msg }}</div>
    <div>{{ msg2 }}</div>
    <div>{{ token }}</div>
  </section>
</template>

<script>
export default {
  asyncData ({ env }) {
    return {
      msg: env.POST_TYPE_ID,
      msg2: 'aaaaa',
      token: process.env.POST_TYPE_ID
    }
  }
}
</script>
