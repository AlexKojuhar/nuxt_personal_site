<template>
    <div class="container mx-auto max-w-4xl">
        <header class="flex justify-between items-start md:items-center mt-5">
            <div class="flex items-center md:space-x-12">
                <div class="hidden md:block">
                    <NuxtLink class="text-xl font-semibold p-2 hover:bg-gray-200 dark:hover:bg-gray-800" to="/">
                        Oleksandra Kozhukhar
                    </NuxtLink>
                </div>
                <Menu />
            </div>
            <ClientOnly>
                <ColorModeSelector />
            </ClientOnly>
        </header>
        <main class="p- mt-10">
            <slot />
        </main>
    </div>
</template>
<script setup>
useHead({
    titleTemplate: '%s - Oleksandra Kozhukhar'
})
</script>

<style>
body {
    font-family: 'Roboto', 'Courier New', Courier, monospace;
}

body {
    @apply bg-white dark:bg-gray-900 text-gray-700 dark:text-gray-300
}
</style>  
