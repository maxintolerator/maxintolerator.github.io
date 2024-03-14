<script setup>
import { ref, computed } from 'vue'
import { useMouseInElement } from '@vueuse/core'
const props = defineProps({
    image: {
        type: String,
        required: false
    },
    color: {
        type: String,
        required: false
    },
    head: {
        type: String,
        required: false
    },
    body: {
        type: String,
        required: true
    },
    classes: {
        type: String,
        required: false
    },
    link: {
        type: String,
        required: false
    }
})
const target = ref(null)
const { elementX, elementY, isOutside, elementHeight, elementWidth } =
    useMouseInElement(target)
const cardTransform = computed(() => {
    const MAX_ROTATION = 10
    const rX = (
        MAX_ROTATION / 2 -
        (elementY.value / elementHeight.value) * MAX_ROTATION
    ).toFixed(2) // handles x-axis
    const rY = (
        (elementX.value / elementWidth.value) * MAX_ROTATION -
        MAX_ROTATION / 2
    ).toFixed(2) // handles y-axis
    return isOutside.value
        ? ''
        : `perspective(${elementWidth.value}px) rotateX(${rX}deg) rotateY(${rY}deg)`
})
</script>
<template>
    <q-card
        :class="classes"
        ref="target"
        :style="{
            transform: cardTransform,
            transition: 'transform 0.25s ease-out'
        }"
    >
        <q-card-section
            v-if="image"
            class="row justify-center items-center"
            style="width: 50%; margin: 0 auto; min-height: 120px"
        >
            <a :href="link" target="_blank"
                ><img :src="image" style="height: 100px"
            /></a>
        </q-card-section>
        <q-separator
            v-if="image"
            class="q-my-sm"
            style="width: 94%; margin: 0 auto; 'color: ' + color"
        />
        <q-card-section :style="'color: ' + color">
            <div class="head-3 q-mb-lg" v-if="head" v-html="head" />

            <div class="text-body1" v-html="body" />
        </q-card-section>
    </q-card>
</template>
