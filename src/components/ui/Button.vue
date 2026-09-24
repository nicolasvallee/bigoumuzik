<script setup lang="ts">
import { Primitive } from 'reka-ui'
import { computed } from 'vue'
import { cva } from 'class-variance-authority'
import type { PropType } from 'vue'
import { cn } from '@/lib/utils'

const props = defineProps({
  as: { type: [String, Object] as PropType<string | object>, default: 'button' },
  variant: { type: String as PropType<'default' | 'ghost'>, default: 'default' },
  size: { type: String as PropType<'default' | 'sm'>, default: 'default' },
  class: { type: null as unknown as PropType<string | string[] | null>, default: null },
})

const buttonVariants = cva(
  'inline-flex items-center justify-center whitespace-nowrap rounded-full text-sm font-semibold transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-accent focus-visible:ring-offset-2 focus-visible:ring-offset-background disabled:pointer-events-none disabled:opacity-50',
  {
    variants: {
      variant: {
        default: 'bg-accent text-accent-foreground hover:bg-foreground hover:text-background',
        ghost: 'text-muted-foreground hover:bg-foreground/10 hover:text-foreground',
      },
      size: {
        default: 'h-10 px-4 py-2',
        sm: 'h-9 px-3',
      },
    },
    defaultVariants: { variant: 'default', size: 'default' },
  },
)

const classes = computed(() => cn(buttonVariants({ variant: props.variant, size: props.size }), props.class))
</script>

<template>
  <Primitive :as="as" :class="classes">
    <slot />
  </Primitive>
</template>
