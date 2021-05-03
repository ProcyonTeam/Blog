<template>
  <main>
    <div class="md:flex lg:max-w-3/4 m-auto bg-gray-100">
      <div class="w-full md:w-2/3 lg:w-3/4">
        <SideItem>
          <article class="m-4 lg:m-2">
            <section>
              <h1 class="text-4xl font-bold">{{ article.title }}</h1>
              <div class="m-2">
                <fa icon="history" class="mr-2" />{{ getData }}
              </div>
              <div class="m-2">
                <fa icon="tags" class="mr-2" />
                <Tags v-for="tag of article.tags" :key="tag">{{ tag }}</Tags>
              </div>
            </section>

            <NuxtContent class="prose-lg" :document="article" />
          </article>
        </SideItem>
      </div>
      <div class="hidden md:w-1/3 lg:w-1/4 md:block">
        <div class="sticky top-0">
          <AppTableOfContents :article="article" />
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  async asyncData({ $content }) {
    const article = await $content('app', 'home').fetch()

    return {
      article,
    }
  },
  computed: {
    getData() {
      const date = new Date(this.article.updatedAt)
      const dateFormatted = date.toLocaleDateString('ja-JP')
      return dateFormatted
    },
  },
}
</script>
