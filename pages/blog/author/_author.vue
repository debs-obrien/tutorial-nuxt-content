<template>
  <div>
    <h1 class="text-4xl font-bold">Author: {{ articles[0].author.name }}</h1>
    <p class="mb-4">Bio: {{ articles[0].author.bio }}</p>
    <h3 class="mb-4">
      Here are a list of articles by {{ articles[0].author.name }}:
    </h3>
    <div
      v-for="article of articles"
      :key="article.slug"
      class="flex justify-between"
    >
      <div class="border-gray-300 border">
        <NuxtLink :to="`/blog/${article.slug}`">
          <img
            :src="require(`~/assets/img/${article.img}`)"
            :alt="article.alt"
          />
          <h2>{{ article.title }}</h2>
          <p>{{ article.description }}</p>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const articles = await $content('articles', params.slug)
      .where({
        'author.name': {
          $regex: [params.author, 'i']
        }
      })
      // .only(['title', 'slug', 'author', 'bio', 'description', 'alt', 'img'])
      .without('body')
      .sortBy('createdAt', 'asc')
      .fetch()
    return {
      articles
    }
  }
}
</script>
