<template>
    <GuestLayout>
        <h1 class="text-md px-2 py-2 border-b-2 font-medium">Seasons {{ season }}</h1>
        <Card v-for="data in data.data" :key="data.id" :anime="data" />
        <Pagination :page="data.pagination" />
    </GuestLayout>
</template>

<script>
import GuestLayout from '../../Layouts/GuestLayout.vue';
import Card from '../../components/Card.vue';
import Pagination from '../../components/Pagination.vue';



export default {
    data() {
        return {
            season: this.$route.params.slug
        };
    },
    async asyncData({ $config: { baseAPI_URL }, query, params }) {
        let page = 1;
        if (query.page) {
            page = query.page;
        }

        const response = await fetch(baseAPI_URL + '/api/v1/kusonime/seasons/' + params.slug + '?page=' + page)
        const data = await response.json()

        return {
            data
        }
    },
    components: { GuestLayout, Card, Pagination }
}
</script>