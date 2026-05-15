<script setup lang="ts">
type Article = {
  title: string
  subtitle: string
  slug: string
  image: string
  category: {
    title: string
    slug: string
  }
  tag: string
  readTime: number
  publishedAt: string
}

const route = useRoute()
const categorySlug = computed(() => String(route.params.category || 'istanbul'))
const activeFilter = ref('all')
const page = ref(1)

const category = computed(() => ({
  title: categorySlug.value === 'istanbul' ? 'Istanbul' : 'No category',
  slug: categorySlug.value,
  description:
    'Thoughtful Beyongo guides for choosing where to stay, what to explore, and how to move through the city with more intention.',
}))

const articles = computed<Article[]>(() => [
  {
    title: 'A quieter way to explore Istanbul',
    subtitle: 'Slower neighborhoods, thoughtful stays, and days that leave room for discovery.',
    slug: 'quiet-istanbul-guide',
    image: '',
    category: { title: category.value.title, slug: category.value.slug },
    tag: 'sightseeing',
    readTime: 7,
    publishedAt: '14 May 2026',
  },
  {
    title: 'Where to stay near the Bosphorus',
    subtitle: 'Calm waterside neighborhoods with easy access to local food, ferries, and cultural stops.',
    slug: 'where-to-stay-bosphorus',
    image: '',
    category: { title: category.value.title, slug: category.value.slug },
    tag: 'accommodations',
    readTime: 5,
    publishedAt: '09 May 2026',
  },
  {
    title: 'A thoughtful food day in Kadikoy',
    subtitle: 'Markets, coffee, bakeries, and dinner without rushing across the city.',
    slug: 'kadikoy-food-day',
    image: '',
    category: { title: category.value.title, slug: category.value.slug },
    tag: 'food',
    readTime: 6,
    publishedAt: '07 May 2026',
  },
  {
    title: 'Culture stops beyond the obvious',
    subtitle: 'Small museums, historic streets, and neighborhood walks for a deeper sense of place.',
    slug: 'istanbul-culture-stops',
    image: '',
    category: { title: category.value.title, slug: category.value.slug },
    tag: 'culture',
    readTime: 8,
    publishedAt: '02 May 2026',
  },
  {
    title: 'A ferry-first weekend plan',
    subtitle: 'Use the water as your guide for a slower, easier route between neighborhoods.',
    slug: 'ferry-first-weekend-plan',
    image: '',
    category: { title: category.value.title, slug: category.value.slug },
    tag: 'sightseeing',
    readTime: 4,
    publishedAt: '28 Apr 2026',
  },
  {
    title: 'A gentle evening in Beyoglu',
    subtitle: 'Low-pressure routes for dinner, galleries, and music after dark.',
    slug: 'gentle-evening-beyoglu',
    image: '',
    category: { title: category.value.title, slug: category.value.slug },
    tag: 'nightlife',
    readTime: 5,
    publishedAt: '24 Apr 2026',
  },
])

const filterItems = [
  { label: 'All', value: 'all' },
  { label: 'Sightseeing', value: 'sightseeing' },
  { label: 'Food', value: 'food' },
  { label: 'Culture', value: 'culture' },
  { label: 'Nightlife', value: 'nightlife' },
]

const featuredArticle = computed(() => articles.value[0] as Article)
const topGuides = computed(() => articles.value.slice(1, 4))
const topAccommodations = computed(() => articles.value.filter((article) => article.tag === 'accommodations'))
const filteredArticles = computed(() =>
  activeFilter.value === 'all'
    ? articles.value
    : articles.value.filter((article) => article.tag === activeFilter.value),
)

useSeoMeta({
  title: () => `${category.value.title} guides`,
  description: () => category.value.description,
})
</script>

<template>
  <div>
    <BeyongoHeader />

    <div class="mx-auto max-w-6xl px-4 pb-16 pt-7">
      <AppBreadcrumb
        :items="[
          { label: 'Home', to: '/' },
          { label: category.title },
        ]"
        class="mb-3"
      />

      <CategoryHero
        :title="category.title"
        :description="category.description"
      />

      <section class="mt-16">
        <CategoryFeatured :article="featuredArticle" />
      </section>

      <CategorySection title="Top guides" class="mt-16">
        <div class="grid gap-x-5 gap-y-8 md:grid-cols-2 lg:grid-cols-3">
          <ArticleCard
            v-for="article in topGuides"
            :key="article.slug"
            :article="article"
          />
        </div>
      </CategorySection>
    </div>

    <section class="bg-[#E8EEF6]/45 py-16">
      <div class="mx-auto max-w-6xl px-4">
        <CategorySection title="Top accommodations">
          <div class="grid gap-x-5 gap-y-8 md:grid-cols-2 lg:grid-cols-3">
            <ArticleCard
              v-for="article in topAccommodations"
              :key="article.slug"
              :article="article"
            />
          </div>
        </CategorySection>
      </div>
    </section>

    <div class="mx-auto max-w-6xl px-4 pb-8 pt-16">
      <section>
        <h2 class="text-xl font-bold text-highlighted md:text-2xl">All guides</h2>
        <div class="mt-6">
          <ArticleFilterTabs v-model="activeFilter" :items="filterItems" />
        </div>
        <div class="mt-6 grid gap-x-5 gap-y-8 md:grid-cols-2 lg:grid-cols-3">
          <ArticleCard
            v-for="article in filteredArticles"
            :key="article.slug"
            :article="article"
          />
        </div>
      </section>

      <AppPagination
        v-model:page="page"
        :total="filteredArticles.length"
        :items-per-page="6"
      />
    </div>
  </div>
</template>
