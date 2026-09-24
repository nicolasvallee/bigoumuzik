<script setup lang="ts">
import * as alphaTab from '@coderline/alphatab'
import { onBeforeUnmount, onMounted, ref } from 'vue'

const props = defineProps<{
  src: string
  title: string
}>()

const scoreElement = ref<HTMLElement | null>(null)
let api: alphaTab.AlphaTabApi | null = null

onMounted(() => {
  if (!scoreElement.value) return

  api = new alphaTab.AlphaTabApi(scoreElement.value, {
    core: { engine: 'svg', fontDirectory: '/font/', useWorkers: false },
    display: { layoutMode: 'page', scale: 1 },
  })
  api.load(props.src)
})

onBeforeUnmount(() => {
  api?.destroy()
})
</script>

<template>
  <div class="mt-12 max-w-3xl overflow-hidden rounded-2xl border border-border bg-white px-4 py-5 text-foreground shadow-2xl shadow-black/10 sm:px-6">
    <div class="mb-4 flex items-baseline justify-between gap-4">
      <div>
        <p class="text-xs font-bold uppercase tracking-[0.18em] text-accent">A first sketch</p>
        <h2 class="mt-2 font-serif text-2xl font-normal sm:text-3xl">{{ title }}</h2>
      </div>
      <span class="text-xs text-foreground/60">1 measure</span>
    </div>
    <div ref="scoreElement" class="alpha-tab min-h-32 overflow-x-auto" aria-label="Rendered MusicXML score" />
  </div>
</template>

<style scoped>
.alpha-tab :deep(svg) {
  display: block;
  min-width: 560px;
  width: 100%;
}
</style>
