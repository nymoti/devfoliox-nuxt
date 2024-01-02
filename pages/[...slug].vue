<script setup>
import { ref } from 'vue'

const route = useRoute()
const slug = ref('')

if (route.params.slug) {
    let lastIndex = route.params.slug.length - 1
    if (!route.params.slug[lastIndex]) {
        slug.value = route.params.slug[lastIndex - 1]
    } else {
        slug.value = route.params.slug[lastIndex]
    }
} else {
    slug.value = 'home'
}

const { data, pending, error, refresh } = await useFetch('http://devfoliox.local/wp-json/wp/v2/pages', {
    query: { slug: slug.value }
})

</script>

<template>
    <main>
        <PrimaryMenu/>
        <Content :content="data[0].content.rendered"/>
        <!-- <h1>{{ data[0].title.rendered }}</h1>
        <div v-html="data[0].content.rendered"></div>-->
        <!-- {{data}} -->
        <!-- {{ slug }} -->
    </main>
</template>
