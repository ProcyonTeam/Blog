<template>
  <main>{{ articles }}</main>
</template>
<script>
export default {
  async asyncData({ $content }) {
    const articles = await $content('articles').only(['title']).fetch()

    return {
      articles,
    }
  },
}
</script>
