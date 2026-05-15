<script setup lang="ts">
type CmsAuthor = {
  name: string
  avatar: string
}

type CmsCategory = {
  title: string
  slug: string
}

type CmsArticle = {
  title: string
  subtitle: string
  slug: string
  author: CmsAuthor
  publishedAt: string
  readTime: number
  heroImage: string
  body: string
  category: CmsCategory
  metaTopic: string
  metaKeyWay: string
  metaBestFor: string
}

const route = useRoute()
const slug = computed(() => String(route.params.slug || ''))
const categorySlug = computed(() => String(route.params.category || ''))

const mockArticle: CmsArticle = {
  title: 'A quieter way to explore Istanbul',
  subtitle: 'A Beyongo guide to slower neighborhoods, thoughtful stays, and days that leave room for discovery.',
  slug: slug.value || 'quiet-istanbul-guide',
  author: {
    name: 'Beyongo Editorial',
    avatar: '',
  },
  publishedAt: '2026-05-14',
  readTime: 7,
  heroImage: '',
  body: 'article.body',
  category: {
    title: 'Istanbul',
    slug: categorySlug.value || 'istanbul',
  },
  metaTopic: 'Sustainable Travel',
  metaKeyWay: 'Intentional Immersion',
  metaBestFor: 'Thoughtful Explorers',
}

const mockRelatedArticles: CmsArticle[] = [
  {
    title: 'Where to stay near the Bosphorus',
    subtitle: 'Calm waterside neighborhoods with easy access to local food, ferries, and cultural stops.',
    slug: 'where-to-stay-bosphorus',
    author: mockArticle.author,
    publishedAt: '2026-05-09',
    readTime: 5,
    heroImage: '',
    body: 'article.body',
    category: mockArticle.category,
    metaTopic: 'Accommodations',
    metaKeyWay: 'Waterside Base',
    metaBestFor: 'First-time Visitors',
  },
  {
    title: 'A thoughtful food day in Kadikoy',
    subtitle: 'A simple route for markets, coffee, bakeries, and dinner without rushing across the city.',
    slug: 'kadikoy-food-day',
    author: mockArticle.author,
    publishedAt: '2026-05-07',
    readTime: 6,
    heroImage: '',
    body: 'article.body',
    category: mockArticle.category,
    metaTopic: 'Food',
    metaKeyWay: 'Local Rhythm',
    metaBestFor: 'Curious Diners',
  },
  {
    title: 'Culture stops beyond the obvious',
    subtitle: 'Small museums, historic streets, and neighborhood walks for a deeper sense of place.',
    slug: 'istanbul-culture-stops',
    author: mockArticle.author,
    publishedAt: '2026-05-02',
    readTime: 8,
    heroImage: '',
    body: 'article.body',
    category: mockArticle.category,
    metaTopic: 'Culture',
    metaKeyWay: 'Deeper Context',
    metaBestFor: 'Slow Travelers',
  },
  {
    title: 'A ferry-first weekend plan',
    subtitle: 'Use the water as your guide for a slower, easier route between neighborhoods.',
    slug: 'ferry-first-weekend-plan',
    author: mockArticle.author,
    publishedAt: '2026-04-28',
    readTime: 4,
    heroImage: '',
    body: 'article.body',
    category: mockArticle.category,
    metaTopic: 'Sightseeing',
    metaKeyWay: 'Soft Transit',
    metaBestFor: 'Weekend Planners',
  },
]

const { data: articleData } = await useAsyncData(`article-${slug.value}`, async () => mockArticle)
const { data: relatedArticles } = await useAsyncData(
  `article-related-${categorySlug.value}-${slug.value}`,
  async () => mockRelatedArticles.filter((article) => article.slug !== slug.value).slice(0, 3),
)

const article = computed(() => articleData.value || mockArticle)
const category = computed(() => article.value.category)

const formattedPublishedAt = computed(() => {
  if (!article.value.publishedAt) return 'No publishedAt'

  return new Intl.DateTimeFormat('en-GB', {
    day: '2-digit',
    month: 'short',
    year: 'numeric',
  }).format(new Date(article.value.publishedAt))
})

const heroProps = computed(() => ({
  title: article.value.title || 'No title',
  subtitle: article.value.subtitle || 'No subtitle',
  author: article.value.author || { name: 'No author', avatar: '' },
  publishedAt: formattedPublishedAt.value,
  readTime: article.value.readTime || 'No readTime',
  heroImage: article.value.heroImage || '',
  metaTopic: article.value.metaTopic || 'No metaTopic',
  metaKeyWay: article.value.metaKeyWay || 'No metaKeyWay',
  metaBestFor: article.value.metaBestFor || 'No metaBestFor',
}))

useSeoMeta({
  title: () => article.value.title || 'No title',
  description: () => article.value.subtitle || 'No subtitle',
})
</script>

<template>
  <article class="mx-auto max-w-6xl px-4 py-8">
    <AppBreadcrumb
      :items="[
        { label: 'Home', to: '/' },
        { label: category.title || 'No category', to: `/blog/${category.slug || categorySlug}` },
        { label: article.title || 'No title' },
      ]"
      class="mb-8"
    />

    <ArticleHero v-bind="heroProps" />

    <div class="mt-10 grid gap-10 lg:grid-cols-[1fr_320px]">
      <div>
        <ArticleBody>
          <div class="space-y-5 text-muted">
            <p id="overview">
              {{ article.body || 'No body' }}
            </p>
            <p id="where-to-start">
              Use this space as the future rich text renderer. For now, it shows the real CMS field name fallback requested in the brief.
            </p>
            <p id="local-notes">
              The full article body, custom cards, quotes, and steps will be connected after the CMS schema is ready.
            </p>
          </div>
        </ArticleBody>
      </div>

      <div class="hidden lg:block sticky top-16 self-start">
        <ArticleSidebar />
      </div>
    </div>

    <ArticleNewsletter class="mt-12" />

    <ArticleContinueExploring
      class="mt-12"
      :articles="relatedArticles || []"
    />
  </article>
</template>
