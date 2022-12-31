<template>
    <GuestLayout>
        <h1 class="text-md px-2 py-2 border-b-2 font-medium">Genres</h1>
        <div class="grid grid-cols-4 py-2 border-b">
            <nuxt-link v-for="season in data.data" :key="season.id" :to="'/seasons/' + season.slug" class="border-b">
                <div class="flex flex-col items-center justify-center hover:bg-gray-300">
                    <p class="text-sm py-4 px-4">{{ season.name }}</p>
                </div>
            </nuxt-link>
        </div>

    </GuestLayout>
</template>

<script>
import GuestLayout from '../../Layouts/GuestLayout.vue';

export default {
    data() {
        return {
            //
        };
    },
    async asyncData({ $config: { baseAPI_URL }, query }) {
        let page = 1;
        if (query.page) {
            page = query.page;
        }

        const response = await fetch(baseAPI_URL + '/api/v1/kusonime/seasons')
        const data = await response.json()

        return {
            data
        }
    },
    components: { GuestLayout }
}
</script>