<template>
    <div>
        <div v-if="recom.length > 0" class="flex w-full text-sm bg-white">
            <div class="bg-gray-800 text-gray-300 px-4 py-2 flex-shrink-0">
                Rekomendasi Anime
            </div>
            <div class="w-full overflow-x-auto flex items-center px-2">
                <a :href="'/' + rec.slug" v-for="rec in recom" :key="rec.id" class="mr-2 flex-shrink-0 hover:text-blue-500">{{ rec.title }}</a>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            recom: []
        }
    },
    async created() {
        const res = await fetch(this.$config.baseAPI_URL + '/api/v1/kusonime/?limit=10')
        const data = await res.json()

        this.recom = data.data
    }
}
</script>