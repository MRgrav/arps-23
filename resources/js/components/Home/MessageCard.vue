<script setup lang="ts">
import { Profile } from '@/types';
import defaultProfileIcon from '@/../../resources/images/defaults/profile.png';
import { Link } from '@inertiajs/vue3';
// import { BookOpenCheck } from 'lucide-vue-next';

interface Props {
    profiles: Profile[];
}
const props = defineProps<Props>();

const handleImageError = (event: Event) => {
    (event.target as HTMLImageElement).src = defaultProfileIcon;
};
</script>


<template>
    <div class="px-8 py-16">
        <div class="max-w-7xl mx-auto">
            <h2 class="text-center py-10 text-[#4e71ff]">Leadership Messages</h2>
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-10 py-10">
                <Link v-for="profile in props.profiles" :href="`/profiles/${profile.id}`" :key="profile.id"
                    class="bg-[var(--primary-brand-500)]/80 hover:scale-101 w-full max-w-[400px]  mx-auto transition duration-400 ease-in-out rounded-xs block shadow-md h-full">
                    <div class="-translate-1 hover:-translate-1.5 bg-white w-full h-full border-[var(--primary-brand-500)]/80 border hover:scale-99 transition duration-400 ease-in-out">
                        <div class="aspect-[4/3] object-center object-cover overflow-hidden">
                            <img v-if="profile.image" :src="`/storage/uploads/${profile.image}`"
                                class="w-full h-full object-cover" @error="handleImageError" alt="Profile Image" />
                            <img v-else :src="defaultProfileIcon" alt="">
                        </div>
                        <div class="p-4 relative">
                            <h3 class="text-[var(--primary-brand-500)] py-1">
                                {{ profile.role?.display_name || "name" }}
                            </h3>
                            <h4 class="text-slate-700">
                                {{ profile.name || "Please Select a Role" }}
                            </h4>
                            <p class="text-slate-500 max-t text-sm">
                                {{ profile?.message ? profile.message.slice(0, 220) + "..." : "No Message" }}
                            </p>
                        </div>
                    </div>
                </Link>
            </div>
        </div>
    </div>
</template>
