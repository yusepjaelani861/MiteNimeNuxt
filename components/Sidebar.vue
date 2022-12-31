<template>
    <div>
        <!-- <div class="bg-gray-800 text-gray-300 px-4 py-2 mb-2 border-l-4 border-blue-500">
            Rekomendasi Anime
        </div>
        <div class="px-2">
            <p v-for="i in 5" :key="i" class="mr-2">Hahahaha</p>
        </div> -->

        <div class="bg-gray-800 text-gray-300 px-4 py-2 mb-2 border-l-4 border-blue-500">
            Genres
        </div>
        <div class="overflow-y-auto h-32 mb-4 px-2">
            <div class="grid grid-cols-3">
                <a :href="'/genres/' + genre.slug" v-for="genre in genres" :key="genre.id"
                    class="px-1 py-1 mb-2 bg-gray-700 hover:bg-gray-900 text-white text-center text-sm block rounded line-clamp mr-0.5">
                    {{ genre.name }}
                </a>
            </div>
        </div>

        <div class="bg-gray-800 text-gray-300 px-4 py-2 mb-2 border-l-4 border-blue-500">
            Seasons
        </div>
        <div class="overflow-y-auto h-32 mb-4 px-2">
            <div class="grid grid-cols-3">
                <a :href="'/seasons/' + season.slug" v-for="season in seasons" :key="season.id"
                    class="px-1 py-1 mb-2 block bg-gray-700 hover:bg-gray-900 text-white text-center text-sm rounded line-clamp mr-0.5">
                    {{ season.name }}
                </a>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            genres: [],
            seasons: []
        }
    },
    async created() {
        const res = await fetch(this.$config.baseAPI_URL + '/api/v1/kusonime/genres')
        const data = await res.json()

        this.genres = data.data

        const res2 = await fetch(this.$config.baseAPI_URL + '/api/v1/kusonime/seasons')
        const data2 = await res2.json()

        this.seasons = data2.data
    }
}
</script>