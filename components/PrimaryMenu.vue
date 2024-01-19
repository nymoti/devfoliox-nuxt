<template>
    <header class="header text-center">
        <nav class="navbar navbar-expand-lg navbar-dark" >

            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navigation" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
            </button>
            <div class="mobile-profile">
                <img class="mb-3 mx-auto profile-image" :src="personnalDetails.menuImage.url" alt="logo" >
            </div>
            <div id="navigation" class="collapse navbar-collapse flex-column" >
                <div class="profile">
                    <img class="mb-3 mx-auto profile-image" :src="personnalDetails.menuImage.url" alt="logo" >
                    <a class="site-title pt-lg-4 mb-0" href="/">
                        {{ personnalDetails.firstName + ' ' + personnalDetails.lastName }}
                        <span class="back-name">{{ personnalDetails.firstName + ' ' + personnalDetails.lastName }}</span>
                    </a>
                </div>
                <div class="menu">
                    <ul class="navbar-nav flex-column text-sm-center text-md-left">
                        <li class="nav-item"
                            v-for="item in navigation"
                            :key="item.name"
                            :class="item.href === current ? 'active' : undefined" >
                            <a class="nav-link" :href="item.href"><i class="fas fa-home fa-fw mr-2"></i> {{item.name}}</a>
                        </li>
                    </ul>
                </div>
                <div class="footer">
                    <ul class="social-list list-inline py-3 mx-auto">
                        <li class="list-inline-item">
                            <a :href="profileSocialMedia.github" target="_blank">
                                <Icon name="fa6-brands:github" />
                            </a>
                        </li>
                        <li class="list-inline-item">
                            <a :href="profileSocialMedia.linkedin" target="_blank">
                                <Icon name="fa6-brands:linkedin-in" />
                            </a>
                        </li>
                        <li class="list-inline-item">
                            <a :href="getMailtoLink(profileContactInfo.email)">
                                <Icon name="basil:gmail-outline" />
                            </a>
                        </li>
                    </ul>
                    <div class="copyright">
                        Copyright ©{{ new Date().getFullYear() +' '+ personnalDetails.firstName.substring(0, 1) + '. ' + personnalDetails.lastName }} .<br>
                        All right reserved.
                    </div>
                </div>
            </div>
        </nav>
    </header>
</template>

<script setup>
const route = useRoute()
// Replace 'http://localhost:3000' with your frontend location
const current = 'http://localhost:3000' + route.fullPath
// IMPORTANT
// console.log(route.path)
// If your frontend is http then use http
// in your useFetch endpoint
// If it is https then use https
// Replace 'http://wp.websitegoblin.com' with your backend location
const { data: navigation } = await useFetch('http://devfoliox.local/wp-json/wp/v2/primary-menu')
const { data: personnalDetails } = await useFetch('http://devfoliox.local/wp-json/wp/v2/personal-details')
const { data: profileSocialMedia } = await useFetch('http://devfoliox.local/wp-json/wp/v2/profile-social-media')
const { data: profileContactInfo } = await useFetch('http://devfoliox.local/wp-json/wp/v2/profile-contact-info')
const fullName = personnalDetails.firstName + ' ' + personnalDetails.lastName
const getMailtoLink = (email) => {
    const [user, domain] = email.split('@');
    const sanitizedUser = encodeURIComponent(user);
    return `mailto:${sanitizedUser}@${domain}`;
}

</script>