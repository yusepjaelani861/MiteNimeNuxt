<template>
    <GuestLayout>
        <h1 class="text-md px-2 py-2 border-b-2 font-medium">List Anime Batch Subtitle Indonesia</h1>
        <div class="flex flex-wrap mb-2">
            <a :href="'#' + letter" v-for="letter in alphabet" :key="letter.id" class="px-2 py-1 border mr-0.5 bg-black text-gray-500 text-sm text-justify">{{ letter }}</a>
        </div>

        <div class="w-full px-4 p-2" v-for="anime in data.data" :key="anime.id">
            <h1 :id="anime.letter" class="text-md px-2 py-2 border-b-2 border-blue-500 font-medium">{{ anime.letter }}</h1>
            <ul class="space-y-1 list-disc list-inside">
                <li v-for="list in anime.anime" :key="list.id">
                    <nuxt-link :to="'/' + list.slug" class="hover:text-blue-500">{{ list.title }}</nuxt-link>
                </li>
            </ul>
        </div>
        <Pagination :page="data.pagination" />
    </GuestLayout>
</template>

<script>
import GuestLayout from '../Layouts/GuestLayout.vue';
import Pagination from '../components/Pagination.vue';

export default {
    data() {
        return {
            alphabet: ['#', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
        };
    },
    async asyncData({ $config: { baseAPI_URL }, query }) {
        if (query.page) {
            const response = await fetch(baseAPI_URL + '/api/v1/kusonime/anime-list?page=' + query.page)
            const data = await response.json()

            return {
                data,
            }
        } else {
            const response = await fetch(baseAPI_URL + '/api/v1/kusonime/anime-list')
            const data = await response.json()

            return {
                data
            }
        }
    },
    components: { GuestLayout, Pagination }
}
</script>