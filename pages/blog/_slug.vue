<template>
  <article>
    <h1 class="font-bold text-4xl">{{ article.title }}</h1>
    <p>{{ article.description }}</p>
    <img :src="require(`~/assets/img/${article.img}`)" :alt="article.alt" />
    <p class="pb-4">Post last updated: {{ formatDate(article.updatedAt) }}</p>
    <nav class="pb-6">
      <ul>
        <li
          v-for="link of article.toc"
          :key="link.id"
          :class="{
            'font-semibold': link.depth === 2
          }"
        >
          <nuxtLink
            :to="`#${link.id}`"
            class="hover:underline"
            :class="{
              'py-2': link.depth === 2,
              'ml-2 pb-2': link.depth === 3
            }"
            >{{ link.text }}</nuxtLink
          >
        </li>
      </ul>
    </nav>
    <nuxt-content :document="article" />

    <author :author="article.author" />

    <PrevNext :prev="prev" :next="next" class="lg:px-8 mt-4" />
  </article>
</template>
<script>
export default {
  async asyncData({ $content, params }) {
    const article = await $content('articles', params.slug).fetch()
    const [prev, next] = await $content('articles')
      .only(['title', 'slug'])
      .sortBy('createdAt', 'asc')
      .surround(params.slug)
      .fetch()
    return {
      article,
      prev,
      next
    }
  },
  methods: {
    formatDate(date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' }
      return new Date(date).toLocaleDateString('en', options)
    }
  }
}
</script>
<style>
.nuxt-content p {
  margin-bottom: 20px;
}
.nuxt-content h2 {
  font-weight: bold;
  font-size: 28px;
}
.nuxt-content h3 {
  font-weight: bold;
  font-size: 22px;
}
.icon.icon-link {
  background-image: url('~assets/svg/icon-hashtag.svg');
  display: inline-block;
  width: 20px;
  height: 20px;
  background-size: 20px 20px;
}
</style>
