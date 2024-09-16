<template>
    <div class="container">
      <div>
        <h1 class="title">My Blog</h1>
      </div>
      <div class="posts">
        <div v-for="post in posts" :key="post._id">
          <h2><a v-bind:href="post.slug.current" v-text="post.title" /></h2>
          <div class="summary">
                <PortableText
                    :value="post.body[0]"
                    v-bind:key="post.body[0]._id"
                    v-if="post.body.length"
                />
            </div>
        </div>
      </div>
    </div>
</template>

<script setup>
    import { PortableText } from '@portabletext/vue';
    const query = groq`*[_type == "post"]`;
    const { data: posts, refresh } = useSanityQuery(query);
</script>