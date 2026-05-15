<script setup lang="ts">
const props = defineProps<{
  total: number
  itemsPerPage: number
}>()

const page = defineModel<number>('page', { default: 1 })

const pageCount = computed(() => Math.max(1, Math.ceil(props.total / props.itemsPerPage)))

const paginationItems = computed(() => {
  const count = pageCount.value
  const current = page.value

  if (count <= 7) {
    return Array.from({ length: count }, (_, index) => index + 1)
  }

  const items: Array<number | 'ellipsis'> = [1]

  if (current > 4) {
    items.push('ellipsis')
  }

  const start = Math.max(2, current - 1)
  const end = Math.min(count - 1, current + 1)

  for (let value = start; value <= end; value += 1) {
    items.push(value)
  }

  if (current < count - 3) {
    items.push('ellipsis')
  }

  items.push(count)

  return items
})

const setPage = (value: number) => {
  page.value = Math.min(Math.max(value, 1), pageCount.value)
}
</script>

<template>
  <div class="flex w-full justify-center pt-8">
    <nav class="mx-auto flex w-fit items-center justify-center gap-6 text-sm font-semibold text-[#6B7380]" aria-label="Pagination">
      <button
        type="button"
        class="flex items-center gap-1.5 bg-transparent px-2.5 py-1.5 text-[#6B7380] transition-colors hover:text-[#0B1220] disabled:cursor-not-allowed disabled:text-[#9AA3B0]"
        :disabled="page <= 1"
        @click="setPage(page - 1)"
      >
        <span aria-hidden="true" class="text-2xl leading-none">&lsaquo;</span>
        <span>Prev</span>
      </button>

      <template v-for="(item, index) in paginationItems" :key="`${item}-${index}`">
        <span
          v-if="item === 'ellipsis'"
          class="px-1 text-[#6B7380]"
        >
          ...
        </span>
        <button
          v-else
          type="button"
          class="flex items-center justify-center gap-1.5 border-0 bg-transparent px-2.5 py-1.5 text-[#6B7380] shadow-none transition-colors hover:text-[#0B1220]"
          :class="item === page ? 'rounded-md !bg-[#D84F2A] !text-white hover:!text-white' : ''"
          @click="setPage(item)"
        >
          {{ item }}
        </button>
      </template>

      <button
        type="button"
        class="flex items-center gap-1.5 bg-transparent px-2.5 py-1.5 text-[#6B7380] transition-colors hover:text-[#0B1220] disabled:cursor-not-allowed disabled:text-[#9AA3B0]"
        :disabled="page >= pageCount"
        @click="setPage(page + 1)"
      >
        <span>Next</span>
        <span aria-hidden="true" class="text-2xl leading-none">&rsaquo;</span>
      </button>
    </nav>
  </div>
</template>
