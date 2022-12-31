<template>
    <div class="flex w-full p-2 mb-2 border-b">
        <div class="flex-shrink-0 mr-2 w-44">
            <img :src="'https://i0.wp.com/' + $config.baseAPI_URL.replace('https://', '') + anime.image"
                alt="One Piece" class="w-full h-24 object-cover">
        </div>
        <div class="w-full bg-gray-50 p-2 font-light">
            <nuxt-link :to="'/' + anime.slug" class="text-md font-medium mb-2 line-clamp hover:text-blue-500">{{ anime.title }}</nuxt-link>
            <p class="flex items-center text-xs">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-3 h-3 mr-1">
                    <path fill-rule="evenodd"
                        d="M7.5 6a4.5 4.5 0 119 0 4.5 4.5 0 01-9 0zM3.751 20.105a8.25 8.25 0 0116.498 0 .75.75 0 01-.437.695A18.683 18.683 0 0112 22.5c-2.786 0-5.433-.608-7.812-1.7a.75.75 0 01-.437-.695z"
                        clip-rule="evenodd" />
                </svg>
                <span>Posted by Admin</span>
            </p>
            <p class="flex items-center text-xs">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                    stroke="currentColor" class="w-3 h-3 mr-1">
                    <path stroke-linecap="round" stroke-linejoin="round"
                        d="M12 6v6h4.5m4.5 0a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
                <span>Released on {{ convertDate(anime.created_at) }}</span>
            </p>
            <div class="flex items-center text-xs w-full">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-3 h-3 mr-1">
                    <path fill-rule="evenodd"
                        d="M5.25 2.25a3 3 0 00-3 3v4.318a3 3 0 00.879 2.121l9.58 9.581c.92.92 2.39 1.186 3.548.428a18.849 18.849 0 005.441-5.44c.758-1.16.492-2.629-.428-3.548l-9.58-9.581a3 3 0 00-2.122-.879H5.25zM6.375 7.5a1.125 1.125 0 100-2.25 1.125 1.125 0 000 2.25z"
                        clip-rule="evenodd" />
                </svg>
                <span class="">Genre <span v-for="genre in anime.genres" :key="genre.id"><nuxt-link :to="'/genres/' + genre.slug" class="text-blue-500 hover:text-blue-700">{{ genre.name }}</nuxt-link>, </span></span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['anime'],
    data() {
        return {

        }
    },
    methods: {
        convertDate(date) {
            // 30 Dec, 2022
            return new Date(date).toLocaleDateString('en-GB', {
                day: 'numeric',
                month: 'short',
                year: 'numeric'
            })
        }
    }
}
</script>