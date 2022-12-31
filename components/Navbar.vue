<template>
    <div class="w-full bg-gray-800 mb-2">
        <div class="md:flex justify-between p-1">
            <ul class="flex items-center md:mb-0 mb-2">
                <li class="px-2 py-1 hover:bg-slate-600"
                    :class="this.$route.path === '/' ? 'bg-slate-600' : ''"
                >
                    <nuxt-link to="/" class="text-white">Home</nuxt-link>
                </li>
                <li class="px-2 py-1 hover:bg-slate-600"
                    :class="this.$route.path === '/anime-list' ? 'bg-slate-600' : ''"
                >
                    <nuxt-link to="/anime-list" class="text-white">Anime List</nuxt-link>
                </li>
                <li class="px-2 py-1 hover:bg-slate-600"
                    :class="this.$route.path === '/genres' ? 'bg-slate-600' : ''"
                >
                    <nuxt-link to="/genres" class="text-white">Genres</nuxt-link>
                </li>
                <li class="px-2 py-1 hover:bg-slate-600"
                    :class="this.$route.path === '/seasons' ? 'bg-slate-600' : ''"
                >
                    <nuxt-link to="/seasons" class="text-white">Seasons</nuxt-link>
                </li>
            </ul>
            <form action="/search" method="GET" class="md:mb-0 mb-2">
                <input name="title" type="text" placeholder="Search" class="bg-gray-700 text-white px-2 py-1 rounded-l-none">
            </form>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            //
        }
    }
}
</script>