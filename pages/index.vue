<template>
  <main>
    <AppHome />

    <article class="prose-lg mx-auto p-4">
      <nuxt-content :document="article" />
    </article>
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
  head() {
    return {
      script: [
        { src: 'https://identity.netlify.com/v1/netlify-identity-widget.js' },
      ],
    }
  },
}
</script>
