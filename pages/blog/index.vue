<template>
  <div>
    <h1 class="font-bold text-4xl">Blog Posts</h1>
    <ul>
      <li v-for="post in posts" :key="post.slug">
        <NuxtLink
          :to="{ name: 'blog-slug', params: { slug: article.slug } }"
          class="hover:underline"
        >
          {{ post.title }} by {{ post.author }}
        </NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const posts = await $content('articles', params.slug)
      .only(['title', 'slug', 'author'])
      .sortBy('createdAt', 'asc')
      .fetch()
    return {
      posts
    }
  }
}
</script>
