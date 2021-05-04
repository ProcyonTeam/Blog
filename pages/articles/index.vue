<template>
  <main class="container mx-auto">
    <div class="flex flex-wrap">
      <PostCard
        v-for="article in articles"
        :key="article.slug"
        :article="article"
      />
    </div>
  </main>
</template>
<script>
export default {
  async asyncData({ $content }) {
    const articles = await $content('articles').without(['body']).fetch()

    return {
      articles,
    }
  },
}
</script>
