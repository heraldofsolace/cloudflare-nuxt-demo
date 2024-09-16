<template>
    <div class="container">
        <div v-if="post">
            <h1 class="title" v-text="post.title" />
            <div class="content"> 
                <PortableText
                    :value="post.body"
                />


                </div>
        </div>
        <h4><a href="/">← Go back</a></h4>
    </div>
</template>

<script setup>
    import { PortableText } from '@portabletext/vue';
    const route = useRoute()
    const query = groq`*[_type == "post" && slug.current == "${route.params.slug}"][0]`;
    const { data: post } = useSanityQuery(query);
</script>

<style>
.container {
  margin: 2rem;
  min-height: 100vh;
}

.content {
  margin: 2rem 0;
  max-width: 38rem;
}

p {
  margin: 1rem 0;
}
</style>