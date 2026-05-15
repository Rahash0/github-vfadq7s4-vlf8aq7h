<template>
  <header class="border-b border-[#E5E8ED] bg-[#FFFFFF]">
    <div class="mx-auto flex h-14 max-w-6xl items-center justify-between px-4">
      <a href="#" class="text-base font-extrabold tracking-normal text-[#0A2540]" @click.prevent>
        BEYONGO<span class="text-[#D84F2A]">.</span>
      </a>

      <nav class="hidden items-center gap-8 md:flex">
        <a
          v-for="item in ['Destinations', 'Editorial', 'Collections', 'About']"
          :key="item"
          href="#"
          class="text-[10px] font-bold uppercase tracking-[0.18em] text-[#2B3340] hover:text-[#D84F2A]"
          @click.prevent
        >
          {{ item }}
        </a>
      </nav>

      <div class="flex items-center gap-4">
        <a
          href="#"
          class="text-[10px] font-bold uppercase tracking-[0.18em] text-[#2B3340] hover:text-[#D84F2A]"
          @click.prevent
        >
          Search
        </a>
        <span class="hidden h-4 w-px bg-[#E5E8ED] sm:block" />
        <a
          href="#"
          class="hidden text-[10px] font-bold uppercase tracking-[0.18em] text-[#2B3340] hover:text-[#D84F2A] sm:inline"
          @click.prevent
        >
          Sign in
        </a>
      </div>
    </div>
  </header>
</template>
