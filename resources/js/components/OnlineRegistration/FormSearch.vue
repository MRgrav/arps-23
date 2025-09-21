<script setup lang="ts">
import { useForm } from '@inertiajs/vue3';
import { ref } from 'vue';
import Input from '../ui/input/Input.vue';
import Label from '../ui/label/Label.vue';
import Button from '../ui/button/Button.vue';

// Props passed from the parent component
defineProps({
    // Whether the alert should be visible
    show: Boolean,

    // Success message text
    message: {
        type: String,
        default: 'Your form was submitted successfully!'
    },

    // Registration ID to construct the PDF download URL
    id: {
        type: Number,
        default: 0
    }
})

const form = useForm({
    //student information
    dob: '',
    aadhaar_no: '',
});

// Search the form
const search = () => {
    form.post(route('online-registration.search'), {
        onSuccess: (data) => {
            form.reset();
        },
    })
}

</script>

<template>
    <!-- Alert box shown only if 'show' is true -->
    <div class="rounded relative m-8 py-8">
        <h2 class="mb-8">Download Registration Form</h2>
        <form @submit.prevent="search" class="gap-8 grid grid-cols-1 md:grid-cols-4 items-end">
            <div class="space-y-1 md:col-span-2">
                <Label for="aadhaar_no">Aadhaar Number (12 Digit): *</Label>
                <Input id="aadhaar_no" v-model="form.aadhaar_no" placeholder="AADHAAR NUMBER" required
                    class="bg-white" />
            </div>
            <div class="space-y-1 col-span-1">
                <Label for="dob">Date of Birth (MM-DD-YYYY): *</Label>
                <Input type="date" id="dob" v-model="form.dob" required class="bg-white" />
            </div>
            <div>
                <Button class="w-full">Search</Button>
            </div>
        </form>

    </div>
</template>
