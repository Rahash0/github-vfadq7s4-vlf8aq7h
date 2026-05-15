<template>
  <aside class="space-y-6">
    <nav class="space-y-3">
      <p class="text-xs font-medium uppercase tracking-[1px] text-dimmed">Table of contents</p>
      <ul class="space-y-2 text-sm text-muted">
        <li>
          <a href="#overview" class="hover:text-[#0B1220]">Overview</a>
        </li>
        <li>
          <a href="#where-to-start" class="hover:text-[#0B1220]">Where to start</a>
        </li>
        <li>
          <a href="#local-notes" class="hover:text-[#0B1220]">Local notes</a>
        </li>
      </ul>
    </nav>

    <div class="border border-[#E5E8ED] bg-[#FFFFFF] p-4">
      <p class="font-semibold text-highlighted">Build a Beyongo itinerary</p>
      <p class="mt-2 text-sm text-muted">
        Save this guide and turn the best stops into a simple day plan.
      </p>
      <UButton
        class="mt-4"
        label="Start planning"
        color="primary"
        :ui="{ base: 'bg-[#D84F2A] hover:bg-[#BE4423] active:bg-[#BE4423] text-white focus-visible:outline-[#D84F2A]' }"
      />
    </div>

    <slot />
  </aside>
</template>
