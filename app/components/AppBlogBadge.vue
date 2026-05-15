<script setup lang="ts">
defineProps<{
  label: string
}>()
</script>

<template>
  <span class="inline-flex rounded text-[10px] font-bold uppercase leading-3 tracking-[1px] text-[#D84F2A]">
    {{ label }}
  </span>
</template>
