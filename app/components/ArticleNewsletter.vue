<template>
  <section class="border-y border-[#E5E8ED] bg-[#FFFFFF] py-8">
    <div class="mx-auto flex max-w-6xl flex-col gap-5 px-4 md:flex-row md:items-center md:justify-between">
      <div>
        <p class="font-mono text-xs uppercase text-dimmed">Beyongo notes</p>
        <h2 class="mt-2 text-2xl font-semibold text-highlighted">Plan your stay with clearer local guidance.</h2>
        <p class="mt-2 max-w-2xl text-sm text-muted">
          Get thoughtful travel ideas, neighborhood picks, and practical planning notes.
        </p>
      </div>

      <div class="flex flex-wrap gap-3">
        <UButton
          label="Explore experiences"
          color="primary"
          :ui="{ base: 'bg-[#D84F2A] hover:bg-[#BE4423] active:bg-[#BE4423] text-white focus-visible:outline-[#D84F2A]' }"
        />
        <UButton
          label="View stays"
          color="neutral"
          variant="outline"
          :ui="{ base: 'bg-[#FFFFFF] text-[#0A2540] ring-[#E5E8ED] hover:bg-[#E8EEF6] active:bg-[#E8EEF6]' }"
        />
      </div>
    </div>

    <slot />
  </section>
</template>
