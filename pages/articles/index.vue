<template>
  <main>{{ articles }}</main>
</template>
<script>
export default {
  async asyncData({ $content }) {
    const articles = await $content('articles').fetch()
    console.log(articles)
    return {
      articles,
    }
  },
}
</script>
