<template>  
    <div v-if="props.loading" class="flex justify-center items-center h-screen">
        <div class="animate-spin rounded-full h-10 w-10 border-t-2 border-b-2 border-gray-900">
            <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5 text-gray-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            </svg>
        </div>
    </div>
</template>
<script setup>


const props = defineProps({
    loading: {
        type: Boolean,
        default: false
    }
})


const startLoading = () =>{
    props.loading = true;
}

const stopLoading = () =>{
    props.loading = false
}

</script>