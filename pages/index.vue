<template>
  <GuestLayout>
    <h1 class="text-md px-2 py-2 border-b-2 font-medium">UPDATE TERBARU</h1>
    <Card v-for="data in data.data" :key="data.id" :anime="data" />
    <Pagination :page="data.pagination" />

    <h1 class="text-md px-2 py-2 border-b-2 font-medium">Rekomendasi Anime</h1>
    <div class="grid grid-cols-4 mb-4">
      <CardBox v-for="recom in recommend.data" :key="recom.id" :anime="recom" />
    </div>
  </GuestLayout>
</template>

<script>
import GuestLayout from '../Layouts/GuestLayout.vue';
import Card from '../components/Card.vue';
import CardBox from '../components/CardBox.vue';
import Pagination from '../components/Pagination.vue';

export default {
  components: { GuestLayout, Card, Pagination, CardBox },
  async asyncData({ $config: { baseAPI_URL }, query }) {
    if (query.page) {
      const response = await fetch(baseAPI_URL + '/api/v1/kusonime?page=' + query.page)
      const data = await response.json()

      const response_recommendation = await fetch(baseAPI_URL + '/api/v1/kusonime/?limit=12')
      const data_recommendation = await response_recommendation.json()

      return {
        data,
        recommend: data_recommendation
      }
    } else {
      const response = await fetch(baseAPI_URL + '/api/v1/kusonime')
      const data = await response.json()

      const response_recommendation = await fetch(baseAPI_URL + '/api/v1/kusonime/?limit=12')
      const data_recommendation = await response_recommendation.json()

      return {
        data,
        recommend: data_recommendation
      }
    }
  },
  data() {
    return {
      //
    }
  },
  head() {
    return {
      meta: [
        { name: 'description', content: 'MiteNime is a website that provides information about anime, manga, and light novel.' },
        { name: 'keywords', content: 'anime, manga, light novel, mitenime, mitenime.my.id' },
      ]
    }
  }
}
</script>
