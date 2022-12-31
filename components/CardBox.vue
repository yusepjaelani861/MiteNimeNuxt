<template>
    <div>
        <a :href="'/' + anime.slug">
            <div class="relative mr-1">
                <img :src="'https://i0.wp.com/' + $config.baseAPI_URL.replace('https://', '') + anime.image"
                    class="w-full h-32 object-contain" />
                <div class="bg-gradient-to-b from-transparent to-black absolute bottom-0 w-full p-1">
                    <div class="text-white text-sm font-medium line-clamp-3">{{ anime.title }}</div>
                </div>
            </div>
        </a>
    </div>
</template>

<script>
export default {
    props: ['anime'],
    data() {
        return {
            //
        }
    }
}
</script>