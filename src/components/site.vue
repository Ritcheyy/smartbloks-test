<template>
    <div class="flex p-10 h-full">
        <h4 class="text-4xl">{{ title }}</h4>
    </div>
</template>

<script lang='ts' setup>
import { useRoute } from "vue-router";
import { computed } from "vue";

const route = useRoute()

const title = computed(() => route.query.title as string)
</script>

<style lang='postcss' scoped></style>