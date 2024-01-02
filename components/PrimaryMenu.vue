<template>

    <header class="header text-center">
            <a class="site-title pt-lg-4 mb-0" href="index.html">Devfoliox-nuxt</a>

            <nav class="navbar navbar-expand-lg navbar-dark" >

                <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navigation" aria-controls="navigation" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
                </button>

                <div id="navigation" class="collapse navbar-collapse flex-column" >
                    <img class="mb-3 mx-auto logo" src="" alt="logo" >

                    <ul class="navbar-nav flex-column text-sm-center text-md-left">
                        <li class="nav-item active"
                            v-for="item in navigation"
                            :key="item.name"
                            :class="item.href === current ? 'active' : undefined" >
                            <a class="nav-link" :href="item.href"><i class="fas fa-home fa-fw mr-2"></i> {{item.name}}</a>
                        </li>
                    </ul>
                    <hr>
                    <ul class="social-list list-inline py-3 mx-auto">
                        <li class="list-inline-item"><a href="#"><i class="fab fa-twitter fa-fw"></i></a></li>
                        <li class="list-inline-item"><a href="#"><i class="fab fa-linkedin-in fa-fw"></i></a></li>
                        <li class="list-inline-item"><a href="#"><i class="fab fa-github-alt fa-fw"></i></a></li>
                        <li class="list-inline-item"><a href="#"><i class="fab fa-stack-overflow fa-fw"></i></a></li>
                        <li class="list-inline-item"><a href="#"><i class="fab fa-codepen fa-fw"></i></a></li>
                    </ul>

                </div>
            </nav>
    </header>
</template>

<script setup>
const route = useRoute()
// Replace 'http://localhost:3000' with your frontend location
const current = 'http://localhost:3000' + route.fullPath
// IMPORTANT
// If your frontend is http then use http
// in your useFetch endpoint
// If it is https then use https
// Replace 'http://wp.websitegoblin.com' with your backend location
const { data: navigation, pending, error, refresh } = await useFetch('http://devfoliox.local/wp-json/wp/v2/primary-menu');

</script>