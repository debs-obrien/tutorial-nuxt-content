<template>
  <div class="bg-gray-100 p-4">
    <h4 class="font-semibold">Author</h4>
    <p>
      <NuxtLink :to="`/blog/author/${author.name}`">
        {{ author.name }}
      </NuxtLink>
    </p>
    <p>{{ author.bio }}</p>
  </div>
</template>

<script>
export default {
  props: {
    author: {
      type: Object,
      required: true
    }
  }
}
</script>
