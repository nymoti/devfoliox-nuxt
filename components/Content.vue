<template>
    <div class="main">
        <div v-html="content" class="wp-content"></div>
    </div>
</template>

<script setup>
const props = defineProps({
    content: String
})
</script>
