<script setup lang="ts">
import AppLayout from '@/layouts/AppLayout.vue';
import { Registration, type Notification } from '@/types';
import { Link } from '@inertiajs/vue3';

interface Props {
    registrations: Registration[]
}

const props = defineProps<Props>();
</script>

<template>
    <AppLayout>
        <div class="p-8 lg:p-16">
            <h1 class="font-bold mb-4">Search Result</h1>

            <div class="my-4">
                <Link href="/online-registration" class="text-blue-600 hover:underline flex items-center">
                    <!-- Optional arrow icon -->
                    <svg class="w-4 h-4 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
                    </svg>
                    Back
                </Link>
            </div>


            <div class="space-y-4 my-8" v-if="props.registrations.length > 0" v-for="registration in props.registrations">
                <div class="w-full border border-gray-200 rounded-lg overflow-hidden">
                    <table class="w-full text-sm text-gray-600">
                        <tbody>
                            <tr class="bg-gray-100">
                                <td class="px-4 py-2 font-medium border w-1/3">ID</td>
                                <td class="px-4 py-2 border">{{ registration.id }}</td>
                            </tr>
                            <tr>
                                <td class="px-4 py-2 font-medium border">Applicant Name</td>
                                <td class="px-4 py-2 border">{{ registration.applicant_name }}</td>
                            </tr>
                            <tr class="bg-gray-100">
                                <td class="px-4 py-2 font-medium border">DOB</td>
                                <td class="px-4 py-2 border">{{ registration.dob }}</td>
                            </tr>
                            <tr>
                                <td class="px-4 py-2 font-medium border">Gender</td>
                                <td class="px-4 py-2 border">{{ registration.gender }}</td>
                            </tr>
                            <tr class="bg-gray-100">
                                <td class="px-4 py-2 font-medium border">Class Seeking</td>
                                <td class="px-4 py-2 border">{{ registration.admission_sought_for_class }}</td>
                            </tr>
                            <tr>
                                <td class="px-4 py-2 font-medium border">Father's Name</td>
                                <td class="px-4 py-2 border">{{ registration.father_name }}</td>
                            </tr>
                            <tr>
                                <td class="px-4 py-2 font-medium border">Mother's Name</td>
                                <td class="px-4 py-2 border">{{ registration.mother_name }}</td>
                            </tr>
                            <tr class="bg-gray-100">
                                <td class="px-4 py-2 font-medium border">Actions</td>
                                <td class="px-4 py-2 border">
                                    <a :href="`/online-registration/${registration.id}/pdf`" target="_blank"
                                        class="text-blue-600 hover:underline">Download Form</a>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <div v-else>
                <p class="text-red-500 text-center text-xl py-6">No registraion found.</p>
            </div>
        </div>
    </AppLayout>
</template>
