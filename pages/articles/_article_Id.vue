<template>
  <main>
    <div class="md:flex lg:max-w-3/4 m-auto bg-gray-100">
      <div class="w-full md:w-2/3 lg:w-3/4">
        <SideItem>
          <article class="m-4 lg:m-2">
            <section class="pb-4">
              <h1 class="text-4xl font-bold">{{ article.title }}</h1>
              <div class="m-2">
                <fa icon="history" class="mr-2" />{{ getData }}
              </div>
              <div class="m-2">
                <fa icon="tags" class="mr-2" />
                <Tags v-for="tag of article.tags" :key="tag">{{ tag }}</Tags>
              </div>
              <nuxt-img :src="`/images/${article.ogpImageName}`" />
            </section>

            <NuxtContent class="prose-lg" :document="article" />
          </article>
        </SideItem>
      </div>
      <div class="hidden md:w-1/3 lg:w-1/4 md:block">
        <div class="sticky top-0">
          <SideItem v-if="member" class="">
            <h2 class="text-2xl border-b-2 p-1">投稿者</h2>
            <section class="flex items-center m-2">
              <nuxt-img :src="member.icon" class="rounded-full h-16 border-2" />
              <div class="">
                <h2 class="text-xl font-semibold pl-2">{{ member.name }}</h2>
                <p class="pl-3 text-sm">{{ member.appeal }}</p>
              </div>
            </section>
          </SideItem>
          <AppTableOfContents :article="article" />
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const article = await $content('articles', params.article_Id).fetch()

    const member = (await $content('members').fetch()).find(
      (mem) => mem.name === article.contributor
    )
    return {
      article,
      member,
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
