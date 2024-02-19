<template>
    <article
        class="prose dark:prose-invert max-w-none prose-pre:bg-white dark:prose-pre:bg-gray-800 prose-pre:text-gray-700 dark:prose-pre:text-gray-300">
        <ContentDoc>
            <template #not-found>
                <h1>Document not found</h1>
            </template>
            <template v-slot="{ doc }">
                <div class="grid grid-cols-6 gap-16">
                    <div :class="doc.toc ? 'col-span-6 md:col-span-4' : 'col-span-6'">
                        <ContentRenderer :value="doc" />
                    </div>
                    <div class="hidden md:block md:col-span-2 not-prose" v-if="doc.toc">
                        <aside class="sticky top-8">
                            <div class="font-semibold mb-2">
                                Table of Contents
                            </div>
                            <nav>
                                <TocLinks :links="doc.body.toc.links" :active-id="activeId" />
                            </nav>
                        </aside>
                    </div>
                </div>
            </template>
        </ContentDoc>
    </article>
</template>

<script setup>
const activeId = ref(null)

let observer = null
let elements = []

const callback = (entries) => {
    for (const entry of entries) {
        console.log(entry);
        if (entry.isIntersecting) {
            activeId.value = entry.target.id
            break
        }
    }
}

onMounted(() => {
    observer = new IntersectionObserver(callback, {
        root: null,
        threshold: 0.5,
        rootMargin: '20px'
    })
    elements = document.querySelectorAll('h2, h3')
    elements.forEach(element => {
        observer.observe(element)
    })
})

onBeforeUnmount(() => {
    elements.forEach(element => {
        observer.unobserve(element)
    })
})
</script>