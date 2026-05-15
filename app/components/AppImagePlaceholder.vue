<script setup lang="ts">
withDefaults(
  defineProps<{
    label: string
    title?: string
    tone?: 'secondary' | 'accent' | 'primary' | 'surface'
  }>(),
  {
    title: '',
    tone: 'secondary',
  },
)

const toneClasses = {
  secondary: 'bg-[#E8EEF6]',
  accent: 'bg-[#DDEDEA]',
  primary: 'bg-[#FBEDE8]',
  surface: 'bg-[#F7F5F2]',
}
</script>

<template>
  <div
    class="flex h-full w-full items-end rounded-lg border border-[#E5E8ED] p-4"
    :class="toneClasses[tone]"
  >
    <div>
      <p class="text-xs font-medium uppercase tracking-[1px] text-[#9AA3B0]">{{ label }}</p>
      <p v-if="title" class="mt-1 text-sm font-medium text-[#6B7380]">{{ title }}</p>
    </div>
  </div>
</template>
