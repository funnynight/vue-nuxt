<template>
  <article class="article--main-container">
    <AppButton
      button-text="Return to articles"
      name="blog"
      colour="greenColour"
    />

    <h1>{{ article.title }}</h1>
    <p>{{ formatDate(article.updatedAt) }}</p>
    <div>{{ article.intro }}</div>

    <img class="article--top-image" :src="require(`~/assets/images/articles/${article.img}`)" :alt="article.alt">
    <nuxt-content :document="article" />
    <AppButton
      button-text="Return to articles"
      name="blog"
      colour="greenColour"
    />
  </article>
</template>

<script>
export default {
  async asyncData ({ $content, params }) {
    // fetch our article here
    const article = await $content('articles', params.slug).fetch()

    return { article }
  },
  methods: {
    formatDate (date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' }
      return new Date(date).toLocaleDateString('en', options)
    }
  }
}
</script>

<style>
  .nuxt-content h2 {
    font-weight: bold;
    font-size: 28px;
  }
  .nuxt-content h3 {
    font-weight: bold;
    font-size: 22px;
  }
  .nuxt-content p {
    margin-bottom: 20px;
  }

  .icon.icon-link {
  background-image: url('~assets/svg/icon-hashtag.svg');
  display: inline-block;
  width: 20px;
  height: 20px;
  background-size: 20px 20px;
}
</style>
