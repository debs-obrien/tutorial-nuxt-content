---
title: My Second Blog Post
description: Learning how to use @nuxt/content to create a blog
img: first-blog-post.jpg
alt: my first blog post
author: 
  name: Debbie
  bio: All about Benjamin
---

Welcome to my second blog post using content module

## This is a heading
This is some more info
<div class="bg-blue-500 text-white p-4 mb-4">
  This is HTML inside markdown that has a class some classes
</div>

<info-box>
  <template #info-box>
    This is a vue component inside markdown using slots
  </template>
</info-box>

```js
export default {
  nuxt: "is the best"
}
```
```html
<p>code styling is easy</p>
```

### This is a sub heading
This is some more info

### This is another sub heading
This is some more info

## This is another heading
This is some more info

<author :author="author" :bio="bio" />
