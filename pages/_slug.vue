<template>
  <section class="section">
    <div>slug: {{ msg }}</div>
  </section>
</template>

<script>
export default {
  asyncData (context) {
    return {
      msg: context.params.slug
    }
  }
}
</script>
