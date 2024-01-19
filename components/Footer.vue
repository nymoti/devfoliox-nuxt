<template>
    <div class="footer container">
        <p class="copyright">
            Copyright © All right reserved.
        </p>

        <p class="profile-name">
            {{ personnalDetails.firstName + ' ' + personnalDetails.lastName }}
        </p>

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
    </div>
</template>

<script setup>
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