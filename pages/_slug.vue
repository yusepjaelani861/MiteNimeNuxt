<template>
    <GuestLayout>
        <div class="px-2">
            <img :src="'https://i0.wp.com/' + $config.baseAPI_URL.replace('https://', '') + anime.image"
                :alt="anime.title" class="w-full max-h-96 object-contain mb-2">
            <div class="flex justify-between items-center border-b uppercase font-medium text-sm py-1 mb-4">
                <div class="flex items-center">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor"
                        class="w-4 h-4 mr-1">
                        <path fill-rule="evenodd"
                            d="M7.5 6a4.5 4.5 0 119 0 4.5 4.5 0 01-9 0zM3.751 20.105a8.25 8.25 0 0116.498 0 .75.75 0 01-.437.695A18.683 18.683 0 0112 22.5c-2.786 0-5.433-.608-7.812-1.7a.75.75 0 01-.437-.695z"
                            clip-rule="evenodd" />
                    </svg>
                    <span>Posted by Admin On </span> <span> {{ convertDate(anime.created_at) }}</span>
                </div>
                <!-- <p class="flex items-center">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor"
                        class="w-5 h-5 mr-1">
                        <path d="M12 15a3 3 0 100-6 3 3 0 000 6z" />
                        <path fill-rule="evenodd"
                            d="M1.323 11.447C2.811 6.976 7.028 3.75 12.001 3.75c4.97 0 9.185 3.223 10.675 7.69.12.362.12.752 0 1.113-1.487 4.471-5.705 7.697-10.677 7.697-4.97 0-9.186-3.223-10.675-7.69a1.762 1.762 0 010-1.113zM17.25 12a5.25 5.25 0 11-10.5 0 5.25 5.25 0 0110.5 0z"
                            clip-rule="evenodd" />
                    </svg>
                    <span>0 Views</span>
                </p> -->
            </div>

            <div class="grid grid-cols-2 mb-4">
                <div class="bg-blue-50 px-2 py-1 mr-2 mb-2">
                    <strong>Japanese:</strong> {{ anime.title }}
                </div>
                <div class="bg-blue-50 px-2 py-1 mb-2 break-words">
                    <strong>Genre: </strong> <nuxt-link class="text-blue-500 hover:text-blue-700 mr-1"
                        v-for="genre in anime.genres" :to="/genres/ + genre.slug">{{ genre.name }}</nuxt-link>
                </div>
                <div class="bg-blue-50 px-2 py-1 mr-2 mb-2">
                    <strong>Seasons:</strong> <a v-for="season in anime.seasons" :href="'/seasons/' + season.slug"
                        class="text-blue-500 hover:text-blue-700 mr-1">{{ season.name }}</a>
                </div>
                <div class="bg-blue-50 px-2 py-1 mb-2">
                    <strong>Producers:</strong> {{ anime.producers }}
                </div>
                <div class="bg-blue-50 px-2 py-1 mr-2 mb-2">
                    <strong>Type:</strong> {{ anime.type }}
                </div>
                <div class="bg-blue-50 px-2 py-1 mb-2">
                    <strong>Status:</strong> {{ anime.status }}
                </div>
                <div class="bg-blue-50 px-2 py-1 mr-2 mb-2">
                    <strong>Total Episode:</strong> {{ anime.total_episode }}
                </div>
                <div class="bg-blue-50 px-2 py-1 mb-2">
                    <strong>Score:</strong> {{ anime.score }}
                </div>
                <div class="bg-blue-50 px-2 py-1 mr-2 mb-2">
                    <strong>Duration:</strong> {{ anime.duration }}
                </div>
                <div class="bg-blue-50 px-2 py-1 mb-2">
                    <strong>Released on:</strong> {{ convertDate(anime.created_at) }}
                </div>
            </div>

            <p class="text-justify mb-4 font-light">
                {{  anime.description }}
            </p>

            <div class="bg-gray-300 p-1 mb-4">
                <div class="bg-gray-800 text-gray-300 px-4 py-2 mb-2 border-l-4 border-blue-500">
                    Download {{ anime.title }}
                </div>
                <div class="bg-white overflow-auto">
                    <div v-for="download in anime.downloads"
                        class="bg-white shadow-sm md:text-xs w-full text-md text-center text-gray-700 md:flex items-center p-2 mr-2">
                        <p class="bg-slate-700 text-white py-1 px-2 mr-2 text-center">{{ download.quality }}</p>
                        <div class="break-words flex items-center md:justify-start justify-center">
                            <div v-for="url in download.downloads" class="mr-2"
                                :key="url.id">
                                <a :href="url.url" class="hover:text-blue-500">{{ url.name }}</a>
                            </div>
    
                        </div>
                    </div>
                </div>
            </div>

            <h1 class="text-md px-2 py-2 border-b-2 font-medium">Rekomendasi Series</h1>
            <Card v-for="recom in recommen.data" :key="recom.id" :anime="recom" />
        </div>
    </GuestLayout>
</template>

<script>
import GuestLayout from '../Layouts/GuestLayout.vue';
import Card from '../components/Card.vue';
export default {
    data() {
        return {
            //
        }
    },

    async asyncData({ params, $config: { baseAPI_URL }, req }) {
        const response = await fetch(baseAPI_URL + '/api/v1/kusonime/' + params.slug)
        const data = await response.json()

        if (data.status === 404) {
            return {
                notFound: true
            }
        }

        const response_recommendation = await fetch(baseAPI_URL + '/api/v1/kusonime/?limit=5')
        const data_recommendation = await response_recommendation.json()

        const myUrl = req ? req.headers.host : window.location.host.split(':')[0]

        return {
            anime: data.data,
            recommen: data_recommendation,
            myUrl
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
    },
    components: { GuestLayout, Card },
    head() {
        return {
            title: this.anime.title + ' | MiteNime',
            meta: [
                { name: 'description', content: this.anime.description.substring(0, 150) + '...' },
                { name: 'keywords', content: this.anime.genres.map(genre => genre.name).join(', ') + ', ' + this.anime.title },
                { name: 'og:title', content: this.anime.title },
                { name: 'og:description', content: this.anime.description.substring(0, 150) + '...' },
                { name: 'og:image', content: this.anime.thumbnail },
                { name: 'og:url', content: 'https://' + this.myUrl + '/' + this.anime.slug },
                { name: 'og:type', content: 'website' },
                { name: 'twitter:title', content: this.anime.title },
                { name: 'twitter:description', content: this.anime.description.substring(0, 150) + '...' },
                { name: 'twitter:image', content: this.anime.thumbnail },
                { name: 'twitter:card', content: 'summary_large_image' },
            ],
            link: [
                { rel: 'canonical', href: 'https://' + this.myUrl + '/' + this.anime.slug }
            ]
        }
    }
}
</script>