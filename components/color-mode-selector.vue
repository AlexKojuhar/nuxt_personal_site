<template>
    <div class="flex space-x-2 items-center">
        <span class="text-gray-500 text-xs" v-if="showNextModeLable">Change to {{ nextMode }}</span>
        <button @mouseenter="showNextModeLable = true" @mouseleave="showNextModeLable = false" @click="toggleMode"
            class="hover:bg-gray-200 dark:hover:bg-gray-600 px-2 py-2 text-gray-500 text-2xl md:text-base">{{ nextModeIcon
            }}</button>
    </div>
</template>
<script setup>
const showNextModeLable = ref(false)
const colorMode = useColorMode()

const modes = [
    'system',
    'light',
    'dark'
]

const nextModeIcons = {
    system: '🌓',
    light: '🌕',
    dark: '🌑'
}

const nextMode = computed(() => {
    const currentModeIndex = modes.indexOf(colorMode.preference)
    let nextModeIndex = null
    if (currentModeIndex + 1 === modes.length) {
        nextModeIndex = 0
    }
    else {
        nextModeIndex = currentModeIndex + 1
    }
    return modes[nextModeIndex]
})

const nextModeIcon = computed(() => nextModeIcons[nextMode.value])

const toggleMode = () => colorMode.preference = nextMode.value

</script>