<template>
    <div class="max-w-5xl mx-auto">
        <div class="flex justify-center items-center relative">
            <img src="https://kusonime.com/wp-content/uploads/2017/09/Banner-Kusonime-2.png" alt="MiteNime"
                class="w-full">
            <div class="absolute text-white text-center">
                <h1 class="text-3xl md:text-4xl font-bold mb-4">Kusonime</h1>
            </div>
        </div>
        <Navbar />
        <NavRecom />

        <div class="md:flex w-full p-2 bg-white">
            <div class="w-3/4">
                <slot />
            </div>
            <div class="flex-shrink-0 md:w-64 w-1/4">
                <Sidebar />
            </div>
        </div>
        <Footer />
    </div>
</template>

<script>
import Footer from '../components/Footer.vue';
import Navbar from '../components/Navbar.vue';
import NavRecom from '../components/NavRecom.vue';
import Sidebar from '../components/Sidebar.vue';
export default {
    data() {
        return {
            //
        }
    },
    components: { Navbar, NavRecom, Sidebar, Footer }
}
</script>