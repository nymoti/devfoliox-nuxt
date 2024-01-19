<template>
    <div class="main" :class="activePage">
        <div v-html="content" class="wp-content container"></div>
        <div v-if="activePage === 'contact'">

    <div v-if="formHtml" v-html="formHtml"></div>
    <div v-else>Loading...</div>


            <div class="conact-form">
                <form action="http://devfoliox.local/wp-json/contact-form-7/v1/contact-forms/d45df23/feedback" method="post">
                <input id="name" type="text" name="name">
                <input id="email" type="email" name="email">
                <input id="subject" type="text" name="subject">
                <textarea id="message" name="message"></textarea>
                <button type="submit" class="btn btn-dark">Submit</button>
                </form>
            </div>
        </div>
        <Footer/>
    </div>
</template>

<script setup>
const props = defineProps({
    content: String,
    activePage: String
})


import { ref } from 'vue';

const formHtml = ref(null);

const fetchFormHtml = async () => {
  try {
    const response = await fetch('http://devfoliox.local/wp-json/contact-form-7/v1/contact-forms/d45df23');
    const formData = await response.json();
    formHtml.value = formData.form;
  } catch (error) {
    console.error('Error fetching form:', error.message);
  }
};

onMounted(() => {
  fetchFormHtml();
});
</script>
