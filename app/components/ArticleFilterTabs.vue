<script setup lang="ts">
defineProps<{
  items: Array<{
    label: string
    value: string
  }>
}>()

const model = defineModel<string>({ default: 'all' })
</script>

<template>
  <div class="overflow-x-auto">
    <div class="inline-flex min-w-max gap-1 rounded-lg bg-[#F8FAFC] p-1">
      <button
        v-for="item in items"
        :key="item.value"
        type="button"
        class="rounded px-3 py-1.5 text-sm font-medium transition-colors"
        :class="model === item.value
          ? 'bg-[#0A2540] text-[#FFFFFF]'
          : 'text-[#6B7380] hover:text-[#0B1220]'"
        @click="model = item.value"
      >
        {{ item.label }}
      </button>
    </div>
  </div>
</template>
