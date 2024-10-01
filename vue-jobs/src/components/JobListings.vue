<script setup>
import JobListin from './JobListin.vue';
import JobData from '@/jobs.json';
import {ref, defineProps } from 'vue';

const jobs = ref (JobData);

defineProps({ 
    limit: Number
 });

</script>

<template>  
    <section class="bg-blue-50 px-4 py-10 " >
        <div class="container-xl lg:container m-auto ">
            <h2 class="text-3xl font-bold text-green-500 text-center mb-6 ">
                Serviços
            </h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <JobListin v-for="job in jobs.slice(0, limit || jobs.length  ) " :key="job.id" :job="job"/>
            </div>
        </div>

    </section>



    
</template>