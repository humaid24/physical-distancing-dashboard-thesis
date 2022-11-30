<template>
    <Head title="Monitoring" />

    <BreezeAuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Monitoring
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">

                    <div class="p-6 bg-white border-b border-gray-200">
                        <h1 class="font-extrabold">Hi, {{ auth?.user?.name.toUpperCase() }} :) </h1>
                        Do you want to open {{ appName }}? Just press the button below. 
                    </div>
                </div>
            </div>
            <div class="mt-6 max-w-2xl mx-auto sm:px36 lg:max-w-7xl lg:px-8 lg:grid lg:grid-cols-3 lg:gap-x-8">
            
                <a type="button" :href="system_link" target="_blank" class="bg-blue-500 hover:bg-blue-700 text-white text-center py-2 px-4 rounded" :class="{ 'opacity-25': processing }" :disabled="processing" v-on:click="open_monitoring_window">{{processing ? 'Loading...' : 'Start Monitoring'}}</a>
            </div>
        </div>
    </BreezeAuthenticatedLayout>
</template>

<script>
import { ref } from 'vue'
import BreezeAuthenticatedLayout from '@/Layouts/Authenticated.vue'
import { Head } from '@inertiajs/inertia-vue3';
import http from '../utils/https';
export default {
    components: {
        BreezeAuthenticatedLayout,
        Head,
    },
    props:['appName', 'auth', 'system_link'],
    setup(props){
        const processing = ref(false)

         const open_monitoring_window = async () => {
           processing.value = true
           setTimeout(() => {processing.value = false}, 2000);
        }
        return {
            open_monitoring_window,
            processing
        }
    }
}
</script>
