<script setup>
    defineProps(["inicio", "fin", "postLength"])
</script>

<template>
    <section class="flex gap-2 m-3 items-center">
        <button
            @click="$emit('previus')"
            :disabled="inicio === 0"
            class="rounded-md bg-slate-600 hover:bg-slate-300 hover:text-slate-200 duration-300 p-2 flex items-center gap-x-3"
            title="Save">
            <span class="text-sm font-bold pr-1 text-slate-200">Previus</span>
        </button>
        <p class="font-bold pr-1 text-slate-800">{{inicio + 1}} - {{fin}}</p>
        <button
            @click="$emit('next')"
            :disabled="fin >= postLength"
            class="rounded-md bg-slate-600 hover:bg-slate-300 hover:text-slate-200 duration-300 p-2 flex items-center gap-x-3"
            title="Save">
            <span class="text-sm font-bold pr-1 text-slate-200">Next</span>
        </button>
    </section>
</template>


