<template>
  <main class="container mx-auto">
    <div class="flex flex-wrap">
      <div
        v-for="article in articles"
        :key="article.slug"
        to="#"
        class="sm:w-1/2 p-4"
      >
        <NuxtLink :to="`/articles/${article.slug}`">
          <div
            class="border-2 rounded-lg transform hover:scale-95 transition duration-200"
          >
            <nuxt-img
              :src="`/images/${article.ogpImageName}`"
              class="rounded-t-lg"
            />
            <div class="m-2">
              <fa icon="history" class="mr-2" />{{ getData(article.updatedAt) }}
            </div>
            <div class="text-2xl font-semibold p-2">{{ article.title }}</div>
          </div>
        </NuxtLink>
      </div>
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
  methods: {
    getData(dateAt) {
      const date = new Date(dateAt)
      const dateFormatted = date.toLocaleDateString('ja-JP')
      return dateFormatted
    },
  },
}
</script>
