<script setup lang="ts">
import MusicXmlViewer from './MusicXmlViewer.vue'

const tracks = [
  { title: 'First note', src: '/music/first-note.musicxml' },
]
</script>

<template>
  <section id="back-to-batuk" class="flex min-h-svh items-center bg-background-soft px-5 pb-20 pt-32 scroll-mt-20 sm:px-16 lg:px-36" aria-labelledby="batuk-title">
    <div class="mx-auto w-full max-w-6xl">
      <p class="mb-6 text-xs font-bold uppercase tracking-[0.18em] text-accent">The next stop</p>
      <h2 id="batuk-title" class="max-w-[12ch] font-serif text-[clamp(3.25rem,9vw,8rem)] font-normal leading-[0.88]">Back to Batuk</h2>
      <MusicXmlViewer
        v-for="track in tracks"
        :key="track.src"
        :title="track.title"
        :src="track.src"
      />
    </div>
  </section>
</template>
