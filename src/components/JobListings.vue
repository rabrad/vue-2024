<script setup lang="ts">
import { onMounted, reactive } from 'vue';
import JobListing from '@/components/JobListing.vue';
import { RouterLink } from 'vue-router';
import PulseLoader from 'vue-spinner/src/PulseLoader.vue'

interface Job {
    id: number;
    title: string;
    description: string;
    type: string;
    salary: string;
    location: string;
    company: {
        name: string;
        description: string;
        contactEmail: string;
        contactPhone: string;
    };
}

interface Props {
    limit?: number;
    showButton?: boolean;
}

const props = withDefaults(defineProps<Props>(), {
    limit: undefined,
    showButton: false
});

const state = reactive<{
    jobs: Job[];
    isLoading: boolean;
}>({
    jobs: [],
    isLoading: true
});

onMounted(async () => {
    try {
        const response = await fetch('/api/jobs')
        const jobData: Job[] = await response.json();
        state.jobs = jobData;
    } catch (error) {
        console.error('Error fetching jobs:', error);
    } finally {
        state.isLoading = false
    }
})
</script>

<template>

    <section class="bg-green-50 px-4 py-10">
        <div class="container-xl lg:container m-auto">
            <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
                Browse Jobs
            </h2>
            <!-- Show loading while fetching-->
            <div v-if="state.isLoading" class="text-center text-gray-400">
                <PulseLoader />
            </div>
            <!-- Show Data after fetching-->
            <div v-else class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <JobListing v-for="job in state.jobs.slice(0, limit || state.jobs.length)" :key="job.id" :job="job" />
            </div>
        </div>
    </section>
    <section v-if="showButton" class="m-auto max-w-lg my-10 px-6">
        <RouterLink to="/jobs" class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700">View
            All Jobs</RouterLink>
    </section>


</template>