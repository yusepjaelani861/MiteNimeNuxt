<template>
    <div>
        <div class="flex text-sm mb-4">
            <div class="flex items-center">
                <p class="mr-2 border px-2 py-1">Page {{ page.current_page }} of {{ page.total_pages }}</p>
                <a v-if="page.prev_page !== null" :href="'?page=' + page.prev_page" class="px-2 py-1 border mr-1 hover:bg-gray-500 hover:text-white">«</a>
                <button class="px-2 py-1 border mr-1">...</button>
                <a v-if="page.next_page !== null" :href="'?page=' + page.next_page" class="px-2 py-1 border mr-1 hover:bg-gray-500 hover:text-white">»</a>
                <a :href="'?page=' + page.total_pages" class="px-2 py-1 border mr-1 hover:bg-gray-500 hover:text-white">Last »</a>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['page'],
    data() {
        return {
            //
        }
    }
}
</script>